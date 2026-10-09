# PEIA — Modelo de amenazas

Repositorio académico de la asignatura **Seguridad en Aplicaciones**. Documenta el modelado de amenazas de una **Plataforma Empresarial de Inteligencia Artificial (PEIA)** y mantiene trazabilidad entre arquitectura, amenazas, riesgo, controles, casos de abuso y remediaciones.

> Por razones de confidencialidad, el nombre comercial del producto ha sido anonimizado en este repositorio y sustituido por la denominación Plataforma Empresarial de Inteligencia Artificial (PEIA).

## Objetivo y alcance

El modelo cubre la arquitectura cloud y on-premise, autenticación y sesiones, aislamiento multi-tenant, Gateway de IA y RAG, procesamiento documental, licenciamiento, instalación y actualización, dependencias de terceros y cadena de suministro. La entrega consolida **6 DFD**, **37 amenazas STRIDE**, **15 casos de abuso** y **22 remediaciones**.

Los códigos `TH-SOF-*`, `CTRL-SOF-*` y `REM-SOF-*` se conservan exclusivamente como identificadores internos canónicos para no romper la trazabilidad histórica. No representan el nombre público ni comercial de la plataforma.

## Modelo OWASP Threat Dragon

Los archivos se prepararon para **OWASP Threat Dragon 2.6.2**:

- [PEIA Threat Model v0.5](Threat_Dragon/PEIA_Threat_Model_v0.5.json): línea base de arquitectura, elementos, flujos y fronteras de confianza.
- [PEIA Threat Model v0.6 STRIDE](Threat_Dragon/PEIA_Threat_Model_v0.6_STRIDE.json): versión consolidada con las 37 amenazas y sus relaciones.

Los UUID, IDs de celdas, relaciones y códigos de trazabilidad fueron preservados durante la anonimización. Los JSON fueron validados sintácticamente y contrastados con sus fuentes. **Validación de reimportación en Threat Dragon pendiente de verificación manual.**

## Diagramas de flujo de datos

| Nivel | Vista | Diagrama |
|---|---|---|
| 0 | Contexto y actores externos | [dfd_nivel_0_contexto.png](Threat_Dragon/Diagramas/dfd_nivel_0_contexto.png) |
| 1 | Arquitectura general | [dfd_nivel_1_arquitectura.png](Threat_Dragon/Diagramas/dfd_nivel_1_arquitectura.png) |
| 2A | Identidad y aislamiento multi-tenant | [dfd_nivel_2a_identidad_multi_tenant.png](Threat_Dragon/Diagramas/dfd_nivel_2a_identidad_multi_tenant.png) |
| 2B | Gateway de IA y RAG | [dfd_nivel_2b_gateway_ia_rag.png](Threat_Dragon/Diagramas/dfd_nivel_2b_gateway_ia_rag.png) |
| 2C | Enrollment, licencia y actualización | [dfd_nivel_2c_enrollment_licencia_actualizacion.png](Threat_Dragon/Diagramas/dfd_nivel_2c_enrollment_licencia_actualizacion.png) |
| 2D | Pipeline documental | [dfd_nivel_2d_pipeline_documental.png](Threat_Dragon/Diagramas/dfd_nivel_2d_pipeline_documental.png) |

## Metodología y entregables

- **STRIDE:** [matriz de amenazas](Matrices/MATRIZ_STRIDE_FINAL.md) con categoría, activo, escenario, impacto y trazabilidad.
- **Priorización:** [matriz de riesgos y Top 10](Matrices/MATRIZ_RIESGOS_FINAL.md), conservando puntuaciones y orden canónico.
- **Casos de abuso:** [15 escenarios](Abuse_Cases/ABUSE_CASES_FINAL.md) vinculados a amenazas y activos.
- **Controles y riesgo residual:** [matriz de controles](Matrices/MATRIZ_CONTROLES_RIESGO_RESIDUAL_FINAL.md) con tratamiento y evaluación residual.
- **Remediaciones:** [matriz de remediación](Matrices/MATRIZ_REMEDIACION_ROADMAP_FINAL.md) con responsables sugeridos, evidencia, esfuerzo y horizonte.
- **Roadmap:** [vista de 12 meses](Roadmap/roadmap_mejoras_12_meses.png) derivada de las 22 remediaciones.
- **Anexos:** [criterios y trazabilidad complementaria](Anexos/ANEXOS_ESENCIALES.md).

## Estructura

```text
PEIA-threat-model/
├── README.md
├── Threat_Dragon/
│   ├── PEIA_Threat_Model_v0.5.json
│   ├── PEIA_Threat_Model_v0.6_STRIDE.json
│   └── Diagramas/
├── Matrices/
├── Abuse_Cases/
├── Roadmap/
└── Anexos/
```

## Estado de los controles

Los controles y las remediaciones son propuestas académicas. Su consideración en el riesgo residual no constituye evidencia de implementación; cada cierre requiere la evidencia indicada en la matriz correspondiente.
