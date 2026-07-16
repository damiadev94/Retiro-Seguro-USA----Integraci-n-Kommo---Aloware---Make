# Domain Events

## Objetivo

Este documento identifica los eventos del dominio que impulsan el comportamiento de la integración entre **Kommo CRM** y **Aloware**.

Un **Domain Event** representa un hecho de negocio que ya ocurrió y que puede desencadenar uno o más procesos dentro de la integración.

La implementación técnica (Webhooks, APIs o escenarios de Make) se documentará en fases posteriores.

---

# ¿Qué es un Domain Event?

Un Domain Event representa un cambio significativo en el estado del negocio.

No describe cómo ocurre el evento, sino **qué ocurrió** y cuál es su impacto funcional.

Ejemplos:

- Un Lead cambió de etapa.
- Una llamada finalizó.
- Se recibió un SMS.
- Se generó un resumen mediante IA.

---

# Clasificación de Eventos

| Categoría | Descripción |
|-----------|-------------|
| **CRM Events** | Eventos originados en Kommo. |
| **Communication Events** | Eventos originados en Aloware. |
| **Integration Events** | Eventos generados durante el proceso de integración. |

---

# CRM Events

## DE-01 — Lead Stage Changed

### Origen

Kommo CRM

### Descripción

La etapa de un Lead cambia dentro del pipeline comercial.

### Dispara

- Sincronización del Lead.
- Actualización de lista de marcación.
- Validación de reglas de negocio.

---

## DE-02 — Lead Updated

### Origen

Kommo CRM

### Descripción

Se modifica información relevante de un Lead.

### Dispara

- Actualización del contacto en Aloware cuando corresponda.

---

## DE-03 — Contact Updated

### Origen

Kommo CRM

### Descripción

Se actualizan datos de un contacto asociado al Lead.

### Dispara

- Sincronización de información operativa.

---

# Communication Events

## DE-04 — Call Completed

### Origen

Aloware

### Descripción

Finaliza una llamada entre un agente y un cliente.

### Dispara

- Registro de actividad.
- Asociación de la llamada al Lead correspondiente.

---

## DE-05 — SMS Sent

### Origen

Aloware

### Descripción

Se envía un mensaje SMS al cliente.

### Dispara

- Registro del mensaje en Kommo.

---

## DE-06 — SMS Received

### Origen

Aloware

### Descripción

Se recibe un mensaje SMS del cliente.

### Dispara

- Registro de la conversación en Kommo.

---

## DE-07 — Note Created

### Origen

Aloware

### Descripción

Un agente registra una nota relacionada con una comunicación.

### Dispara

- Creación de una nota o actividad en Kommo.

---

## DE-08 — Recording Available

### Origen

Aloware

### Descripción

La grabación de una llamada queda disponible.

### Dispara

- Asociación del enlace de la grabación al Lead correspondiente.

---

## DE-09 — AI Summary Generated

### Origen

Aloware

### Descripción

AloAI genera automáticamente un resumen de la llamada.

### Dispara

- Registro del resumen como actividad o nota en Kommo.

---

# Integration Events

## DE-10 — Synchronization Started

### Origen

Make

### Descripción

Comienza el procesamiento de un evento recibido.

### Dispara

- Validaciones.
- Transformaciones.
- Ejecución del flujo correspondiente.

---

## DE-11 — Synchronization Completed

### Origen

Make

### Descripción

La sincronización finaliza correctamente.

### Dispara

- Registro de éxito.
- Finalización del proceso.

---

## DE-12 — Synchronization Failed

### Origen

Make

### Descripción

Se produce un error durante la sincronización.

### Dispara

- Registro del error.
- Aplicación de las políticas de recuperación definidas.

---

# Ciclo General de Eventos

```text
Evento de Negocio

        │

        ▼

Recepción por Make

        │

        ▼

Validaciones

        │

        ▼

Transformación

        │

        ▼

Sincronización

        │

        ▼

Registro del resultado
```

---

# Resumen de Eventos

| ID | Evento | Origen |
|----|--------|--------|
| DE-01 | Lead Stage Changed | Kommo |
| DE-02 | Lead Updated | Kommo |
| DE-03 | Contact Updated | Kommo |
| DE-04 | Call Completed | Aloware |
| DE-05 | SMS Sent | Aloware |
| DE-06 | SMS Received | Aloware |
| DE-07 | Note Created | Aloware |
| DE-08 | Recording Available | Aloware |
| DE-09 | AI Summary Generated | Aloware |
| DE-10 | Synchronization Started | Make |
| DE-11 | Synchronization Completed | Make |
| DE-12 | Synchronization Failed | Make |

---

# Consideraciones

- Los Domain Events representan hechos de negocio ya ocurridos.
- Un mismo evento puede desencadenar múltiples casos de uso.
- No todos los eventos requieren una sincronización entre plataformas.
- La lógica de negocio asociada a cada evento se define en **Business Rules**.
- La implementación técnica de estos eventos (Webhooks, APIs y escenarios de Make) se documentará durante el análisis técnico y el diseño de la integración.

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **Actors** | Define quién genera o consume cada evento. |
| **Use Cases** | Describe las funcionalidades activadas por los eventos. |
| **Business Rules** | Define las reglas que condicionan el procesamiento de cada evento. |
| **Information Flow** | Describe el recorrido de los eventos entre los sistemas. |
| **Technical Analysis** | Documentará cómo se implementa técnicamente la recepción y procesamiento de estos eventos. |