# Access Checklist — Kommo ↔ Aloware ↔ Make

> **Objetivo:** Recolectar toda la información necesaria durante el acceso temporal a las plataformas para completar el análisis técnico, el diseño de la integración y la implementación.

---

# 1. Aloware

## 1.1 API

### Credenciales

* [x] Obtener API Token
* [x] Confirmar permisos del token
* [ ] Verificar si existen restricciones de acceso

Registrar:

```text
API Token:B327972A
Usuario propietario:
Fecha de obtención:
```

---

### API Version

Confirmar:

* [x] Versión de la API
* [x] Base URL
* [x] Endpoint principal

Registrar:

```text
Version: v1
Base URL: https://app.aloware.io
Lead Endpoint: /api/v1/webhook/forms
```

Actualmente identificado:

```text
Version: v1

POST
/api/v1/webhook/forms

Base URL
https://app.aloware.io
```

---

### Autenticación

Confirmar:

* [x] Método de autenticación
* [ ] Dónde se envía el token
* [ ] Tipo de contenido

Registrar:

```text
Authentication:
API Token

Credential:
api_token B327972A

OAuth:
No

Bearer:
No

Content-Type:
application/json

Accept:
application/json
```

---

### Documentación

Guardar los enlaces oficiales.

Lead API

https://support.aloware.com/en/articles/9020058-aloware-lead-api-documentation

SMS API

https://support.aloware.com/en/articles/9020040-api-documentation-aloware-sms-api-integration

Two-Legged Call API

https://support.aloware.com/en/articles/9019991-api-documentation-aloware-two-legged-call-api-integration

Webhooks

https://support.aloware.com/en/articles/9020028-using-aloware-webhook-integration-for-real-time-automation

Users API

https://support.aloware.com/en/articles/9352647-api-documentation-users-api

MCP

https://support.aloware.com/en/articles/14707667-troubleshooting-aloware-mcp

Common Errors

https://support.aloware.com/en/articles/9020342-common-dialer-and-messaging-errors-in-aloware

---

## 1.2 Contactos

Realizar pruebas.

* [ ] Crear contacto
* [ ] Buscar contacto
* [ ] Editar contacto
* [ ] Eliminar contacto (si aplica)

Registrar:

```text
Contacto ID:

Campos disponibles:

Campo obligatorio:

Campos opcionales:

Teléfono:

Email:

Status:

Tags:

Observaciones:
```

---

## 1.3 Users

Obtener:

* [ ] User ID
* [ ] Nombre
* [ ] Email
* [ ] Rol
* [ ] Estado

---

## 1.4 Ring Groups

Registrar:

* [ ] Ring Group ID
* [ ] Nombre
* [ ] Usuarios asociados

---

## 1.5 Lists

Muy importante.

Confirmar:

* [ ] Cómo se crean
* [ ] Cómo agregar contactos
* [ ] Cómo quitar contactos
* [ ] Si poseen API
* [ ] Si poseen IDs

Registrar:

```text
List Name

List ID

Descripción
```

---

## 1.6 Sequences

Registrar:

* [ ] Sequence ID
* [ ] Nombre
* [ ] Objetivo

---

## 1.7 Tags

Registrar:

* [ ] Tag ID
* [ ] Nombre

---

## 1.8 Disposition Status

Registrar:

* [ ] ID
* [ ] Nombre

---

## 1.9 Lines

Registrar:

* [ ] Line ID
* [ ] Número
* [ ] Tipo

---

## 1.10 Campañas

Revisar:

* [ ] Campaigns
* [ ] AutoDialer
* [ ] Queues
* [ ] PowerDialer

Responder:

* ¿Cómo utilizan realmente las listas?
* ¿Qué dispara una llamada?
* ¿Qué ocurre cuando un contacto entra en una lista?

---

## 1.11 Webhooks

Registrar:

* [ ] Contact Created
* [ ] Contact Updated
* [ ] Call Started
* [ ] Call Ended
* [ ] SMS Sent
* [ ] SMS Received
* [ ] Otros eventos

