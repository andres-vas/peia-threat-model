# Abuse Cases finales

Se consolidan 15 escenarios arquitectónicos defensivos. No contienen payloads ni afirman explotación real.

## AC-SOF-001 — Saturación de la entrada pública

- **AC ID:** AC-SOF-001
- **Título:** Saturación de la entrada pública
- **Threat IDs:** TH-SOF-033
- **Actor:** Atacante remoto no autenticado o usuario malicioso
- **Objetivo:** Degradar o impedir el acceso a los servicios públicos de PEIA.
- **Precondiciones:** Acceso de red a endpoints públicos; capacidad de emitir solicitudes repetidas o costosas.
- **Vector:** Solicitudes HTTP/HTTPS repetidas contra Caddy, frontend, AI API, MCP o rutas públicas.
- **Método:** Abuso volumétrico o de costo asimétrico de entradas HTTP públicas, sin incluir payloads destructivos.
- **Secuencia:**

1. Identifica rutas públicas y operaciones con mayor costo relativo.

2. Emite tráfico sostenido o ráfagas concurrentes desde uno o varios orígenes.

3. Caddy y los servicios posteriores aceptan o procesan solicitudes hasta consumir conexiones, workers o capacidad.

4. Usuarios legítimos experimentan latencia, errores o indisponibilidad.

- **Impacto:** Pérdida de disponibilidad general, degradación operacional y posible propagación a workers o dependencias.
- **Controles principales:** Existentes: Caddy, autenticación en rutas protegidas y algunos rate limits. Preventivo: Límites distribuidos por IP, identidad y ruta; WAF/CDN; timeouts; límites de cuerpo y concurrencia; aislamiento de pools. Detectivo: Métricas de tasa, latencia, saturación y rechazos; alertas por anomalías y eventos de rate limit centralizados. Correctivo: Bloquear orígenes abusivos, reducir temporalmente rutas costosas, escalar capacidad y preservar evidencia de tráfico.

## AC-SOF-002 — Agotamiento de capacidad IA y cuota de proveedor

- **AC ID:** AC-SOF-002
- **Título:** Agotamiento de capacidad IA y cuota de proveedor
- **Threat IDs:** TH-SOF-029
- **Actor:** Usuario autenticado malicioso o actor con API/project key válida
- **Objetivo:** Agotar capacidad local, contexto, tokens o cuota/costo del proveedor.
- **Precondiciones:** Credencial o acceso permitido a inferencia/RAG; posibilidad de repetir solicitudes o ampliar contexto.
- **Vector:** API call, prompt, retrieval o invocación MCP hacia AI API y Gateway.
- **Método:** Uso abusivo de funciones autorizadas con cargas válidas pero desproporcionadas.
- **Secuencia:**

1. Obtiene acceso legítimo o una key reutilizable.

2. Formula solicitudes repetidas con contexto, retrieval o generación de alto costo.

3. Gateway despacha a Ollama o proveedores y consume workers, tokens o cuota.

4. El consumo acumulado reduce capacidad para otros tenants o genera costo no previsto.

- **Impacto:** Indisponibilidad de IA/RAG, incremento de costos y afectación entre tenants si la cuota es compartida.
- **Controles principales:** Existentes: Rate limit por tenant, límites configurables, licencia y whitelist de modelos. Preventivo: Cuotas por tenant/proyecto/modelo, límites de tokens y contexto, rate limiting distribuido, colas acotadas y circuit breakers. Detectivo: Alertas por consumo anómalo, costo, longitud de contexto, cola, tiempo de inferencia y concentración por key. Correctivo: Suspender la key o tenant abusivo, cancelar trabajos, activar degradación controlada y reconciliar consumo/cuota.

## AC-SOF-003 — Prompt injection directa o indirecta en IA/RAG

