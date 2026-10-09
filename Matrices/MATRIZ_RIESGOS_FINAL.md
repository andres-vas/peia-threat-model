# Matriz de riesgos final

| Rank | Threat ID | Amenaza | P | I | Score | Severidad |
|---:|---|---|---:|---:|---:|---|
| 1 | TH-SOF-011 | Prompt injection directa o indirecta modifica la operación de IA | 4 | 4 | 16 | Crítico |
| 2 | TH-SOF-029 | Agotamiento de modelos, contexto o cuota de proveedor | 4 | 4 | 16 | Crítico |
| 3 | TH-SOF-033 | Saturación de la entrada pública de PEIA | 4 | 4 | 16 | Crítico |
| 4 | TH-SOF-004 | Reutilización de API key o project key fuera de contexto | 3 | 5 | 15 | Crítico |
| 5 | TH-SOF-007 | Manipulación del tenant context suministrado por el cliente | 3 | 5 | 15 | Crítico |
| 6 | TH-SOF-008 | Manipulación de membership, rol o permiso de objeto | 3 | 5 | 15 | Crítico |
| 7 | TH-SOF-021 | Divulgación cross-tenant en stores o consultas compartidas | 3 | 5 | 15 | Crítico |
| 8 | TH-SOF-022 | Divulgación de prompts o contexto a proveedor externo | 3 | 5 | 15 | Crítico |
| 9 | TH-SOF-024 | Divulgación de documentos, OCR o derivados | 3 | 5 | 15 | Crítico |
| 10 | TH-SOF-034 | Escalamiento horizontal por bypass de autorización de objeto | 3 | 5 | 15 | Crítico |
| 11 | TH-SOF-037 | Bypass de boundary de proyecto o rutas administrativas Gateway | 3 | 5 | 15 | Crítico |
| 12 | TH-SOF-001 | Reutilización de token web extraído | 3 | 4 | 12 | Alto |
| 13 | TH-SOF-002 | Suplantación mediante credenciales obtenidas o fuerza bruta | 3 | 4 | 12 | Alto |
| 14 | TH-SOF-010 | Envenenamiento de Vector Store o Project Knowledge | 3 | 4 | 12 | Alto |
| 15 | TH-SOF-013 | Manipulación de archivo, metadatos o resultado documental | 3 | 4 | 12 | Alto |
| 16 | TH-SOF-020 | Divulgación de token desde Browser Storage | 3 | 4 | 12 | Alto |
| 17 | TH-SOF-023 | Divulgación de embeddings, chunks o conocimiento de proyecto | 3 | 4 | 12 | Alto |
| 18 | TH-SOF-030 | Agotamiento por archivos complejos o bombas de recursos | 3 | 4 | 12 | Alto |
| 19 | TH-SOF-032 | Interrupción por dependencia de heartbeat, licencia o Registry | 3 | 4 | 12 | Alto |
| 20 | TH-SOF-028 | Saturación de login y validación de identidad | 4 | 3 | 12 | Alto |
| 21 | TH-SOF-006 | Suplantación del Registry o de la fuente de artefactos | 2 | 5 | 10 | Alto |
| 22 | TH-SOF-012 | Manipulación de política de modelo o confidencialidad | 2 | 5 | 10 | Alto |
| 23 | TH-SOF-014 | Adulteración de manifest, imagen o paquete de actualización | 2 | 5 | 10 | Alto |
| 24 | TH-SOF-025 | Divulgación de refresh token, clave o certificado local | 2 | 5 | 10 | Alto |
| 25 | TH-SOF-027 | Divulgación de claims OIDC, semillas MFA o códigos de respaldo | 2 | 5 | 10 | Alto |
| 26 | TH-SOF-035 | Escalamiento vertical mediante cuenta o ruta administrativa | 2 | 5 | 10 | Alto |
| 27 | TH-SOF-036 | Abuso del Installer privilegiado o control de Docker | 2 | 5 | 10 | Alto |
| 28 | TH-SOF-018 | Repudio del ciclo de vida documental | 3 | 3 | 9 | Medio |
| 29 | TH-SOF-003 | Suplantación mediante identidad OIDC o mapeo de claims indebido | 2 | 4 | 8 | Medio |
| 30 | TH-SOF-005 | Suplantación de dispositivo o License Agent | 2 | 4 | 8 | Medio |
| 31 | TH-SOF-009 | Pérdida o manipulación del contexto de tenant en tareas asíncronas | 2 | 4 | 8 | Medio |
| 32 | TH-SOF-015 | Manipulación local de policy, secretos, estado o rollback | 2 | 4 | 8 | Medio |
| 33 | TH-SOF-016 | Repudio de operaciones administrativas | 2 | 4 | 8 | Medio |
| 34 | TH-SOF-026 | Divulgación de secretos o contenido sensible en logs | 2 | 4 | 8 | Medio |
| 35 | TH-SOF-031 | Agotamiento o interrupción de Redis y Celery | 2 | 4 | 8 | Medio |
| 36 | TH-SOF-017 | Repudio de inferencias y cambios de configuración del Gateway | 2 | 3 | 6 | Medio |
| 37 | TH-SOF-019 | Repudio de enrollment, update, revocación o rollback | 2 | 3 | 6 | Medio |

## Top 10

| Posición | Threat ID | Amenaza | Score | Severidad |
|---:|---|---|---:|---|
| 1 | TH-SOF-033 | Saturación de la entrada pública de PEIA | 16 | Crítico |
| 2 | TH-SOF-029 | Agotamiento de modelos, contexto o cuota de proveedor | 16 | Crítico |
| 3 | TH-SOF-011 | Prompt injection directa o indirecta modifica la operación de IA | 16 | Crítico |
| 4 | TH-SOF-021 | Divulgación cross-tenant en stores o consultas compartidas | 15 | Crítico |
| 5 | TH-SOF-034 | Escalamiento horizontal por bypass de autorización de objeto | 15 | Crítico |
| 6 | TH-SOF-007 | Manipulación del tenant context suministrado por el cliente | 15 | Crítico |
| 7 | TH-SOF-037 | Bypass de boundary de proyecto o rutas administrativas Gateway | 15 | Crítico |
| 8 | TH-SOF-022 | Divulgación de prompts o contexto a proveedor externo | 15 | Crítico |
| 9 | TH-SOF-024 | Divulgación de documentos, OCR o derivados | 15 | Crítico |
| 10 | TH-SOF-004 | Reutilización de API key o project key fuera de contexto | 15 | Crítico |

Resumen inherente: 11 críticos, 16 altos, 10 medios y 0 bajos.
