# Actors

## Objetivo

Este documento identifica los actores que participan en la integración entre **Kommo CRM** y **Aloware**, describiendo sus responsabilidades y la forma en que interactúan con el sistema.

Los actores representan tanto usuarios como sistemas externos que intervienen en los procesos de negocio soportados por la integración.

---

# Clasificación de Actores

| Categoría | Descripción |
|-----------|-------------|
| **Human Actors** | Usuarios que interactúan con las plataformas. |
| **System Actors** | Sistemas que generan o consumen eventos. |
| **Integration Actor** | Plataforma responsable de la orquestación de la integración. |

---

# Human Actors

## CRM Administrator

### Descripción

Responsable de la configuración y administración de Kommo CRM.

### Responsabilidades

- Configurar pipelines y etapas.
- Administrar usuarios.
- Configurar credenciales de integración.
- Gestionar permisos.
- Supervisar el funcionamiento del CRM.

### Interacción con la integración

Indirecta.

La integración consume la configuración definida por el administrador, pero no interactúa directamente con él durante la operación normal.

---

## Sales Manager

### Descripción

Responsable del proceso comercial y de la gestión del equipo de ventas.

### Responsabilidades

- Definir el flujo comercial.
- Gestionar etapas del pipeline.
- Asignar responsables a los Leads.
- Supervisar el desempeño del equipo.

### Interacción con la integración

Indirecta.

Las decisiones del Sales Manager determinan cómo se comportan los flujos de automatización.

---

## Sales Agent

### Descripción

Usuario encargado de gestionar la relación con los clientes.

### Responsabilidades

- Gestionar Leads.
- Contactar prospectos.
- Realizar llamadas.
- Enviar y responder SMS.
- Registrar información comercial cuando corresponda.

### Interacción con la integración

Indirecta.

Su actividad dentro de Kommo y Aloware genera eventos que son procesados automáticamente por la integración.

---

# System Actors

## Kommo CRM

### Rol

Sistema de registro (**System of Record**) para la información comercial.

### Responsabilidades

- Gestionar Leads.
- Gestionar Contactos.
- Gestionar pipelines y etapas.
- Mantener la información comercial.
- Emitir eventos hacia la integración.

### Genera

- Cambios de etapa.
- Actualizaciones de Leads.
- Cambios en contactos.

---

## Aloware

### Rol

Plataforma de comunicación con clientes.

### Responsabilidades

- Gestionar llamadas.
- Gestionar SMS.
- Gestionar listas de marcación.
- Gestionar agentes.
- Generar eventos de comunicación.

### Genera

- Llamadas finalizadas.
- SMS enviados y recibidos.
- Notas.
- Grabaciones.
- Resúmenes generados por IA.

---

# Integration Actor

## Make

### Rol

Motor de integración y orquestación.

### Responsabilidades

- Recibir eventos.
- Validar información.
- Transformar datos.
- Ejecutar sincronizaciones.
- Registrar errores.
- Coordinar la comunicación entre plataformas.

### No es responsable de

- Almacenar información de negocio.
- Tomar decisiones comerciales.
- Modificar la lógica interna de Kommo o Aloware.

---

# Relaciones entre Actores

| Actor | Interactúa con | Propósito |
|--------|----------------|-----------|
| CRM Administrator | Kommo | Configuración del CRM. |
| Sales Manager | Kommo | Gestión del proceso comercial. |
| Sales Agent | Kommo / Aloware | Gestión de Leads y comunicaciones. |
| Kommo | Make | Envío de eventos comerciales. |
| Make | Kommo | Registro de actividades y sincronización. |
| Make | Aloware | Gestión de contactos, listas y agentes. |
| Aloware | Make | Envío de eventos de comunicación. |

---

# Responsabilidades Compartidas

| Proceso | Actor Principal | Actor de Soporte |
|----------|-----------------|------------------|
| Gestión comercial | Kommo | Sales Manager |
| Gestión de comunicaciones | Aloware | Sales Agent |
| Sincronización de información | Make | Kommo / Aloware |
| Configuración de la integración | CRM Administrator | Make |

---

# Consideraciones

- Los usuarios interactúan únicamente con Kommo y Aloware.
- Make opera de forma completamente automática y no requiere intervención durante el funcionamiento normal.
- Cada actor posee responsabilidades claramente definidas para evitar duplicidad de funciones.
- La integración no modifica los procesos comerciales establecidos por la organización; únicamente automatiza el intercambio de información entre plataformas.

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **Platform Responsibilities** | Define las responsabilidades de cada plataforma. |
| **Data Ownership Model** | Define la propiedad de los datos gestionados por cada actor. |
| **Information Flow** | Describe cómo circula la información entre los actores. |
| **Use Cases** | Describe las interacciones funcionales entre los actores y la integración. |