# Runbook de Implementación

# S01 – Lead Sync: Kommo → Aloware

---

# Objetivo

Construir el escenario que sincroniza automáticamente un Lead desde Kommo hacia Aloware cuando el Lead ingresa en una etapa configurada.

---

# Requisitos

Antes de comenzar verificar que existan:

* Conexión API a Kommo.
* Conexión API a Aloware.
* API Keys / OAuth configurados.
* Data Store **DS_OwnerMapping**.
* Data Store **DS_DialerMapping**.
* Lista de Stages monitoreados.
* Lista de Power Dialers.

---

# Resultado esperado

El escenario deberá quedar con la siguiente estructura:

```text
Webhook
    │
Normalize Payload
    │
Filter Stage
    │
HTTP Get Lead
    │
HTTP Get Contact
    │
DS Owner Mapping
    │
DS Dialer Mapping
    │
Build Payload
    │
HTTP Search Contact
    │
Router
 ├─────────────┐
 │             │
Create      Update
 │             │
 └──────┬──────┘
        │
Assign Agent
        │
Add To Dialer
        │
Execution Log
        │
Webhook Response
```

---

# Paso 1 — Crear el escenario

Crear un escenario nuevo.

**Nombre**

```text
S01 - Lead Sync - Kommo to Aloware
```

**Scheduling**

Instant.

Guardar.

---

# Paso 2 — Crear el Webhook

Agregar módulo:

```
Webhooks
→ Custom Webhook
```

Nombre

```text
Lead Updated
```

Guardar.

Copiar la URL generada.

---

# Paso 3 — Configurar Kommo

Ir a:

Configuración

→ Integraciones

→ Webhooks

Crear un nuevo Webhook.

Pegar la URL del paso anterior.

Seleccionar el evento:

* Lead Updated

Guardar.

---

# Paso 4 — Probar recepción

Volver a Make.

Presionar:

```
Run Once
```

Mover un Lead a una etapa monitoreada.

Verificar que Make reciba el payload.

Si el payload no llega:

* Revisar URL.
* Revisar permisos.
* Revisar configuración del Webhook.

No continuar hasta recibir correctamente el evento.

---

# Paso 5 — Agregar "Normalize Payload"

Agregar módulo:

```
Tools
→ Set Multiple Variables
```

Crear las siguientes variables:

| Variable   | Valor            |
| ---------- | ---------------- |
| leadId     | Lead ID recibido |
| pipelineId | Pipeline ID      |
| stageId    | Stage ID         |
| accountId  | Account ID       |
| timestamp  | Timestamp        |

Guardar.

---

# Paso 6 — Agregar filtro de Stage

Crear un filtro entre:

Normalize Payload

↓

HTTP Get Lead

Condición:

```
stageId pertenece a AllowedStages
```

Si no cumple:

Finalizar ejecución.

---

# Paso 7 — Obtener Lead

Agregar módulo:

```
HTTP
→ Make a Request
```

Nombre

```
Get Lead
```

Método

```
GET
```

Endpoint

```
/api/v4/leads/{{leadId}}
```

Headers

```
Authorization
Bearer {{KOMMO_TOKEN}}
```

Guardar.

Ejecutar.

Verificar respuesta HTTP 200.

---

# Paso 8 — Obtener Contacto

Agregar otro módulo HTTP.

Nombre

```
Get Contact
```

Método

```
GET
```

Endpoint

```
/api/v4/contacts/{{contactId}}
```

Guardar.

Verificar respuesta 200.

---

# Paso 9 — Buscar Owner Mapping

Agregar módulo:

```
Data Store
→ Get a Record
```

Data Store

```
DS_OwnerMapping
```

Key

```
responsible_user_id
```

Guardar.

Verificar que devuelve:

```
agentId
```

Si no existe registro:

Finalizar con error controlado.

---

# Paso 10 — Buscar Dialer Mapping

Agregar módulo:

```
Data Store
→ Get a Record
```

Data Store

