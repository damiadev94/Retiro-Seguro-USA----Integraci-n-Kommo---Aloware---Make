# Data Mapping Requirements

## Objetivo

Este documento identifica la información que la integración entre **Kommo CRM** y **Aloware** necesita intercambiar para soportar los procesos definidos durante el análisis funcional.

Su propósito es establecer **qué datos son necesarios**, **de dónde provienen**, **para qué se utilizan** y **qué requisitos deben cumplir**.

No define todavía la correspondencia exacta entre campos de ambas plataformas. Ese diseño se desarrollará posteriormente en el documento **Field Mapping** durante la fase de **Technical Design**.

---

# Alcance

Los requisitos documentados corresponden a los siguientes procesos:

- Sincronización de Leads.
- Sincronización de Contactos.
- Asignación de Agentes.
- Asignación de Listas de Marcación.
- Registro de Llamadas.
- Registro de SMS.
- Registro de Notas.
- Registro de Grabaciones.
- Registro de AI Summary.

---

# Clasificación de la Información

| Categoría | Descripción |
|-----------|-------------|
| Identification Data | Permite identificar entidades entre plataformas. |
| Customer Data | Información del cliente. |
| Commercial Data | Información del proceso comercial. |
| Assignment Data | Información necesaria para asignar responsables. |
| Communication Data | Información generada durante las comunicaciones. |
| Metadata | Información técnica utilizada por la integración. |

---

# Identification Data

Información necesaria para relacionar registros entre ambas plataformas.

## Requerimientos

- Identificador del Lead.
- Identificador del Contacto.
- Identificador del Usuario.
- Identificador del Agente.
- Identificador de la Lista.
- Identificadores de llamadas y mensajes cuando existan.

### Utilización

- Resolver correspondencias.
- Evitar duplicados.
- Asociar actividades al registro correcto.

---

# Customer Data

Información del cliente utilizada durante la sincronización.

## Requerimientos

- Nombre.
- Apellido.
- Empresa (cuando corresponda).
- Número telefónico.
- Correo electrónico (cuando exista).

### Utilización

- Crear o actualizar contactos.
- Identificar comunicaciones.
- Resolver coincidencias entre plataformas.

---

# Commercial Data

Información relacionada con el proceso de ventas.

## Requerimientos

- Pipeline.
- Etapa.
- Estado del Lead.
- Responsable.
- Información comercial relevante.

### Utilización

- Determinar si un Lead debe sincronizarse.
- Resolver la lista de marcación correspondiente.
- Mantener actualizado el contexto comercial.

---

# Assignment Data

Información utilizada para asignar correctamente el trabajo entre plataformas.

## Requerimientos

- Usuario responsable en Kommo.
- Agente correspondiente en Aloware.
- Lista de marcación asignada.

### Utilización

- Dirigir correctamente la gestión comercial.
- Automatizar la asignación de llamadas.

---

# Communication Data

Información generada por Aloware durante la interacción con el cliente.

## Requerimientos

- Tipo de comunicación.
- Fecha y hora.
- Duración de la llamada.
- Resultado de la llamada.
- Contenido del SMS.
- Nota del agente.
- URL de la grabación.
- Resumen generado por IA.

### Utilización

- Registrar el historial comercial.
- Facilitar el seguimiento del Lead.
- Conservar evidencia de las interacciones.

---

# Metadata

Información utilizada exclusivamente por la integración.

## Requerimientos

- Identificador del evento.
- Fecha y hora del evento.
- Sistema de origen.
- Estado de la sincronización.
- Resultado del procesamiento.

### Utilización

- Auditoría.
- Logging.
- Trazabilidad.
- Recuperación ante errores.

---

# Requisitos Generales

Toda la información intercambiada deberá cumplir las siguientes condiciones.

## Integridad

Los datos deben ser completos y consistentes antes de iniciar una sincronización.

---

## Unicidad

Cada entidad debe poder identificarse de forma unívoca para evitar duplicaciones.

---

## Consistencia

Las transformaciones realizadas durante la integración no deben modificar el significado funcional de la información.

---

## Trazabilidad

Toda la información procesada debe poder asociarse al evento que originó la sincronización.

---

# Matriz de Requisitos

| Categoría | Kommo | Aloware | Integración |
|-----------|--------|----------|-------------|
| Identificación | ✓ | ✓ | ✓ |
| Cliente | ✓ | ✓ | ✓ |
| Comercial | ✓ | — | ✓ |
| Asignación | ✓ | ✓ | ✓ |
| Comunicación | — | ✓ | ✓ |
| Metadata | — | — | ✓ |

---

# Consideraciones

- No toda la información disponible en las APIs será utilizada por la integración.
- Cada flujo funcional utilizará únicamente los datos necesarios para cumplir su objetivo.
- La ausencia de determinada información podrá impedir la ejecución de un proceso de sincronización.
- La transformación y correspondencia entre campos se documentará durante el diseño técnico.

---

# Fuera del Alcance

Este documento no define:

- Correspondencias entre campos.
- Transformaciones específicas.
- Valores por defecto.
- Reglas de conversión.
- Validaciones de implementación.

Estos aspectos se documentarán en:

- **Field Mapping**
- **Synchronization Model**
- **Stage Mapping**
- **Agent Mapping**

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **API Objects** | Identifica las entidades que contienen esta información. |
| **API Endpoints** | Describe las operaciones utilizadas para obtener o actualizar los datos. |
| **Business Rules** | Define las reglas que condicionan el intercambio de información. |
| **Functional Dependencies** | Identifica la información necesaria para ejecutar cada caso de uso. |
| **Field Mapping** | Definirá la correspondencia exacta entre los campos de Kommo y Aloware. |