- **AC ID:** AC-SOF-003
- **Título:** Prompt injection directa o indirecta en IA/RAG
- **Threat IDs:** TH-SOF-011
- **Actor:** Usuario malicioso, autor de documento no confiable o fuente de conocimiento comprometida
- **Objetivo:** Alterar las instrucciones efectivas del pipeline IA y controlar o sesgar su respuesta.
- **Precondiciones:** Capacidad de enviar un prompt, cargar un documento o influir Project Knowledge recuperado por RAG.
- **Vector:** Prompt, contenido documental, chunk recuperado o Project Knowledge incorporado al contexto.
- **Método:** Confusión entre instrucciones y datos no confiables dentro del contexto del modelo.
- **Secuencia:**

1. Introduce instrucciones adversas en una consulta, documento o fuente de conocimiento.

2. El contenido pasa validaciones funcionales y se almacena o recupera.

3. El constructor de prompt combina instrucciones confiables y contenido no confiable sin separación suficiente.

4. El modelo prioriza o sigue el contenido adverso y produce una respuesta desviada.

- **Impacto:** Respuestas manipuladas, posible divulgación contextual y pérdida de integridad del servicio IA; no se presume ejecución de acciones externas.
- **Controles principales:** Existentes: Política de modelo/confidencialidad y validación de respuesta forman parte del diseño. Preventivo: Separación estricta de instrucciones/datos, plantillas inmutables, filtros de contexto, provenance, allowlist de herramientas y validación de salida. Detectivo: Telemetría de seguridad de prompts, detección de patrones de override, trazabilidad de chunks y revisión de respuestas anómalas. Correctivo: Retirar la fuente contaminada, invalidar índices/chunks, reconstruir contexto y revisar sesiones y respuestas afectadas.

## AC-SOF-004 — Acceso cross-tenant por contexto u autorización de objeto insuficiente

- **AC ID:** AC-SOF-004
- **Título:** Acceso cross-tenant por contexto u autorización de objeto insuficiente
- **Threat IDs:** TH-SOF-021, TH-SOF-034, TH-SOF-007
- **Actor:** Usuario autenticado malicioso de un tenant o proyecto
- **Objetivo:** Leer o modificar recursos pertenecientes a otro tenant/proyecto.
- **Precondiciones:** Cuenta válida; conocimiento o descubrimiento de un identificador ajeno; endpoint que acepte tenant/resource ID.
- **Vector:** HTTP/API request con tenant, project o resource ID manipulado en header, parámetro, ruta o cuerpo.
- **Método:** Manipulación de referencias y contexto en una solicitud autenticada para probar fallos de tenant binding y object-level authorization.
- **Secuencia:**

1. Autentica una cuenta legítima del tenant A.

2. Obtiene o adivina un identificador asociado al tenant B.

3. Sustituye tenant, proyecto u objeto en una solicitud permitida.

4. El servidor resuelve el contexto o recupera el objeto sin vincularlo de nuevo a la identidad y membership.

5. Recibe datos, metadata, contexto RAG o capacidad de modificación del tenant B.

- **Impacto:** Pérdida de confidencialidad/integridad multi-tenant y escalamiento horizontal.
- **Controles principales:** Existentes: Membership, RBAC, tenant/project keys y diseño de tenant context.; RBAC, memberships, permisos por objeto y asserts de tenant observados.; Modelos de membership, RBAC, permisos y resolución de tenant observados. Preventivo: Tenant binding exclusivamente server-side, filtros obligatorios por ownership, autorización a nivel de objeto y pruebas negativas sistemáticas. Detectivo: Alertas por mismatch identidad-tenant, accesos denegados repetidos, consultas cross-tenant y auditoría de objeto. Correctivo: Bloquear sesión, aislar tenant, revocar tokens, revertir cambios, determinar exposición y notificar el incidente según alcance.

## AC-SOF-005 — Reutilización de key y bypass de proyecto o administración Gateway

