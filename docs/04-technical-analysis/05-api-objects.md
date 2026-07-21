# API Objects

## Objetivo

Este documento identifica las principales entidades (**API Objects**) expuestas por las APIs de **Kommo CRM** y **Aloware** que participan en la integración.

Su propósito es proporcionar una visión conceptual del modelo de datos disponible en ambas plataformas antes de documentar los endpoints específicos y el mapeo de campos.

No describe la estructura completa de cada objeto ni sus atributos detallados, ya que esos aspectos se desarrollarán en documentos posteriores.

---

# ¿Qué es un API Object?

Un API Object representa una entidad del modelo de datos que puede consultarse, crearse, actualizarse o relacionarse mediante una API.

Ejemplos:

- Lead
- Contact
- User
- Agent
- Call
- SMS

Cada objeto representa un concepto propio del dominio de una plataforma.

---

# Clasificación

| Plataforma | Objetos |
|------------|----------|
| **Kommo CRM** | Entidades comerciales. |
| **Aloware** | Entidades de comunicación. |

---

# Kommo API Objects

## Lead

### Propósito

Representa una oportunidad comercial dentro del proceso de ventas.

### Utilización en la integración

- Detectar cambios de etapa.
- Obtener información comercial.
- Registrar actividades.
- Asociar comunicaciones.

---

## Contact

### Propósito

Representa una persona o empresa asociada a uno o más Leads.

### Utilización

- Obtener información del cliente.
- Sincronizar datos con Aloware.
- Resolver comunicaciones mediante el número telefónico.

---

## User

### Propósito

Representa un usuario del CRM.

### Utilización

- Identificar el responsable del Lead.
- Resolver la correspondencia con un agente de Aloware.

---

## Pipeline

### Propósito

Representa un proceso comercial.

### Utilización

- Identificar el contexto del Lead.
- Determinar reglas de sincronización.

---

## Stage

### Propósito

Representa una etapa dentro de un Pipeline.

### Utilización

- Disparar procesos de sincronización.
- Determinar la lista de marcación correspondiente.

---

## Note / Activity

### Propósito

Representa información registrada sobre un Lead.

### Utilización

- Registrar llamadas.
- Registrar SMS.
- Registrar notas.
- Registrar grabaciones.
- Registrar resúmenes generados por IA.

---

# Aloware API Objects

## Contact

### Propósito

Representa un cliente dentro de la plataforma de telefonía.

### Utilización

- Gestionar llamadas.
- Gestionar SMS.
- Asociar comunicaciones.

---

## Agent

### Propósito

Representa un operador de Aloware.

### Utilización

- Asignar responsables.
- Registrar actividades realizadas por el agente.

---

## Dialing List

### Propósito

Representa una lista utilizada por el Power Dialer.

### Utilización

- Organizar contactos para campañas de llamadas.
- Asociar etapas comerciales con listas operativas.

---

## Call

### Propósito

Representa una llamada realizada o recibida.

### Utilización

- Registrar la actividad en Kommo.
- Asociar grabaciones.
- Registrar duración y resultado.

---

## SMS

### Propósito

Representa un mensaje de texto.

### Utilización

- Registrar comunicaciones dentro del historial comercial.

---

## Recording

### Propósito

Representa una grabación asociada a una llamada.

### Utilización

- Incorporar la referencia de la grabación al Lead correspondiente.

---

## AI Summary

### Propósito

Representa el resumen generado automáticamente por AloAI.

### Utilización

- Registrar el resultado de la conversación dentro del CRM.

---

# Relaciones Conceptuales

```text
Kommo

Lead
 │
 ├── Contact
 │
 ├── User
 │
 ├── Pipeline
 │
 ├── Stage
 │
 └── Activity


Aloware

Contact
 │
 ├── Agent
 │
 ├── Dialing List
 │
 ├── Call
 │
 ├── SMS
 │
 ├── Recording
 │
 └── AI Summary
```

---

# Objetos Compartidos Conceptualmente

Aunque cada plataforma posee su propio modelo de datos, existen entidades equivalentes utilizadas durante la sincronización.

| Kommo | Aloware | Propósito |
|--------|----------|-----------|
| Lead | Contact | Representación del cliente durante el proceso comercial. |
| Contact | Contact | Información personal del cliente. |
| User | Agent | Responsable de la gestión del cliente. |
| Stage | Dialing List | Estado comercial y operación telefónica. |
| Note / Activity | Call / SMS / Recording / AI Summary | Historial de interacción con el cliente. |

Estas relaciones conceptuales serán desarrolladas en el documento **Field Mapping** durante la fase de **Technical Design**.

---

# Consideraciones

- Cada plataforma mantiene su propio modelo de datos.
- No todos los objetos poseen un equivalente directo en la otra plataforma.
- La integración utiliza únicamente los objetos necesarios para soportar los flujos definidos durante el análisis funcional.
- Las relaciones entre objetos pueden requerir transformaciones durante la sincronización.

---

# Fuera del Alcance

Este documento no incluye:

- Campos de cada objeto.
- Payloads.
- Esquemas JSON.
- Endpoints.
- Relaciones técnicas específicas.

Estos aspectos se documentarán en:

- API Endpoints
- Data Mapping Requirements
- Field Mapping

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **APIs** | Describe las capacidades generales de las APIs. |
| **API Endpoints** | Documenta las operaciones disponibles sobre estos objetos. |
| **Data Mapping Requirements** | Identifica la información necesaria de cada objeto para la integración. |
| **Field Mapping** | Define la correspondencia entre entidades y campos de ambas plataformas. |
| **Business Rules** | Establece las reglas que gobiernan el uso de estos objetos durante la sincronización. |