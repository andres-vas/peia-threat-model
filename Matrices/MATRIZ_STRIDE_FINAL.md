# Matriz STRIDE final

| Threat ID | STRIDE | Elemento | DFD | Amenaza | Activo | Boundary |
|---|---|---|---|---|---|---|
| TH-SOF-001 | S | DS-10 Browser Storage | L0; L1; L2A | Reutilización de token web extraído | A-02 tokens y sesiones; A-01 identidad | TB-02, TB-08 |
| TH-SOF-002 | S | D2A-P02 Autenticación Django | L0; L1; L2A | Suplantación mediante credenciales obtenidas o fuerza bruta | A-01 identidades; A-07 configuración tenant; A-11 CRM | TB-01, TB-08 |
| TH-SOF-003 | S | D2A-P04 OIDC callback/validación | L0; L1; L2A | Suplantación mediante identidad OIDC o mapeo de claims indebido | A-01 identidad; A-10 claims OIDC | TB-07 |
| TH-SOF-004 | S | D2B-P02 Auth tenant/key | L0; L1; L2B | Reutilización de API key o project key fuera de contexto | A-03 service/API/project keys; A-05 prompts; A-09 RAG | TB-05, TB-13 |
| TH-SOF-005 | S | D2C-P06 License Agent | L0; L1; L2C | Suplantación de dispositivo o License Agent | A-04 clave de dispositivo; A-05 refresh token; A-08 licencia/policy | TB-10, TB-14 |
| TH-SOF-006 | S | DEP-08 Registry | L0; L1; L2C | Suplantación del Registry o de la fuente de artefactos | A-09 imágenes/artefactos; A-10 configuración; A-13 disponibilidad | TB-11 |
| TH-SOF-007 | T | D2A-P06 Resolver tenant context | L1; L2A | Manipulación del tenant context suministrado por el cliente | A-07 tenant/proyecto; A-04 documentos; A-11 CRM | TB-02, TB-13 |
| TH-SOF-008 | T | D2A-P07 Membership/RBAC | L1; L2A | Manipulación de membership, rol o permiso de objeto | A-01 identidades; A-07 roles/memberships; A-11 CRM | TB-08, TB-13 |
| TH-SOF-009 | T | P-03 Celery | L1; L2D | Pérdida o manipulación del contexto de tenant en tareas asíncronas | A-04 documentos; A-07 tenant; A-12 auditoría | TB-03, TB-13 |
| TH-SOF-010 | T | DS-05 Vector Store | L1; L2B | Envenenamiento de Vector Store o Project Knowledge | A-06 embeddings/chunks; A-09 contexto RAG; A-07 proyecto | TB-05, TB-13 |
| TH-SOF-011 | T | D2B-P08 Construir prompt | L1; L2B; L2D | Prompt injection directa o indirecta modifica la operación de IA | A-05 prompts/respuestas; A-04 documentos; A-09 contexto RAG | TB-05, TB-07 |
| TH-SOF-012 | T | D2B-P05 Política confidencialidad | L1; L2B | Manipulación de política de modelo o confidencialidad | A-03 keys; A-05 prompts; A-07 configuración; A-14 privacidad | TB-09, TB-13 |
| TH-SOF-013 | T | D2D-P03 Validación archivo | L1; L2D | Manipulación de archivo, metadatos o resultado documental | A-04 documentos y derivados; A-12 auditoría | TB-04, TB-13 |
| TH-SOF-014 | T | D2C-P04 Verificar manifest Ed25519 | L0; L1; L2C | Adulteración de manifest, imagen o paquete de actualización | A-09 artefactos; A-10 configuración; A-13 servicio | TB-11 |
| TH-SOF-015 | T | DS-09 Installer State/Backups | L1; L2C | Manipulación local de policy, secretos, estado o rollback | A-05 refresh token; A-08 policy/licencia; A-10 estado local | TB-14 |
| TH-SOF-016 | R | P-07 Console API | L0; L1 | Repudio de operaciones administrativas | A-11 CRM; A-12 auditoría; A-03 credenciales | TB-08, TB-09 |
| TH-SOF-017 | R | D2B-P11 Audit/logging | L1; L2B | Repudio de inferencias y cambios de configuración del Gateway | A-05 prompts/respuestas; A-07 proyecto; A-12 logs | TB-05, TB-09, TB-13 |
| TH-SOF-018 | R | D2D-P10 Auditoría | L1; L2D | Repudio del ciclo de vida documental | A-04 documentos; A-12 auditoría | TB-02, TB-04, TB-07, TB-13 |
| TH-SOF-019 | R | D2C-P08 Enrollment Start/Challenge | L1; L2C | Repudio de enrollment, update, revocación o rollback | A-08 licencia/manifest; A-09 artefactos; A-12 evidencia | TB-10, TB-11, TB-14 |
| TH-SOF-020 | I | DS-10 Browser Storage | L1; L2A | Divulgación de token desde Browser Storage | A-02 tokens; A-07 contexto tenant | TB-02, TB-08 |
| TH-SOF-021 | I | DS-01/07 PostgreSQL AI / DS-07 CRM | L1; L2A; L2B; L2D | Divulgación cross-tenant en stores o consultas compartidas | A-01…A-07; A-09; A-11 | TB-13 |
| TH-SOF-022 | I | D2B-P09 Provider dispatcher | L0; L1; L2B | Divulgación de prompts o contexto a proveedor externo | A-04 documentos; A-05 prompts; A-06 chunks; A-14 privacidad | TB-07, TB-13 |
| TH-SOF-023 | I | DS-06 Project Knowledge | L1; L2B | Divulgación de embeddings, chunks o conocimiento de proyecto | A-06 embeddings/chunks; A-09 contexto RAG | TB-05, TB-13 |
| TH-SOF-024 | I | DS-03 Storage documental | L1; L2D | Divulgación de documentos, OCR o derivados | A-04 documentos; A-06 extracción; A-14 privacidad | TB-04, TB-07, TB-13 |
| TH-SOF-025 | I | DS-08 Secret Store Agent | L1; L2C | Divulgación de refresh token, clave o certificado local | A-04 clave privada; A-05 refresh token; A-08 certificado/policy | TB-14 |
| TH-SOF-026 | I | D2B-P11 Audit/logging | L1; L2B; L2D | Divulgación de secretos o contenido sensible en logs | A-02/A-03 secretos; A-04/A-05 contenido; A-10 PII; A-12 logs | TB-07, TB-13 |
| TH-SOF-027 | I | DS-01/07 PostgreSQL AI / DS-07 CRM | L1; L2A | Divulgación de claims OIDC, semillas MFA o códigos de respaldo | A-10 claims/MFA seeds; A-01 identidad | TB-03, TB-07, TB-13 |
| TH-SOF-028 | D | D2A-P02 Autenticación Django | L0; L1; L2A | Saturación de login y validación de identidad | A-13 disponibilidad; A-01 identidad | TB-01, TB-07, TB-08 |
| TH-SOF-029 | D | D2B-P09 Provider dispatcher | L0; L1; L2B | Agotamiento de modelos, contexto o cuota de proveedor | A-13 capacidad; A-05 prompts; presupuesto de proveedor | TB-05, TB-06, TB-07 |
| TH-SOF-030 | D | D2D-P03 Validación archivo | L1; L2D | Agotamiento por archivos complejos o bombas de recursos | A-13 disponibilidad; A-04 storage documental | TB-02, TB-04 |
| TH-SOF-031 | D | DS-02 Redis | L1; L2D | Agotamiento o interrupción de Redis y Celery | A-13 disponibilidad; A-12 estado de trabajos | TB-03, TB-13 |
| TH-SOF-032 | D | D2C-P06 License Agent | L0; L1; L2C | Interrupción por dependencia de heartbeat, licencia o Registry | A-13 disponibilidad; A-08 licencia/policy; A-09 artefactos | TB-10, TB-11 |
| TH-SOF-033 | D | P-11 Reverse Proxy Caddy | L0; L1 | Saturación de la entrada pública de PEIA | A-13 disponibilidad general | TB-01 |
| TH-SOF-034 | E | D2A-P08 Permiso sobre recurso | L1; L2A; L2D | Escalamiento horizontal por bypass de autorización de objeto | A-04 documentos; A-07 tenant; A-11 CRM | TB-13 |
| TH-SOF-035 | E | P-07 Console API | L0; L1 | Escalamiento vertical mediante cuenta o ruta administrativa | A-03 claves; A-07 configuración; A-08 licencia; A-11 CRM | TB-08, TB-09 |
| TH-SOF-036 | E | D2C-P02 Installer | L0; L1; L2C | Abuso del Installer privilegiado o control de Docker | A-03/A-05 secretos; A-09 artefactos; A-10 host/configuración | TB-10, TB-11, TB-14 |
| TH-SOF-037 | E | D2B-P03 Resolver proyecto | L1; L2B | Bypass de boundary de proyecto o rutas administrativas Gateway | A-03 keys; A-07 proyecto; A-09 conocimiento; A-13 capacidad | TB-05, TB-09, TB-13 |

Distribución: S=6, T=9, R=4, I=8, D=6 y E=4. Total: 37 amenazas.