- **AC ID:** AC-SOF-005
- **Título:** Reutilización de key y bypass de proyecto o administración Gateway
- **Threat IDs:** TH-SOF-037, TH-SOF-004
- **Actor:** Actor con API/project key robada, tenant autenticado o administrador limitado
- **Objetivo:** Operar bajo otro proyecto o alcanzar funciones Gateway fuera del scope concedido.
- **Precondiciones:** Key válida obtenida o acceso parcial; binding, scope, expiración o ruta administrativa insuficientes.
- **Vector:** Authorization header, API key, project key o llamada a ruta administrativa Gateway.
- **Método:** Replay contextual de credenciales y selección de proyecto/ruta fuera de su alcance autorizado.
- **Secuencia:**

1. Obtiene una key de servicio, tenant o proyecto.

2. La presenta con un project ID diferente o ante una ruta de mayor privilegio.

3. El Gateway valida la credencial pero no aplica completamente scope, binding o tipo de operación.

4. Accede a modelos, conocimiento, configuración o capacidad ajenos.

- **Impacto:** Escalamiento entre proyectos, uso no autorizado de RAG/modelos y exposición o cambio de configuración.
- **Controles principales:** Existentes: Doble autenticación tenant/proyecto, tenant context, admin key y whitelist de modelos.; Resolución TenantContext, rechazo de tenant deshabilitado, doble autenticación de proyecto y keys cifradas. Preventivo: Keys de corta vida y alcance mínimo, binding criptográfico tenant-proyecto-ruta, rotación, autorización por operación y separación admin. Detectivo: Detección de uso de key desde proyectos/orígenes atípicos, alertas de rutas admin y auditoría de cambios. Correctivo: Revocar y rotar keys, bloquear ruta/actor, revertir configuración y revisar accesos históricos asociados.

## AC-SOF-006 — Egreso indebido de datos a proveedor externo

- **AC ID:** AC-SOF-006
- **Título:** Egreso indebido de datos a proveedor externo
- **Threat IDs:** TH-SOF-022, TH-SOF-012
- **Actor:** Usuario autenticado malicioso, administrador con política manipulada o proceso comprometido
- **Objetivo:** Hacer que prompts, documentos, chunks o metadata que deberían permanecer locales sean enviados a un proveedor externo.
- **Precondiciones:** Solicitud con datos sensibles; provider externo configurado; política de modelo/confidencialidad modificable o aplicada de forma incompleta.
- **Vector:** Prompt/API call y selección de provider/policy a través del Gateway.
- **Método:** Desalineación entre clasificación, política de confidencialidad y decisión de egress del dispatcher.
- **Secuencia:**

1. Prepara una solicitud con contenido que requiere procesamiento local.

2. Manipula o aprovecha una política, clasificación o selección de provider incorrecta.

3. El confidentiality gate permite el despacho externo.

4. Gateway envía prompt, contexto o metadata a OpenAI/Anthropic.

- **Impacto:** Divulgación a tercero, incumplimiento de política y exposición de información de tenant/proyecto.
- **Controles principales:** Existentes: Confidentiality gate, providers opcionales, HTTPS y project policy.; Whitelist global, project policies y confidentiality gate observados. Preventivo: Policy enforcement fail-closed, clasificación explícita, minimización, allowlist de provider por proyecto y DLP de egress. Detectivo: Logs de decisión del gate, alertas de egress sensible, conciliación provider-proyecto y trazabilidad sin registrar secretos. Correctivo: Detener egress, corregir política, rotar credenciales si aplica, identificar datos enviados y activar respuesta contractual/privacidad.

## AC-SOF-007 — Divulgación de documentos, OCR o derivados

- **AC ID:** AC-SOF-007
- **Título:** Divulgación de documentos, OCR o derivados
- **Threat IDs:** TH-SOF-024
- **Actor:** Usuario autenticado malicioso, proceso comprometido o tercero con acceso indebido
- **Objetivo:** Obtener originales, OCR, contenido extraído, metadata o derivados no autorizados.
- **Precondiciones:** Acceso a una función de descarga/revisión, identificador de documento o integración documental.
- **Vector:** API de documento, descarga, storage, tarea asíncrona o integración DocuWare.
- **Método:** Abuso de referencias/ACL en el ciclo documental, considerando cada derivado como activo independiente.
- **Secuencia:**

