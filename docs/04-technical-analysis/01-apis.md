# APIs

## Objetivo

Este documento proporciona una visión general de las APIs utilizadas por la integración entre **Kommo CRM** y **Aloware**, describiendo las capacidades que cada plataforma expone y el rol que desempeñan dentro de la solución.

No documenta endpoints específicos, autenticación ni payloads. Esos aspectos se desarrollan en documentos independientes durante la fase de **Technical Analysis**.

---

# Plataformas Analizadas

| Plataforma | API | Rol en la Integración |
|------------|-----|-----------------------|
| **Kommo CRM** | REST API | Gestión de información comercial. |
| **Aloware** | REST API | Gestión de telefonía y comunicaciones. |
| **Make** | HTTP Modules / Webhooks | Orquestación y comunicación entre APIs. |

---

# Arquitectura de Comunicación

```text
                 REST API
┌─────────────┐ ◄──────────────► ┌─────────────┐
│   Kommo     │                  │    Make     │
└─────────────┘                  └─────────────┘
                                        ▲
                                        │
                                        │ REST API
                                        ▼
                               ┌─────────────┐
                               │  Aloware   │
                               └─────────────┘
```

Las plataformas no se comunican directamente entre sí.

Toda interacción es coordinada por **Make**, que actúa como capa de integración.

---

# Kommo API

## Propósito

La API de Kommo permite acceder y administrar la información comercial del CRM.

Dentro de esta integración será utilizada para consultar y actualizar la información necesaria para sincronizar el proceso comercial con Aloware.

## Capacidades utilizadas

- Gestión de Leads.
- Gestión de Contactos.
- Gestión de Usuarios.
- Gestión de Pipelines.
- Gestión de Etapas.
- Registro de Notas y Actividades.
- Recepción de Webhooks.

## Rol dentro de la integración

Kommo actúa como el sistema de referencia (**System of Record**) para toda la información comercial.

La integración consume eventos originados en Kommo y registra en él la actividad proveniente de Aloware.

---

# Aloware API

## Propósito

La API de Aloware permite gestionar la operación de telefonía y acceder a los eventos generados durante la comunicación con los clientes.

Dentro de esta integración será utilizada para automatizar campañas de llamadas y recuperar la actividad realizada por los agentes.

## Capacidades utilizadas

- Gestión de Contactos.
- Gestión de Agentes.
- Gestión de Listas de Marcación.
- Eventos de Llamadas.
- Eventos de SMS.
- Grabaciones.
- Notas.
- Resúmenes generados por IA.
- Webhooks.

## Rol dentro de la integración

Aloware actúa como el sistema responsable de todas las comunicaciones realizadas con los clientes.

---

# Make

## Propósito

Make funciona como plataforma de integración y automatización entre Kommo y Aloware.

No constituye un sistema de negocio ni una fuente permanente de información.

## Capacidades utilizadas

- Recepción de Webhooks.
- Consumo de APIs REST.
- Transformación de datos.
- Validaciones.
- Enrutamiento de flujos.
- Manejo de errores.
- Registro de logs.

## Rol dentro de la integración

Make coordina todos los procesos de sincronización entre ambas plataformas.

---

# Modelo General de Comunicación

## Kommo → Aloware

Kommo genera eventos relacionados con el proceso comercial.

Make consume dichos eventos, transforma la información necesaria y ejecuta las operaciones correspondientes mediante la API de Aloware.

---

## Aloware → Kommo

Aloware genera eventos relacionados con llamadas, mensajes y demás actividades de comunicación.

Make procesa dichos eventos y registra la información correspondiente mediante la API de Kommo.

---

# Tipo de Integración

| Característica | Valor |
|----------------|-------|
| Arquitectura | Event-Driven Integration |
| Comunicación | REST APIs |
| Eventos | Webhooks |
| Formato de datos | JSON |
| Orquestación | Make |
| Sincronización | Bidireccional |

---

# Responsabilidades

| Plataforma | Responsabilidad |
|------------|-----------------|
| Kommo | Exponer información comercial y recibir actividades. |
| Aloware | Exponer información de comunicaciones y ejecutar acciones telefónicas. |
| Make | Orquestar, transformar y sincronizar la información entre plataformas. |

---

# Alcance

Durante esta integración las APIs se utilizarán para:

- Consultar información.
- Crear registros.
- Actualizar registros.
- Registrar actividades.
- Recibir eventos.
- Sincronizar información entre plataformas.

No forman parte del alcance:

- Administración completa de las plataformas.
- Configuración interna mediante API.
- Funcionalidades no relacionadas con el proceso de integración.

---

# Consideraciones

- Cada plataforma mantiene la propiedad de sus propios datos.
- Make consume únicamente las capacidades necesarias para soportar los flujos definidos durante el análisis funcional.
- Las operaciones disponibles dependerán de los permisos otorgados a las credenciales utilizadas.
- La implementación deberá respetar las limitaciones técnicas documentadas en fases posteriores.

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **Authentication** | Describe los mecanismos de autenticación utilizados por cada API. |
| **Webhooks** | Documenta los eventos disponibles y su recepción. |
| **Rate Limits** | Describe las restricciones de consumo de las APIs. |
| **API Objects** | Define las entidades expuestas por cada plataforma. |
| **API Endpoints** | Documenta los endpoints utilizados por la integración. |
| **Technical Constraints** | Describe las limitaciones técnicas identificadas. |
| **Technical Summary** | Resume los resultados del análisis técnico. |