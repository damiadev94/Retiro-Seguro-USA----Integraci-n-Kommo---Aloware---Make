# 03. Data Ownership Model

## Objetivo

Definir el modelo de propiedad de datos de la integración entre Kommo CRM y Aloware.

Este documento establece:

- El propietario (Source of Truth) de cada entidad.
- El ciclo de vida de las entidades sincronizadas.
- Las reglas de propiedad de los datos.
- Las responsabilidades de cada plataforma durante la sincronización.

Su objetivo es garantizar consistencia, evitar conflictos de actualización y eliminar duplicación de información.

---

# Modelo de Propiedad

La arquitectura adopta el principio de **Single Source of Truth (SSOT)**.

Cada entidad posee un único sistema propietario responsable de su creación, actualización y persistencia.

Las demás plataformas únicamente mantienen copias operativas cuando son necesarias para cumplir una función específica.

---

# Catálogo de Entidades

## Business Entities

| Categoría | Entidad | Source of Truth |
| --- | --- | --- |
| CRM | Lead | Kommo |
| CRM | Contact | Kommo |
| CRM | Company | Kommo |
| CRM | Pipeline | Kommo |
| CRM | Stage *(Status en API)* | Kommo |
| CRM | Responsible User | Kommo |
| CRM | Note | Kommo |
| CRM | Tag | Kommo |
| CRM | Custom Field | Kommo |
| Comunicaciones | Agent *(User en API)* | Aloware |
| Comunicaciones | Dialing Sequence | Aloware |
| Comunicaciones | Line | Aloware |
| Comunicaciones | Call | Aloware |
| Comunicaciones | SMS | Aloware |
| Comunicaciones | Recording | Aloware |
| Comunicaciones | Voicemail | Aloware |
| Comunicaciones | AI Summary | Aloware |

---

## Integration Entities

Estas entidades existen únicamente para soportar la sincronización.

| Entidad | Administrador |
| --- | --- |
| User ↔ Agent Mapping | Plataforma de Integración |
| Stage ↔ Dialing Sequence Mapping | Plataforma de Integración |
| Lead ↔ Contact Mapping | Plataforma de Integración |
| Sync Log | Plataforma de Integración |
| Error Log | Plataforma de Integración |
| Retry Queue | Plataforma de Integración |

---

# Source of Truth Matrix

| Entidad | Source of Truth | Copia Operativa | Sincronizada por |
| --- | --- | --- | --- |
| Lead | Kommo | Aloware | Plataforma de Integración |
| Contact | Kommo | Aloware | Plataforma de Integración |
| Company | Kommo | — | — |
| Pipeline | Kommo | — | — |
| Stage | Kommo | — | — |
| Responsible User | Kommo | — | Plataforma de Integración |
| Note | Kommo | — | Plataforma de Integración |
| Tag | Kommo | — | Plataforma de Integración |
| Custom Field | Kommo | — | Plataforma de Integración |
| Agent | Aloware | — | Plataforma de Integración |
| Dialing Sequence | Aloware | — | Plataforma de Integración |
| Line | Aloware | — | Plataforma de Integración |
| Call | Aloware | Kommo (Note) | Plataforma de Integración |
| SMS | Aloware | Kommo (Note) | Plataforma de Integración |
| Recording | Aloware | Kommo (URL) | Plataforma de Integración |
| Voicemail | Aloware | Kommo (Note) | Plataforma de Integración |
| AI Summary | Aloware | Kommo (Note) | Plataforma de Integración |

---

# Lifecycle

| Entidad | Se crea en | Se modifica en | Se consume en |
| --- | --- | --- | --- |
| Lead | Kommo | Kommo | Kommo, Plataforma de Integración, Aloware |
| Contact | Kommo | Kommo | Kommo, Plataforma de Integración, Aloware |
| Note | Kommo | Kommo | Kommo |
| Agent | Aloware | Aloware | Aloware, Plataforma de Integración |
| Dialing Sequence | Aloware | Aloware | Aloware, Plataforma de Integración |
| Call | Aloware | Aloware | Aloware, Plataforma de Integración, Kommo |
| SMS | Aloware | Aloware | Aloware, Plataforma de Integración, Kommo |
| Recording | Aloware | Aloware | Aloware, Plataforma de Integración, Kommo |
| Voicemail | Aloware | Aloware | Aloware, Plataforma de Integración, Kommo |
| AI Summary | Aloware | Aloware | Aloware, Plataforma de Integración, Kommo |

---

# Ownership Rules

### OR-001 — Propietario único

Cada entidad posee un único **Source of Truth**.

---

### OR-002 — Copias operativas

Las copias operativas existen únicamente para soportar la operación de la integración.

Nunca reemplazan al sistema propietario.

---

### OR-003 — Modificación de datos

Las entidades únicamente pueden modificarse en su sistema propietario.

---

### OR-004 — Rol de la Plataforma de Integración

La Plataforma de Integración no es propietaria de datos de negocio.

Su responsabilidad consiste en:

- Orquestar procesos.
- Aplicar reglas de negocio.
- Transformar datos.
- Sincronizar plataformas.
- Registrar información técnica.

---

### OR-005 — Mapeos

Los mapeos forman parte de la integración y son administrados exclusivamente por la Plataforma de Integración.

Incluyen:

- User ↔ Agent
- Stage ↔ Dialing Sequence
- Lead ↔ Contact

---

### OR-006 — Dirección de sincronización

La sincronización siempre sigue la dirección definida por el Source of Truth.

Ejemplos:

- Lead → Kommo → Aloware
- Call → Aloware → Kommo
- SMS → Aloware → Kommo
- AI Summary → Aloware → Kommo

---

### OR-007 — Persistencia

La Plataforma de Integración únicamente puede almacenar información técnica necesaria para la operación.

Ejemplos:

- Logs.
- Configuración.
- Mapeos.
- Reintentos.

Nunca almacena información permanente del negocio.

---

### OR-008 — Trazabilidad

Toda entidad sincronizada debe poder relacionarse mediante identificadores únicos entre ambas plataformas.

---

### OR-009 — Excepción para comunicaciones entrantes

Si una llamada o SMS proviene de un número no registrado, la integración podrá crear automáticamente el Contact y/o Lead correspondiente en Kommo.

Una vez creado, Kommo pasa inmediatamente a ser el Source of Truth de dicha entidad.

---

# Principios

- Un único Source of Truth por entidad.
- Separación entre datos de negocio y datos de integración.
- Bajo acoplamiento entre plataformas.
- Persistencia distribuida.
- Integración dirigida por eventos.
- Trazabilidad completa de las sincronizaciones.

---

# Referencias

- Platform Responsibilities
- Responsibilities Validation
- Architecture Overview
- System Context
- Container Diagram
- Architectural Decisions

---

## Estado

**Versión:** 1.0

**Estado:** Aprobado

**Fase:** 1.1 – Comprensión del Dominio