1. Autentica o compromete un proceso con acceso documental.

2. Solicita un documento/derivado mediante referencia ajena o ruta de integración.

3. La autorización, ACL o ownership no se aplica uniformemente al original y todos sus derivados.

4. El sistema retorna, archiva o transmite contenido no autorizado.

- **Impacto:** Exposición de información sensible, privacidad y posible propagación a terceros.
- **Controles principales:** Existentes: AuthZ tenant/recurso, ownership en DB y credenciales DocuWare. Preventivo: AuthZ por objeto y derivado, ACL consistentes, cifrado, URLs de corta vida, retención mínima y binding tenant en integraciones. Detectivo: Auditoría de descarga/exportación, alertas por volumen o tenant mismatch e integridad de accesos DocuWare. Correctivo: Revocar acceso, detener exportación, aislar documentos, preservar logs y evaluar/notificar la exposición.

## AC-SOF-008 — Carga documental manipulada y agotamiento del pipeline

- **AC ID:** AC-SOF-008
- **Título:** Carga documental manipulada y agotamiento del pipeline
- **Threat IDs:** TH-SOF-013, TH-SOF-030
- **Actor:** Usuario autenticado malicioso o fuente documental comprometida
- **Objetivo:** Alterar resultados documentales o consumir desproporcionadamente CPU, memoria, cola y almacenamiento.
- **Precondiciones:** Permiso para cargar o sincronizar documentos; pipeline procesa formatos complejos o metadata controlable.
- **Vector:** Upload documental, archivo complejo, metadata o documento desde DocuWare.
- **Método:** Abuso de complejidad y confianza en contenido/metadata durante validación y procesamiento asíncrono.
- **Secuencia:**

1. Carga o sincroniza un archivo válido en apariencia pero manipulado o excepcionalmente costoso.

2. El pipeline acepta formato, tamaño, metadata o estructura sin límites suficientes.

3. Workers realizan extracción/OCR y consumen recursos o generan resultados alterados.

4. La cola se retrasa, el storage crece o los derivados pierden integridad.

- **Impacto:** Pérdida de integridad documental, indisponibilidad de workers y consumo de recursos compartidos.
- **Controles principales:** Existentes: Validación de archivo, ownership en PostgreSQL y separación de original/derivados.; Validación y límites de archivo/contexto observados de forma general. Preventivo: Allowlist de formatos, límites de tamaño/páginas/tiempo, sandbox de parser, escaneo, cuotas y validación de metadata/resultado. Detectivo: Alertas por tiempo de OCR, expansión, errores de parser, colas, reintentos y consumo por tenant. Correctivo: Cancelar y aislar jobs/archivos, limpiar derivados, restaurar estado y bloquear temporalmente la fuente.

## AC-SOF-009 — Manipulación de roles y escalamiento administrativo

- **AC ID:** AC-SOF-009
- **Título:** Manipulación de roles y escalamiento administrativo
- **Threat IDs:** TH-SOF-008, TH-SOF-035
- **Actor:** Usuario autenticado con privilegios parciales, administrador de tenant malicioso o cuenta administrativa comprometida
- **Objetivo:** Obtener o conceder privilegios superiores para operar el plano administrativo.
- **Precondiciones:** Acceso a una cuenta válida y a una operación de membership, rol o administración.
- **Vector:** API/UI administrativa, cambio de membership/rol o llamada privilegiada Console/Gateway.
- **Método:** Abuso de transiciones de rol y controles de función administrativa, sin asumir una ruta pública.
- **Secuencia:**

1. Compromete o usa una cuenta con permisos parciales.

2. Solicita un cambio de membership/rol o invoca una función administrativa.

