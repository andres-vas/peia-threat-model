# Anexos esenciales

## A. Trust Boundaries

| ID | Descripción resumida |
|---|---|
| TB-01 | Internet/dispositivo a entrada pública |
| TB-02 | Browser/frontend a backend AI |
| TB-03 | Aplicación AI a base/cola |
| TB-04 | Procesos AI a storage documental |
| TB-05 | PEIA AI a Gateway |
| TB-06 | Gateway a Ollama/nodo IA |
| TB-07 | PEIA a terceros externos |
| TB-08 | Administrador a Console |
| TB-09 | Plano de control a plano de datos |
| TB-10 | Cloud PEIA a host cliente |
| TB-11 | Supply chain a Installer |
| TB-12 | License Agent a servicios locales |
| TB-13 | Aislamiento lógico multi-tenant/proyecto |
| TB-14 | Proceso local a secretos/estado privilegiado |

## B. Inventario compacto de componentes

| ID | Dominio | Componentes | Interfaces o función crítica |
|---|---|---|---|
| CMP-01 | Aplicación AI | AI Frontend, AI API | HTTPS/API, sesión y tenant context |
| CMP-02 | Procesamiento | Celery y Redis | Cola, workers y trabajos asíncronos |
| CMP-03 | Datos AI | PostgreSQL AI y storage documental | Metadatos, originales, OCR y derivados |
| CMP-04 | Gateway IA/RAG | Gateway API/Admin, PostgreSQL Gateway, Vector Store, Project Knowledge | Autorización por proyecto, políticas y retrieval |
| CMP-05 | Inferencia | Ollama, OpenAI y Anthropic | Modelos locales y proveedores externos |
| CMP-06 | Plano de control | Console Frontend/API y PostgreSQL CRM | Tenants, licencias, claves y configuración |
| CMP-07 | Host cliente | Installer, License Agent, Secret Store y backups | Despliegue, heartbeat, licencia y rollback |
| CMP-08 | Integraciones | OIDC IdP, DocuWare, SMTP/API y Registry | Identidad, archivo, mensajería y artefactos |

## C. Inventario compacto de activos críticos

| ID | Activo | Criticidad | Propiedad de seguridad principal |
|---|---|---|---|
| ACT-01 | Identidades, sesiones, roles y MFA | Crítica | Confidencialidad, integridad y autenticidad |
| ACT-02 | Tenant/project context, memberships y permisos | Crítica | Integridad y aislamiento |
| ACT-03 | API keys, project keys, tokens y secretos locales | Crítica | Confidencialidad y autenticidad |
| ACT-04 | Documentos originales, OCR y derivados | Crítica | Confidencialidad, integridad y disponibilidad |
| ACT-05 | Prompts, respuestas, chunks, embeddings y Project Knowledge | Alta | Confidencialidad e integridad |
| ACT-06 | CRM, metadatos y configuración | Alta | Integridad y disponibilidad |
| ACT-07 | Imágenes, manifests, firmas y paquetes | Crítica | Integridad y procedencia |
| ACT-08 | Host Docker, Agent, políticas y backups | Crítica | Integridad y disponibilidad |
| ACT-09 | Logs, auditoría y evidencia | Alta | Integridad, disponibilidad y no repudio |

## D. Arquitectura lógica y dependencias externas

La arquitectura lógica sigue el recorrido usuario o administrador → entrada pública → AI API/Console → servicios de aplicación y Gateway → stores/colas → inferencia, documentos y terceros. El plano cloud administra tenants, proyectos y licencias; el host cliente ejecuta Installer y License Agent detrás de TB-10/TB-14. TB-13 representa el aislamiento lógico multi-tenant que debe mantenerse en cada ruta, consulta, caché y trabajo. La referencia gráfica son los seis DFD del directorio `Threat_Dragon/Diagramas` y el modelo nativo `PEIA_Threat_Model_v0.6_STRIDE.json`.

Dependencias de terceros consideradas: OIDC IdP para identidad federada; DocuWare para gestión documental; OpenAI y Anthropic para inferencia externa; SMTP/API para mensajería; y Registry para distribución de artefactos. Su disponibilidad, retención, región y controles contractuales no se presumen validados.

