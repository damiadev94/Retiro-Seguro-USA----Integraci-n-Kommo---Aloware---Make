# API Endpoints

## Objetivo

Este documento identifica los principales **API Endpoints** que la integración entre **Kommo CRM** y **Aloware** utilizará para implementar los flujos definidos durante el análisis funcional.

Su propósito es documentar **qué operaciones necesita realizar la integración**, independientemente de la implementación específica en Make.

No pretende ser una referencia completa de las APIs, sino un inventario de los endpoints relevantes para este proyecto.

---

# Alcance

Los endpoints documentados corresponden únicamente a las operaciones necesarias para soportar los siguientes procesos:

- Sincronización de Leads.
- Sincronización de Contactos.
- Asignación de agentes.
- Asignación de listas.
- Registro de llamadas.
- Registro de SMS.
- Registro de notas.
- Registro de grabaciones.
- Registro de resúmenes generados por IA.

---

# Clasificación

| Plataforma | Operaciones |
|------------|-------------|
| **Kommo CRM** | Consulta y actualización de información comercial. |
| **Aloware** | Gestión de contactos y comunicaciones. |

---

# Kommo API Endpoints

## Leads

| Operación | Método | Propósito |
|------------|--------|-----------|
| Obtener Lead | GET | Recuperar la información de un Lead. |
| Actualizar Lead | PATCH | Actualizar información del Lead cuando corresponda. |
| Buscar Lead | GET | Localizar un Lead para asociar una comunicación. |

---

## Contacts

| Operación | Método | Propósito |
|------------|--------|-----------|
| Obtener Contacto | GET | Recuperar información del contacto asociado al Lead. |
| Buscar Contacto | GET | Identificar un contacto mediante criterios de búsqueda. |

---

## Users

| Operación | Método | Propósito |
|------------|--------|-----------|
| Obtener Usuario | GET | Identificar el responsable del Lead. |

---

## Pipelines

| Operación | Método | Propósito |
|------------|--------|-----------|
| Obtener Pipeline | GET | Recuperar la estructura del proceso comercial. |

---

## Stages

| Operación | Método | Propósito |
|------------|--------|-----------|
| Obtener Etapas | GET | Resolver el estado actual del Lead. |

---

## Notes / Activities

| Operación | Método | Propósito |
|------------|--------|-----------|
| Crear Nota | POST | Registrar actividades provenientes de Aloware. |
| Obtener Notas | GET | Consultar el historial cuando sea necesario. |

---

# Aloware API Endpoints

## Contacts

| Operación | Método | Propósito |
|------------|--------|-----------|
| Buscar Contacto | GET | Verificar si el contacto ya existe. |
| Crear Contacto | POST | Crear un nuevo contacto. |
| Actualizar Contacto | PUT / PATCH | Sincronizar información del contacto. |

---

## Agents

| Operación | Método | Propósito |
|------------|--------|-----------|
| Obtener Agentes | GET | Resolver la correspondencia entre usuarios y agentes. |

---

## Dialing Lists

| Operación | Método | Propósito |
|------------|--------|-----------|
| Obtener Listas | GET | Consultar listas disponibles. |
| Asignar Contacto a Lista | POST | Incorporar el contacto a la lista correspondiente. |

---

## Calls

| Operación | Método | Propósito |
|------------|--------|-----------|
| Consultar Llamada | GET | Obtener información adicional sobre una llamada. |

---

## SMS

| Operación | Método | Propósito |
|------------|--------|-----------|
| Consultar SMS | GET | Recuperar información de un mensaje cuando sea necesario. |

---

## Recordings

| Operación | Método | Propósito |
|------------|--------|-----------|
| Obtener Grabación | GET | Recuperar la referencia de una grabación. |

---

## AI Summary

| Operación | Método | Propósito |
|------------|--------|-----------|
| Obtener Resumen | GET | Recuperar el resumen generado por IA. |

---

# Uso de los Endpoints

Los endpoints cumplen distintos roles dentro de la integración.

| Tipo de operación | Finalidad |
|-------------------|-----------|
| Consulta | Obtener información necesaria para ejecutar un flujo. |
| Creación | Incorporar nuevos registros en la plataforma destino. |
| Actualización | Mantener la información sincronizada. |
| Registro | Incorporar actividades generadas durante la comunicación. |

---

# Dependencias

La utilización de los endpoints depende de:

- Autenticación válida.
- Permisos suficientes.
- Disponibilidad de la API.
- Existencia de las entidades relacionadas.
- Cumplimiento de las reglas de negocio.

---

# Consideraciones

- Un único flujo funcional puede requerir múltiples llamadas a diferentes endpoints.
- Algunos Webhooks contienen únicamente identificadores, por lo que será necesario consultar la API para obtener información adicional.
- La integración debe minimizar la cantidad de solicitudes realizadas para optimizar el rendimiento y reducir el consumo de las APIs.
- La implementación deberá contemplar el manejo de errores y reintentos cuando una operación no pueda completarse correctamente.

---

# Fuera del Alcance

Este documento no incluye:

- URLs específicas.
- Parámetros de consulta.
- Payloads.
- Esquemas JSON.
- Ejemplos de Request/Response.
- Códigos de estado HTTP.

Estos detalles se documentarán durante la implementación y la configuración de los escenarios de Make.

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **APIs** | Describe las capacidades generales de las APIs. |
| **Authentication** | Define los mecanismos de autenticación necesarios para consumir estos endpoints. |
| **Webhooks** | Describe los eventos que originan el consumo de los endpoints. |
| **API Objects** | Define las entidades sobre las que operan estos endpoints. |
| **Data Mapping Requirements** | Identifica la información que debe obtenerse o enviarse mediante estos endpoints. |
| **Rate Limits** | Describe las restricciones que afectan el consumo de estos endpoints. |

---

## Recomendación de arquitectura

En una siguiente iteración, cuando ya dispongas de los accesos del cliente, convertiría este documento en un Endpoint Catalog mucho más útil para la implementación. En lugar de listar sólo las operaciones, cada endpoint tendría una ficha como esta:

|Campo | Valor |
|------|-------|
|Endpoint	| /api/v4/leads/{id}|
|Método	| GET |
|Objeto |	Lead |
|Flujo |	Kommo → Aloware |
|Escenario | Make	Scenario K→A |
| Requiere Auth |	Sí |
| Rate Limited |	Sí |
| Documentación oficial	| Enlace |
|Utilizado por |	UC-01, UC-02 |

De esta forma, el documento deja de ser únicamente descriptivo y se convierte en una referencia operativa durante el desarrollo y el mantenimiento de la integración.