3. La autorización, segregación o aprobación no restringe la transición sensible.

4. Obtiene o asigna privilegios para modificar tenants, claves, licencias, modelos o datos.

- **Impacto:** Control del plano administrativo, cambios sobre múltiples tenants y exposición de secretos/configuración.
- **Controles principales:** Existentes: RBAC, memberships, segregación de funciones y permisos por objeto observados.; IsAuthenticated por defecto; permisos staff/superuser/partner en operaciones sensibles; RBAC. Preventivo: Matriz RBAC explícita, deny-by-default, MFA administrativo, step-up auth, aprobación dual y separación de funciones. Detectivo: Auditoría inmutable de roles/cambios, alertas de elevación, sesiones privilegiadas anómalas y revisión periódica. Correctivo: Deshabilitar cuenta, revertir roles/cambios, rotar secretos afectados y revisar todas las acciones privilegiadas.

## AC-SOF-010 — Compromiso de identidad web y abuso de autenticación

- **AC ID:** AC-SOF-010
- **Título:** Compromiso de identidad web y abuso de autenticación
- **Threat IDs:** TH-SOF-001, TH-SOF-020, TH-SOF-002, TH-SOF-028
- **Actor:** Atacante remoto, extensión/proceso de navegador malicioso o actor con credenciales obtenidas
- **Objetivo:** Suplantar a un usuario o degradar la autenticación mediante extracción/replay de token, credenciales o intentos masivos.
- **Precondiciones:** Token accesible/vigente, credencial obtenida o endpoint de login alcanzable.
- **Vector:** Browser Storage, Authorization header y solicitudes repetidas al login.
- **Método:** Replay de bearer/token persistido, credential abuse y automatización contra autenticación.
- **Secuencia:**

1. Obtiene un token/credencial o automatiza intentos de autenticación.

2. Presenta el material en una nueva sesión o concentra solicitudes en login.

3. Si expiración, MFA, rate limit o detección son insuficientes, el sistema acepta replay o consume capacidad.

4. El actor usa el alcance de la cuenta o degrada el acceso legítimo.

- **Impacto:** Toma de cuenta, exposición/modificación con alcance del usuario e indisponibilidad de autenticación.
- **Controles principales:** Existentes: Token DRF; logout elimina tokens; autenticación requerida en rutas protegidas.; Redacción de logs; logout revoca tokens; controles del origin del navegador.; Rate scope de login en AI; MFA TOTP disponible; autenticación Token/Session en Console.; Rate scope login observado en AI; límites configurables. Preventivo: Tokens de corta vida en cookie HttpOnly/SameSite cuando aplique, rotación/revocación, MFA, protección anti-bot y rate limit distribuido. Detectivo: Alertas de login/replay por dispositivo, geografía y velocidad; detección de credential stuffing y sesiones simultáneas. Correctivo: Revocar sesiones/tokens, bloquear origen/cuenta, forzar reset y revisar acciones posteriores a la autenticación.

## AC-SOF-011 — Envenenamiento o divulgación de conocimiento RAG

- **AC ID:** AC-SOF-011
- **Título:** Envenenamiento o divulgación de conocimiento RAG
- **Threat IDs:** TH-SOF-010, TH-SOF-023
- **Actor:** Usuario autorizado malicioso, conector/proceso comprometido o usuario de otro proyecto
- **Objetivo:** Contaminar el conocimiento recuperado o extraer embeddings/chunks de otro proyecto.
- **Precondiciones:** Capacidad de cargar conocimiento, consultar retrieval o influir un conector; provenance o filtros insuficientes.
- **Vector:** Project Knowledge, carga de chunks, búsqueda híbrida y consultas RAG.
- **Método:** Manipulación y consulta de stores RAG aprovechando provenance o aislamiento lógico incompletos.
- **Secuencia:**

1. Inserta contenido controlado o consulta referencias fuera de su proyecto.

