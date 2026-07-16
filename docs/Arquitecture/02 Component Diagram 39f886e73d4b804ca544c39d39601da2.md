# 02. Component Diagram

---

## Objetivo

Describir la arquitectura interna de la **Plataforma de Integración**, identificando los componentes funcionales que colaboran para sincronizar Kommo CRM y Aloware.

Este documento corresponde al **Nivel 3 del modelo C4 (Component Diagram)**.

No representa módulos específicos de Make, sino una arquitectura lógica independiente de la tecnología utilizada.

---

# Arquitectura de Componentes

La Plataforma de Integración se organiza en componentes especializados, cada uno con una responsabilidad única.

```
                    Kommo CRM
                         │
                         ▼
                 Event Receiver
                         │
                         ▼
              Business Rules Engine
                         │
      ┌──────────┬──────────┬──────────┐
      ▼          ▼          ▼          ▼
 Validation   Mapping   Transformation Error Handler
      │          │          │          │
      └──────────┴──────┬───┴──────────┘
                         ▼
               Communication Layer
                         │
                         ▼
                     Aloware
                         │
                         ▼
                  Logging Service
```

---

# Componentes

## Event Receiver

### Responsabilidad

Recibir los eventos provenientes de Kommo y Aloware e iniciar el flujo de integración correspondiente.

---

## Business Rules Engine

### Responsabilidad

Aplicar las reglas de negocio y decidir las acciones que debe ejecutar la integración.

Ejemplos:

- ¿Debe sincronizarse el Lead?
- ¿A qué secuencia debe enviarse?
- ¿Debe registrarse una nota?

---

## Validation Service

### Responsabilidad

Verificar que la información recibida sea válida antes de continuar el procesamiento.

Incluye:

- Campos obligatorios.
- Consistencia.
- Prevención de duplicados.

---

## Mapping Service

### Responsabilidad

Resolver las equivalencias entre ambas plataformas.

Incluye:

- Responsible User ↔ Agent
- Stage ↔ Dialing Sequence
- Lead ↔ Contact

---

## Transformation Engine

### Responsabilidad

Adaptar los datos entre los modelos de Kommo y Aloware.

Ejemplos:

- Conversión de estructuras.
- Normalización de datos.
- Adaptación de formatos.

---

## Communication Layer

### Responsabilidad

Gestionar toda la comunicación con las plataformas externas.

Funciones:

- Envío de solicitudes.
- Recepción de respuestas.
- Aislamiento de la lógica de comunicación.

---

## Error Handler

### Responsabilidad

Gestionar errores durante la sincronización.

Funciones:

- Clasificación de errores.
- Reintentos.
- Recuperación del flujo.
- Registro de incidencias.

---

## Logging Service

### Responsabilidad

Registrar toda la actividad técnica de la integración.

Incluye:

- Logs de sincronización.
- Auditoría.
- Diagnóstico.
- Trazabilidad.

---

# Flujo de Componentes

```
Evento

↓

Event Receiver

↓

Business Rules Engine

↓

Validation Service

↓

Mapping Service

↓

Transformation Engine

↓

Communication Layer

↓

Sistema Destino

↓

Logging Service
```

En caso de error:

```
Error

↓

Error Handler

↓

Logging Service

↓

Retry (si corresponde)
```

---

# Relaciones

| Componente | Utiliza |
| --- | --- |
| Event Receiver | Business Rules Engine |
| Business Rules Engine | Validation Service |
| Business Rules Engine | Mapping Service |
| Business Rules Engine | Transformation Engine |
| Business Rules Engine | Error Handler |
| Transformation Engine | Communication Layer |
| Communication Layer | Logging Service |
| Error Handler | Logging Service |

---

# Principios

- Cada componente posee una responsabilidad única.
- La lógica de negocio está separada de la comunicación con sistemas externos.
- Los componentes son reutilizables por distintos flujos de integración.
- La arquitectura permanece independiente de Make.
- Nuevos escenarios pueden incorporarse reutilizando los mismos componentes.

---

# Referencias

- Container Diagram
- Data Ownership Model
- Architectural Decisions
- Information Flow

---

## Estado

**Versión:** 1.0

**Estado:** Aprobado

**Fase:** 1.1 – Comprensión del Dominio