```
DS_DialerMapping
```

Key

```
stageId
```

Verificar que devuelve:

```
dialerListId
```

---

# Paso 11 — Construir Payload

Agregar módulo:

```
Tools
→ Set Multiple Variables
```

Construir:

* first_name
* last_name
* phone
* email
* agentId
* dialerListId

No realizar llamadas HTTP en este paso.

Solo preparar el payload.

---

# Paso 12 — Buscar Contacto en Aloware

Agregar módulo:

```
HTTP
→ Make a Request
```

Nombre

```
Search Contact
```

Método

```
GET
```

Buscar utilizando:

```
phone
```

Guardar.

---

# Paso 13 — Crear Router

Agregar un Router.

Crear dos rutas.

## Ruta A

Contacto encontrado.

## Ruta B

Contacto no encontrado.

---

# Paso 14 — Ruta A (Actualizar)

Agregar módulo HTTP.

Nombre

```
Update Contact
```

Método

```
PUT
```

Endpoint

```
/contacts/{contactId}
```

Enviar el payload construido.

Guardar.

---

# Paso 15 — Ruta B (Crear)

Agregar módulo HTTP.

Nombre

```
Create Contact
```

Método

```
POST
```

Endpoint

```
/contacts
```

Enviar el payload construido.

Guardar.

---

# Paso 16 — Unificar rutas

Conectar ambas rutas al siguiente módulo.

Verificar que ambas continúan correctamente.

---

# Paso 17 — Asignar Agente

Agregar módulo HTTP.

Nombre

```
Assign Agent
```

Método

```
POST
```

Enviar:

* Contact ID
* Agent ID

Guardar.

---

# Paso 18 — Agregar al Power Dialer

Agregar módulo HTTP.

Nombre

```
Add To Dialer
```

Enviar:

* Contact ID
* Dialer List ID

Guardar.

---

# Paso 19 — Registrar ejecución

Agregar módulo:

```
Data Store
→ Create or Update Record
```

Data Store

```
DS_ExecutionLog
```

Registrar:

* Correlation ID
* Lead ID
* Contact ID
* Agent ID
* Resultado
* Fecha
* Código HTTP

Guardar.

---

# Paso 20 — Responder al Webhook

Agregar módulo:

```
Webhook Response
```

Status

```
200
```

Body

```json
{
  "status":"success"
}
```

Guardar.

---

# Configurar rutas de error

En todos los módulos HTTP:

Agregar Error Handler.

## Error 401

Finalizar.

---

## Error 404

Registrar.

Finalizar.

---

## Error 429

Retry.

Máximo:

```
3 intentos
```

Espera:

* 2 segundos
* 5 segundos
* 10 segundos

---

## Error 500

Retry.

---

## Error 502

Retry.

---

## Error 503

Retry.

---

# Validación final

Ejecutar nuevamente el escenario.

Verificar:

* El Webhook recibe el evento.
* El Stage pasa el filtro.
* El Lead se obtiene correctamente.
* El Contacto se obtiene correctamente.
* El Mapping devuelve Agent.
* El Mapping devuelve Dialer.
* El Contacto se crea o actualiza.
* El Agente queda asignado.
* El Contacto queda agregado al Dialer.
* El Log se registra.
* El escenario finaliza con HTTP 200.

---

# Checklist

* ☐ Escenario creado.
* ☐ Webhook funcionando.
* ☐ Filtro de Stage configurado.
* ☐ Consulta de Lead correcta.
* ☐ Consulta de Contacto correcta.
* ☐ Owner Mapping funcionando.
* ☐ Dialer Mapping funcionando.
* ☐ Payload construido.
* ☐ Búsqueda de Contacto correcta.
* ☐ Router configurado.
* ☐ Create Contact probado.
* ☐ Update Contact probado.
* ☐ Assign Agent probado.
* ☐ Add To Dialer probado.
* ☐ Logging funcionando.
* ☐ Error Handlers configurados.
* ☐ Prueba completa exitosa.