2. El store acepta chunks sin provenance/revisión suficiente o la búsqueda omite un filtro de proyecto.

3. El retrieval incorpora contenido contaminado o ajeno al contexto.

4. La respuesta queda sesgada o revela conocimiento/metadata no autorizados.

- **Impacto:** Pérdida de integridad de respuestas y confidencialidad de conocimiento/embeddings.
- **Controles principales:** Existentes: Resolución de proyecto, políticas y búsqueda híbrida gobernada.; Project resolution, key por proyecto y políticas de retrieval. Preventivo: Namespaces y filtros obligatorios por proyecto, provenance firmado, revisión de ingestión y autorización en cada retrieval. Detectivo: Trazabilidad chunk-fuente-proyecto, alertas por cruces de namespace y monitoreo de cambios/consultas anómalas. Correctivo: Despublicar conocimiento, reconstruir índices, purgar cachés y evaluar respuestas/consultas afectadas.

## AC-SOF-012 — Compromiso de supply chain e Installer privilegiado

- **AC ID:** AC-SOF-012
- **Título:** Compromiso de supply chain e Installer privilegiado
- **Threat IDs:** TH-SOF-006, TH-SOF-014, TH-SOF-036
- **Actor:** Proveedor/Registry comprometido, operador local malicioso o atacante con control de publicación/Installer
- **Objetivo:** Introducir un manifest, imagen o actualización alterada y aprovechar privilegios Docker/host.
- **Precondiciones:** Control de Registry, credenciales/publicación, canal de update o ejecución local del Installer; verificación no fail-closed.
- **Vector:** Manifest, registry artifact, imagen Docker o paquete de actualización.
- **Método:** Sustitución de artefacto en la cadena de suministro seguida de ejecución por un componente privilegiado.
- **Secuencia:**

1. Compromete o suplanta una fuente de artefactos, manifest o actualización.

2. Publica o entrega un artefacto distinto del autorizado.

3. Installer acepta el contenido si firma, digest o procedencia no son obligatorios y fail-closed.

4. El artefacto se ejecuta con acceso Docker/filesystem y afecta el host o stack.

- **Impacto:** Control del host on-premise, secretos, disponibilidad y todos los componentes locales.
- **Controles principales:** Existentes: HTTPS/auth de registry; soporte de digest, Cosign y manifest Ed25519.; Manifest Ed25519; SHA-256; soporte de Cosign/digest.; Preflight, manifest Ed25519, permisos 0600 y separación de secretos. Preventivo: Verificación obligatoria de firma y digest, provenance/SBOM, publicación protegida, allowlist, mínimo privilegio y aislamiento Docker. Detectivo: Alertas de firma/digest, monitoreo de integridad, auditoría de Registry y cambios en contenedores/host. Correctivo: Detener despliegue, aislar host, rollback a artefacto verificado, rotar secretos y reconstruir desde baseline confiable.

## AC-SOF-013 — Divulgación de secretos locales del License Agent

- **AC ID:** AC-SOF-013
- **Título:** Divulgación de secretos locales del License Agent
- **Threat IDs:** TH-SOF-025
- **Actor:** Operador local malicioso, proceso comprometido o usuario con acceso indebido al host
- **Objetivo:** Obtener refresh token, clave privada, certificado o material de licencia local.
- **Precondiciones:** Acceso al host, backup, filesystem, memoria o logs con permisos insuficientes.
- **Vector:** Secret Store Agent, archivos de estado, backup o logging local.
- **Método:** Acceso local a material criptográfico y tokens persistentes fuera del proceso autorizado.
- **Secuencia:**

1. Obtiene ejecución o acceso parcial al host cliente.

2. Enumera archivos, backups, permisos, memoria o logs del Agent/Installer.

3. Extrae material sensible si ACL, cifrado o redacción son insuficientes.

4. Reutiliza el secreto para suplantación, acceso cloud o manipulación de licencia.