Anotar:

```text
Evento

Payload

Endpoint

Observaciones
```

---

## 1.12 Call Logs

Buscar:

* [ ] Endpoint
* [ ] Payload
* [ ] Recording
* [ ] Disposition
* [ ] Duración
* [ ] Resultado

---

## 1.13 Custom Fields

Registrar:

```text
Nombre

ID

Tipo

Descripción
```

---

## 1.14 Configuración

Registrar:

* [ ] Timezone
* [ ] Caller IDs
* [ ] Phone Numbers
* [ ] Business Hours
* [ ] Configuración relevante

---

# 2. Kommo

## 2.1 Pipelines

Registrar:

```text
Pipeline Name

Pipeline ID
```

---

## 2.2 Stages

Registrar todos.

```text
Stage Name

Stage ID
```

---

## 2.3 Custom Fields

Registrar:

```text
Nombre

ID

Tipo

Entidad
```

---

## 2.4 Usuarios

Registrar:

```text
Nombre

User ID

Rol
```

---

## 2.5 Tags

Registrar:

```text
Nombre

ID
```

---

## 2.6 Lead Status

Confirmar:

* Flujo real de ventas
* Uso de cada etapa
* Reglas del negocio

---

## 2.7 Webhooks

Registrar:

* [ ] Ya existen
* [ ] Eventos configurados
* [ ] Destino

---

## 2.8 Integraciones

Revisar:

Settings → Integrations

Registrar:

* Integraciones instaladas
* Integraciones antiguas
* Marketplace Apps

---

# 3. Make

## Organización

Registrar:

* [ ] Organización
* [ ] Team
* [ ] Owners

---

## Connections

Registrar:

* [ ] Kommo
* [ ] Aloware
* [ ] HTTP
* [ ] Otras

---

## Escenarios

Registrar:

* [ ] Nombre
* [ ] Estado
* [ ] Trigger
* [ ] Descripción

---

## Webhooks

Registrar:

* [ ] Nombre
* [ ] URL
* [ ] Uso

---

## Variables

Registrar:

* Variables
* Secrets
* API Keys

---

## Data Stores

Registrar:

* Nombre
* Campos
* Uso

---

# 4. Inventario Técnico

## Kommo

```text
Pipeline ID:

Stages:

Custom Fields:

Users:

Tags:

Webhooks:

Integraciones:
```

---

## Aloware

```text
API Version:

API Token:

Authentication:

Lists:

Ring Groups:

Sequences:

Users:

Custom Fields:

Tags:

Disposition Status:

Lines:

Campaigns:

Webhooks:

Call Logs:

Phone Numbers:

Caller IDs:
```

---

## Make

```text
Organization:

Team:

Connections:

Scenarios:

Webhooks:

Variables:

Data Stores:
```

---

# 5. Prueba Funcional Completa

Realizar el flujo completo y documentar cada resultado.

* [ ] Crear Lead en Kommo
* [ ] Mover el Lead de etapa
* [ ] Confirmar si ocurre alguna automatización
* [ ] Crear Contacto en Aloware
* [ ] Agregarlo a una Lista
* [ ] Verificar asignación (User / Ring Group)
* [ ] Agregar al PowerDialer
* [ ] Realizar una llamada
* [ ] Cambiar Disposition
* [ ] Verificar si cambia el Contacto
* [ ] Revisar Call Logs
* [ ] Revisar Webhooks
* [ ] Registrar observaciones

---

# 6. Pendientes para la Documentación

Durante el relevamiento, identificar y anotar cualquier información necesaria para completar:

* APIs.md
* Authentication.md
* Webhooks.md
* API Objects.md
* API Endpoints.md
* Data Mapping Requirements.md
* Technical Constraints.md
* Technical Risks.md
* Technical Summary.md
* Business Rules.md
* Functional Dependencies.md
* Functional Constraints.md

No abandonar la plataforma sin verificar que toda la información necesaria para estos documentos haya sido recopilada.