## E. Trazabilidad Threat → AC → CTRL → REM

| Threat | AC | Controles recomendados | Remediaciones |
|---|---|---|---|
| TH-SOF-001 | AC-SOF-010 | CTRL-SOF-018, CTRL-SOF-020, CTRL-SOF-038 | REM-SOF-004, REM-SOF-010, REM-SOF-018, REM-SOF-020 |
| TH-SOF-002 | AC-SOF-010 | CTRL-SOF-017, CTRL-SOF-018, CTRL-SOF-020, CTRL-SOF-021, CTRL-SOF-032, CTRL-SOF-038 | REM-SOF-003, REM-SOF-004, REM-SOF-010, REM-SOF-018, REM-SOF-020, REM-SOF-021 |
| TH-SOF-003 | No aplica (riesgo medio) | CTRL-SOF-020, CTRL-SOF-032, CTRL-SOF-035, CTRL-SOF-037, CTRL-SOF-038 | REM-SOF-004, REM-SOF-010, REM-SOF-015, REM-SOF-017, REM-SOF-018, REM-SOF-020 |
| TH-SOF-004 | AC-SOF-005 | CTRL-SOF-019, CTRL-SOF-020, CTRL-SOF-038 | REM-SOF-004, REM-SOF-006, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-005 | No aplica (riesgo medio) | CTRL-SOF-019, CTRL-SOF-020, CTRL-SOF-030, CTRL-SOF-031, CTRL-SOF-037, CTRL-SOF-038 | REM-SOF-004, REM-SOF-006, REM-SOF-012, REM-SOF-014, REM-SOF-015, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-006 | AC-SOF-012 | CTRL-SOF-020, CTRL-SOF-028, CTRL-SOF-035, CTRL-SOF-037, CTRL-SOF-038 | REM-SOF-004, REM-SOF-011, REM-SOF-015, REM-SOF-017, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-007 | AC-SOF-004 | CTRL-SOF-016, CTRL-SOF-020, CTRL-SOF-038 | REM-SOF-004, REM-SOF-005, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-008 | AC-SOF-009 | CTRL-SOF-016, CTRL-SOF-017, CTRL-SOF-020, CTRL-SOF-038 | REM-SOF-004, REM-SOF-005, REM-SOF-010, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-009 | No aplica (riesgo medio) | CTRL-SOF-016, CTRL-SOF-020, CTRL-SOF-026, CTRL-SOF-033, CTRL-SOF-037, CTRL-SOF-038 | REM-SOF-004, REM-SOF-005, REM-SOF-009, REM-SOF-015, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-010 | AC-SOF-011 | CTRL-SOF-020, CTRL-SOF-023, CTRL-SOF-024, CTRL-SOF-038 | REM-SOF-001, REM-SOF-004, REM-SOF-007, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-011 | AC-SOF-003 | CTRL-SOF-020, CTRL-SOF-023, CTRL-SOF-024, CTRL-SOF-038 | REM-SOF-001, REM-SOF-004, REM-SOF-007, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-012 | AC-SOF-006 | CTRL-SOF-019, CTRL-SOF-020, CTRL-SOF-025, CTRL-SOF-038 | REM-SOF-004, REM-SOF-006, REM-SOF-008, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-013 | AC-SOF-008 | CTRL-SOF-020, CTRL-SOF-023, CTRL-SOF-026, CTRL-SOF-027, CTRL-SOF-038 | REM-SOF-001, REM-SOF-004, REM-SOF-009, REM-SOF-013, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-014 | AC-SOF-012 | CTRL-SOF-020, CTRL-SOF-028, CTRL-SOF-029, CTRL-SOF-038 | REM-SOF-004, REM-SOF-011, REM-SOF-012, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-015 | No aplica (riesgo medio) | CTRL-SOF-020, CTRL-SOF-030, CTRL-SOF-036, CTRL-SOF-038 | REM-SOF-004, REM-SOF-012, REM-SOF-016, REM-SOF-018, REM-SOF-020 |
| TH-SOF-016 | No aplica (riesgo medio) | CTRL-SOF-017, CTRL-SOF-020, CTRL-SOF-034, CTRL-SOF-038 | REM-SOF-004, REM-SOF-010, REM-SOF-018, REM-SOF-020 |
| TH-SOF-017 | No aplica (riesgo medio) | CTRL-SOF-020, CTRL-SOF-034, CTRL-SOF-038 | REM-SOF-004, REM-SOF-018, REM-SOF-020 |
| TH-SOF-018 | No aplica (riesgo medio) | CTRL-SOF-020, CTRL-SOF-026, CTRL-SOF-034, CTRL-SOF-038 | REM-SOF-004, REM-SOF-009, REM-SOF-018, REM-SOF-020 |
| TH-SOF-019 | No aplica (riesgo medio) | CTRL-SOF-020, CTRL-SOF-031, CTRL-SOF-034, CTRL-SOF-038 | REM-SOF-004, REM-SOF-014, REM-SOF-018, REM-SOF-020 |
| TH-SOF-020 | AC-SOF-010 | CTRL-SOF-018, CTRL-SOF-020, CTRL-SOF-038 | REM-SOF-004, REM-SOF-010, REM-SOF-018, REM-SOF-020 |
| TH-SOF-021 | AC-SOF-004 | CTRL-SOF-016, CTRL-SOF-020, CTRL-SOF-026, CTRL-SOF-038, CTRL-SOF-040 | REM-SOF-004, REM-SOF-005, REM-SOF-009, REM-SOF-018, REM-SOF-019, REM-SOF-020, REM-SOF-022 |
| TH-SOF-022 | AC-SOF-006 | CTRL-SOF-020, CTRL-SOF-025, CTRL-SOF-035, CTRL-SOF-037, CTRL-SOF-038, CTRL-SOF-040 | REM-SOF-004, REM-SOF-008, REM-SOF-015, REM-SOF-017, REM-SOF-018, REM-SOF-019, REM-SOF-020 |
| TH-SOF-023 | AC-SOF-011 | CTRL-SOF-020, CTRL-SOF-024, CTRL-SOF-038, CTRL-SOF-040 | REM-SOF-004, REM-SOF-007, REM-SOF-018, REM-SOF-019, REM-SOF-020, REM-SOF-022 |
| TH-SOF-024 | AC-SOF-007 | CTRL-SOF-016, CTRL-SOF-020, CTRL-SOF-025, CTRL-SOF-026, CTRL-SOF-035, CTRL-SOF-036, CTRL-SOF-038, CTRL-SOF-040 | REM-SOF-004, REM-SOF-005, REM-SOF-008, REM-SOF-009, REM-SOF-016, REM-SOF-017, REM-SOF-018, REM-SOF-019, REM-SOF-020, REM-SOF-022 |
| TH-SOF-025 | AC-SOF-013 | CTRL-SOF-019, CTRL-SOF-020, CTRL-SOF-030, CTRL-SOF-037, CTRL-SOF-038 | REM-SOF-004, REM-SOF-006, REM-SOF-012, REM-SOF-015, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-026 | No aplica (riesgo medio) | CTRL-SOF-020, CTRL-SOF-034, CTRL-SOF-038, CTRL-SOF-040 | REM-SOF-004, REM-SOF-018, REM-SOF-019, REM-SOF-020 |
| TH-SOF-027 | AC-SOF-015 | CTRL-SOF-017, CTRL-SOF-020, CTRL-SOF-032, CTRL-SOF-035, CTRL-SOF-038, CTRL-SOF-040 | REM-SOF-004, REM-SOF-010, REM-SOF-017, REM-SOF-018, REM-SOF-019, REM-SOF-020 |
| TH-SOF-028 | AC-SOF-010 | CTRL-SOF-018, CTRL-SOF-020, CTRL-SOF-021, CTRL-SOF-038, CTRL-SOF-039 | REM-SOF-002, REM-SOF-003, REM-SOF-004, REM-SOF-010, REM-SOF-018, REM-SOF-020, REM-SOF-021 |
| TH-SOF-029 | AC-SOF-002 | CTRL-SOF-019, CTRL-SOF-020, CTRL-SOF-022, CTRL-SOF-037, CTRL-SOF-038, CTRL-SOF-039 | REM-SOF-002, REM-SOF-004, REM-SOF-006, REM-SOF-015, REM-SOF-018, REM-SOF-020, REM-SOF-021, REM-SOF-022 |
| TH-SOF-030 | AC-SOF-008 | CTRL-SOF-020, CTRL-SOF-027, CTRL-SOF-038, CTRL-SOF-039 | REM-SOF-002, REM-SOF-004, REM-SOF-013, REM-SOF-018, REM-SOF-020, REM-SOF-021 |
| TH-SOF-031 | No aplica (riesgo medio) | CTRL-SOF-020, CTRL-SOF-022, CTRL-SOF-027, CTRL-SOF-033, CTRL-SOF-036, CTRL-SOF-037, CTRL-SOF-038, CTRL-SOF-039 | REM-SOF-002, REM-SOF-004, REM-SOF-013, REM-SOF-015, REM-SOF-016, REM-SOF-018, REM-SOF-020, REM-SOF-021 |
| TH-SOF-032 | AC-SOF-014 | CTRL-SOF-020, CTRL-SOF-028, CTRL-SOF-031, CTRL-SOF-035, CTRL-SOF-036, CTRL-SOF-037, CTRL-SOF-038 | REM-SOF-004, REM-SOF-011, REM-SOF-014, REM-SOF-015, REM-SOF-016, REM-SOF-017, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-033 | AC-SOF-001 | CTRL-SOF-020, CTRL-SOF-021, CTRL-SOF-022, CTRL-SOF-038, CTRL-SOF-039 | REM-SOF-002, REM-SOF-003, REM-SOF-004, REM-SOF-018, REM-SOF-020, REM-SOF-021 |
| TH-SOF-034 | AC-SOF-004 | CTRL-SOF-016, CTRL-SOF-020, CTRL-SOF-038 | REM-SOF-004, REM-SOF-005, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-035 | AC-SOF-009 | CTRL-SOF-017, CTRL-SOF-019, CTRL-SOF-020, CTRL-SOF-038 | REM-SOF-004, REM-SOF-006, REM-SOF-010, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-036 | AC-SOF-012 | CTRL-SOF-020, CTRL-SOF-028, CTRL-SOF-029, CTRL-SOF-030, CTRL-SOF-036, CTRL-SOF-037, CTRL-SOF-038 | REM-SOF-004, REM-SOF-011, REM-SOF-012, REM-SOF-015, REM-SOF-016, REM-SOF-018, REM-SOF-020, REM-SOF-022 |
| TH-SOF-037 | AC-SOF-005 | CTRL-SOF-019, CTRL-SOF-020, CTRL-SOF-024, CTRL-SOF-038 | REM-SOF-004, REM-SOF-006, REM-SOF-007, REM-SOF-018, REM-SOF-020, REM-SOF-022 |

## F. Incertidumbres preservadas

TLS/mTLS interno; obligatoriedad de MFA; cobertura exhaustiva de AuthZ; WAF/CDN; SIEM; scanning/sandbox documental; rate limiting distribuido; secrets management; cifrado en reposo; enforcement de firmas; backups/rollback; observabilidad; región, retención y controles de terceros. Ninguna se declara resuelta sin evidencia.

## G. Validación técnica y nota sobre imágenes

Se revisaron 6/6 DFD, se consolidaron 37 amenazas STRIDE sin IDs duplicados y se comprobaron 0 referencias locales rotas. Los duplicados semánticos fueron fusionados durante la consolidación y cada amenaza conserva la cadena Threat → Element → DFD. Esta es una validación técnica interna basada en los seis repositorios y los artefactos generados; no constituye validación independiente de terceros.

Las seis imágenes incluidas son renders reales de las especificaciones Mermaid canónicas de los DFD de Etapa 2 y corresponden a L0, L1 y L2A–D. No son capturas de la interfaz Threat Dragon. El artefacto nativo entregado es el JSON v0.6. Las seis capturas directas desde Threat Dragon permanecen **PENDIENTES DE VALIDACIÓN MANUAL**.