- **Impacto:** Suplantación del dispositivo, abuso de licencia y posible acceso a servicios de control.
- **Controles principales:** Existentes: Refresh token cifrado con AES-GCM y escritura atómica. Preventivo: Vault/keystore, ACL mínima, cifrado, tokens cortos/rotables, no inclusión en backups y redacción estricta. Detectivo: File integrity monitoring, alertas de acceso a secretos, uso anómalo de refresh token y auditoría del host. Correctivo: Revocar/rotar token, clave y certificados; aislar host; re-enrolar dispositivo y revisar accesos cloud.

## AC-SOF-014 — Interrupción de servicio por licencia, heartbeat o Registry

- **AC ID:** AC-SOF-014
- **Título:** Interrupción de servicio por licencia, heartbeat o Registry
- **Threat IDs:** TH-SOF-032
- **Actor:** Atacante de red, tercero comprometido, operador malicioso o fallo externo
- **Objetivo:** Impedir validación de licencia, heartbeat o acceso a artefactos para degradar el stack.
- **Precondiciones:** Dependencia disponible por red y tolerancia/failover insuficientes; capacidad de bloquear o alterar conectividad/servicio.
- **Vector:** Heartbeat, validación de licencia, acceso Registry o respuesta de dependencia.
- **Método:** Indisponibilidad de dependencias de control/supply chain y agotamiento de tolerancias.
- **Secuencia:**

1. Interrumpe o degrada la conectividad hacia Console, AI API o Registry.

2. Agent/Installer acumula fallos de heartbeat, licencia o descarga.

3. La política de tolerancia o caché no sostiene operación segura.

4. Servicios locales se degradan, bloquean o no pueden actualizarse.

- **Impacto:** Interrupción operativa on-premise y retraso de recuperación/actualización.
- **Controles principales:** Existentes: Gracia offline default de 72 h y validación local; snapshots/rollback diseñados. Preventivo: Grace period acotado, caché firmada, retries con backoff, redundancia, modo degradado seguro y artefactos previamente validados. Detectivo: Alertas de heartbeat ausente, fallos de licencia/Registry, SLO de dependencias y correlación multi-host. Correctivo: Conmutar a dependencia/caché válida, restaurar conectividad, reparar estado y reconciliar heartbeats/licencia.

## AC-SOF-015 — Divulgación de claims OIDC y secretos MFA

- **AC ID:** AC-SOF-015
- **Título:** Divulgación de claims OIDC y secretos MFA
- **Threat IDs:** TH-SOF-027
- **Actor:** Proceso/logging comprometido, administrador indebido o atacante con acceso a configuración/soporte
- **Objetivo:** Obtener claims sensibles, semillas TOTP o códigos de respaldo para facilitar suplantación.
- **Precondiciones:** Acceso a logs, base, configuración, respuesta OIDC o función administrativa que maneje material MFA.
- **Vector:** OIDC callback, almacenamiento de MFA, logs, exportación o soporte administrativo.
- **Método:** Exposición de material de identidad en persistencia, observabilidad o flujo administrativo.
- **Secuencia:**

1. Accede a una ruta, log, store o función que procesa claims/MFA.

2. Busca material sensible que no esté minimizado, cifrado o redactado.

3. Extrae claims, semilla o códigos de respaldo.

4. Usa la información para perfilar identidades o intentar superar un factor de autenticación.

- **Impacto:** Suplantación, debilitamiento de MFA y exposición de datos de identidad.
- **Controles principales:** Existentes: TOTP y códigos de respaldo implementados; campos sensibles cifrables. Preventivo: Cifrado de semillas, hashing cuando aplique, acceso mínimo, redacción, códigos de un uso y minimización de claims. Detectivo: Auditoría de lectura/exportación MFA, alertas de uso de recovery codes y acceso anómalo a configuración de identidad. Correctivo: Invalidar códigos/semillas, forzar re-enrolamiento, revocar sesiones y revisar logs/accesos afectados.
