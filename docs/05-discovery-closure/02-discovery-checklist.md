# Discovery Checklist

## Objetivo

Este documento proporciona una lista de verificación para confirmar que la fase de **Discovery** se encuentra completa y que el proyecto dispone de toda la información necesaria para iniciar la fase de **Technical Design**.

Su propósito es asegurar que el dominio, los requisitos funcionales y las capacidades técnicas han sido analizados de forma suficiente, reduciendo la incertidumbre antes de comenzar el diseño de la solución.

---

# Estado General

| Área | Estado |
|-------|--------|
| Domain Discovery | ☐ |
| Functional Analysis | ☐ |
| Technical Analysis | ☐ |
| Discovery Closure | ☐ |

---

# 1. Domain Discovery

## Comprensión del dominio

| Verificación | Estado |
|---------------|--------|
| Se identificó el objetivo de la integración. | ☐ |
| Se definió el alcance del proyecto. | ☐ |
| Se identificaron las plataformas involucradas. | ☐ |
| Se definieron las responsabilidades de cada plataforma. | ☐ |
| Se identificó el System of Record de cada entidad. | ☐ |

---

## Arquitectura

| Verificación | Estado |
|---------------|--------|
| Se documentó la arquitectura general. | ☐ |
| Se elaboró el System Context. | ☐ |
| Se documentó el Container Diagram. | ☐ |
| Se documentó el Component Diagram. | ☐ |
| Se registraron las decisiones arquitectónicas principales. | ☐ |

---

## Flujos

| Verificación | Estado |
|---------------|--------|
| Se documentaron los flujos principales. | ☐ |
| Se identificó el origen de cada evento. | ☐ |
| Se identificó el destino de cada proceso. | ☐ |
| Se documentó el Information Flow. | ☐ |

---

# 2. Functional Analysis

## Actores

| Verificación | Estado |
|---------------|--------|
| Se identificaron todos los actores. | ☐ |
| Se definieron sus responsabilidades. | ☐ |

---

## Casos de Uso

| Verificación | Estado |
|---------------|--------|
| Todos los procesos principales poseen un caso de uso. | ☐ |
| Cada caso de uso posee objetivo, disparador y resultado esperado. | ☐ |

---

## Eventos

| Verificación | Estado |
|---------------|--------|
| Se identificaron los Domain Events. | ☐ |
| Se documentó el origen de cada evento. | ☐ |
| Se documentó el procesamiento esperado. | ☐ |

---

## Reglas

| Verificación | Estado |
|---------------|--------|
| Se documentaron las reglas de negocio. | ☐ |
| Se identificaron las dependencias funcionales. | ☐ |
| Se documentaron las restricciones funcionales. | ☐ |

---

# 3. Technical Analysis

## APIs

| Verificación | Estado |
|---------------|--------|
| Se analizaron las APIs disponibles. | ☐ |
| Se identificaron las capacidades relevantes. | ☐ |

---

## Seguridad

| Verificación | Estado |
|---------------|--------|
| Se documentaron los mecanismos de autenticación. | ☐ |
| Se identificaron las credenciales necesarias. | ☐ |

---

## Comunicación

| Verificación | Estado |
|---------------|--------|
| Se documentaron los Webhooks disponibles. | ☐ |
| Se documentaron los Rate Limits. | ☐ |

---

## Modelo de Datos

| Verificación | Estado |
|---------------|--------|
| Se identificaron los API Objects. | ☐ |
| Se documentaron los API Endpoints. | ☐ |
| Se identificaron los Data Mapping Requirements. | ☐ |

---

## Arquitectura Técnica

| Verificación | Estado |
|---------------|--------|
| Se documentaron las restricciones técnicas. | ☐ |
| Se identificaron los riesgos técnicos. | ☐ |

---

# 4. Validación General

## Consistencia

| Verificación | Estado |
|---------------|--------|
| No existen contradicciones entre documentos. | ☐ |
| Las responsabilidades están claramente definidas. | ☐ |
| El alcance es consistente en toda la documentación. | ☐ |
| Los procesos funcionales están alineados con la arquitectura. | ☐ |

---

## Trazabilidad

| Verificación | Estado |
|---------------|--------|
| Cada proceso funcional posee soporte técnico identificado. | ☐ |
| Cada decisión arquitectónica posee fundamento. | ☐ |
| Cada riesgo posee estrategia de mitigación. | ☐ |

---

## Preparación para el Diseño

| Verificación | Estado |
|---------------|--------|
| No existen incógnitas críticas. | ☐ |
| La información necesaria para diseñar la solución está disponible. | ☐ |
| Las plataformas fueron analizadas suficientemente. | ☐ |
| La arquitectura conceptual está definida. | ☐ |

---

# Resultado

## Discovery Completa

☐ Sí

☐ No

---

## Observaciones

Registrar aquí cualquier pendiente identificado antes de comenzar la fase de **Technical Design**.

---

# Criterio de Aprobación

La fase de Discovery podrá considerarse formalmente finalizada cuando:

- Todas las verificaciones aplicables se encuentren completadas.
- No existan incógnitas técnicas o funcionales que impidan avanzar.
- La documentación sea consistente entre sí.
- El equipo considere que dispone de suficiente información para diseñar la solución.

---

# Próximo Paso

Una vez aprobada esta lista de verificación, el proyecto queda habilitado para iniciar la **Fase 2 – Technical Design**, donde se definirán los aspectos específicos de implementación de la integración.

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **Discovery Closure Report** | Resume y formaliza el cierre de la fase de Discovery. |
| **Design Readiness Assessment** | Evalúa la preparación del proyecto para comenzar el diseño técnico. |
| **Technical Summary** | Consolida el análisis técnico realizado. |
| **Functional Summary** | Consolida el análisis funcional realizado. |
| **Discovery Report** | Resume los hallazgos del Domain Discovery. |