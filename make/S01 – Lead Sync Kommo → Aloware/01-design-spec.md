S01 — Design Specification
Lead Sync: Kommo → Aloware
Información General
Campo	Valor
ID	S01
Nombre	Lead Sync: Kommo → Aloware
Tipo	Event-Driven
Estado	Draft
Prioridad	Alta
Sistema origen	Kommo
Sistema destino	Aloware
Orquestador	Make
Trigger	Webhook Kommo
Frecuencia	Tiempo real
Objetivo

Sincronizar automáticamente un Lead desde Kommo hacia Aloware cuando ingrese en una etapa del pipeline configurada para iniciar una campaña de llamadas.

El escenario será responsable de recibir el evento desde Kommo, validar que cumpla las reglas de negocio, obtener toda la información necesaria del Lead y del Contacto, transformarla al formato requerido por Aloware, crear o actualizar el contacto según corresponda, asignarlo al agente adecuado e incorporarlo a la lista de Power Dialer.

Responsabilidad
Incluye
Recibir el webhook de Kommo.
Validar el evento recibido.
Validar la etapa del Lead.
Obtener información del Lead.
Obtener información del Contacto.
Obtener el Owner del Lead.
Resolver el mapeo Owner → Agent.
Transformar los datos.
Buscar el contacto en Aloware.
Crear el contacto si no existe.
Actualizar el contacto si ya existe.
Asignar el agente correspondiente.
Agregar el contacto a la lista de Power Dialer.
Registrar la ejecución.
Gestionar errores y reintentos.
No incluye
Registrar llamadas en Kommo.
Registrar SMS.
Registrar AI Summary.
Registrar grabaciones.
Sincronizar usuarios.
Sincronizar catálogos.
Trigger
Campo	Valor
Tipo	Custom Webhook
Sistema	Kommo
Evento	Lead Updated
Condición	Cambio de Stage
Condiciones de inicio

El escenario solo continuará cuando:

el Lead exista;
el cambio corresponda a un Stage monitoreado;
el Lead tenga un Contacto asociado;
exista al menos un teléfono válido.

En cualquier otro caso, finalizará sin ejecutar acciones sobre Aloware.

Flujo funcional
Kommo

↓

Lead Updated

↓

Webhook Make

↓

Validar evento

↓

Validar Stage

↓

Obtener Lead

↓

Obtener Contacto

↓

Resolver Owner

↓

Resolver Agent

↓

Transformar datos

↓

Buscar Contacto en Aloware

↓

¿Existe?

├── Sí
│      ↓
│   Actualizar
│
└── No
       ↓
    Crear

↓

Asignar Agente

↓

Agregar a Power Dialer

↓

Registrar ejecución

↓

Fin
Flujo técnico
Paso	Acción
1	Recibir webhook
2	Validar payload
3	Verificar Stage
4	Obtener Lead desde Kommo
5	Obtener Contacto
6	Obtener Owner
7	Resolver Agent
8	Buscar contacto en Aloware
9	Crear o actualizar contacto
10	Asignar agente
11	Agregar a Dialer
12	Registrar resultado
13	Finalizar
Dependencias
Requiere
Conexión API Kommo.
Conexión API Aloware.
Data Store Owner ↔ Agent.
Lista de Stages monitoreados.
Lista de Power Dialers.
Produce
Contacto sincronizado.
Contacto asignado.
Registro de ejecución.
Datos de entrada
Webhook
Campo	Obligatorio
Lead ID	Sí
Pipeline ID	Sí
Stage ID	Sí
Account ID	Sí
Timestamp	Sí
Datos obtenidos desde Kommo
Lead
ID
Nombre
Pipeline
Stage
Owner
Contact ID
Tags
Custom Fields
Contact
Nombre
Apellido
Email
Teléfono
Datos obtenidos desde Mapping
Entrada	Salida
Responsible User ID	Agent ID
Stage	Power Dialer List
Datos enviados a Aloware
Nombre
Apellido
Email
Teléfono
Agent
Dialer List
Variables
Variable	Descripción
leadId	Lead actual
contactId	Contacto Kommo
ownerId	Responsable
agentId	Agente Aloware
dialerListId	Lista destino
correlationId	Identificador de ejecución
Reglas de negocio
Stage

Procesar únicamente las etapas configuradas.

Contacto

No crear contactos sin teléfono.

Owner

Todo Owner debe tener un Agent asociado.

Si no existe, registrar error y finalizar.

Contacto

Si ya existe en Aloware:

Actualizar.

No crear duplicados.

Dialer

Solo agregar el contacto una vez por lista.

Validaciones
Validación	Acción
Payload válido	Continuar
Stage monitoreado	Continuar
Lead existente	Continuar
Contacto existente	Continuar
Teléfono válido	Continuar
Mapping existente	Continuar
Contacto Aloware encontrado	Actualizar
Contacto inexistente	Crear
Idempotencia

La sincronización deberá ser idempotente.

Clave recomendada:

kommo_lead_id

Antes de crear un contacto:

Buscar en Aloware.
Si existe, actualizar.
Nunca crear duplicados.
Manejo de errores
Errores funcionales
Stage inválido.
Lead eliminado.
Contacto inexistente.
Sin teléfono.
Mapping inexistente.

Finalizar escenario registrando el motivo.

Errores API

401

Detener ejecución.

403

Registrar.

404

Registrar.

429

Retry exponencial.

500

Retry.

502

Retry.

503

Retry.

Logging

Registrar:

Fecha.
Correlation ID.
Lead ID.
Contact ID.
Agent.
Resultado.
Tiempo de ejecución.
Código HTTP.
Error (si aplica).
Resultado esperado

Al finalizar correctamente:

El contacto existe en Aloware.
El contacto contiene la información actualizada.
El agente correcto fue asignado.
El contacto pertenece a la lista de Power Dialer correspondiente.
La ejecución quedó registrada.
Criterios de aceptación
Solo procesa Stages configurados.
No genera contactos duplicados.
No crea contactos sin teléfono.
Todo contacto queda asignado a un agente válido.
Todo contacto queda incorporado a la lista correcta.
Los errores quedan registrados.
Las respuestas 429 y 5xx son reintentadas según la estrategia definida.
La ejecución es idempotente.

15. Diseño del Escenario en Make
Tipo de escenario
Campo	Valor
Trigger	Instant
Inicio	Custom Webhook
Conexión	Kommo
Concurrencia	1 ejecución por webhook
Orden	Secuencial
Procesamiento	Sincrónico
Flujo completo de módulos
Webhook
    │
    ▼
Validar Payload
    │
    ▼
Filtro Stage
    │
    ▼
HTTP Get Lead
    │
    ▼
HTTP Get Contact
    │
    ▼
Data Store
Owner → Agent
    │
    ▼
Data Store
Stage → Dialer List
    │
    ▼
Transform Payload
    │
    ▼
HTTP Search Contact
    │
    ▼
Router
├───────────────┐
│               │
▼               ▼
Create      Update
│               │
└───────┬───────┘
        ▼
Assign Agent
        ▼
Add Dialer
        ▼
Log Success
16. Inventario de módulos
Nº	Tipo Make	Nombre
01	Custom Webhook	Receive Lead Update
02	Tools	Normalize Payload
03	Filter	Stage Validation
04	HTTP	Get Lead
05	HTTP	Get Contact
06	Data Store	Owner Mapping
07	Data Store	Dialer Mapping
08	Tools	Build Payload
09	HTTP	Search Contact
10	Router	Contact Exists
11	HTTP	Create Contact
12	HTTP	Update Contact
13	HTTP	Assign Agent
14	HTTP	Add To Dialer
15	Data Store	Execution Log
16	Webhook Response	200 OK
17. Diseño de cada módulo

Aquí comienza el verdadero diseño.

M01

Receive Lead Update

Entrada

Webhook Kommo

Salida

Payload recibido

Error

Payload vacío

↓

Abortar

M02

Normalize Payload

Responsabilidad

Extraer únicamente:

lead_id

pipeline_id

stage_id

timestamp

account_id

No conservar el resto del payload.

M03

Filter Stage

Comparar:

stage_id

contra

Allowed Stages

Si no coincide

↓

Finalizar escenario.

M04

HTTP Get Lead

Entrada

lead_id

Salida

Lead completo

Errores

404

↓

Registrar

↓

Abortar

M05

HTTP Get Contact

Entrada

contact_id

Salida

Contacto

M06

Owner Mapping

Buscar

responsible_user_id

↓

Obtener

agent_id

Si no existe

↓

Error Controlado.

M07

Dialer Mapping

Buscar

stage_id

↓

Obtener

dialer_list_id
M08

Transform Payload

Construir

Payload Aloware.

No realiza llamadas HTTP.

Solo transforma.

M09

Search Contact

Buscar

Por teléfono.

Respuesta

Existe

↓

Router A

No existe

↓

Router B

M10

Router

Ruta A

Update

Ruta B

Create

M11

Create Contact

POST

Aloware

M12

Update Contact

PUT

Aloware

M13

Assign Agent

Asociar

Agent

↓

Contacto

M14

Add Dialer

Agregar

Contacto

↓

Power Dialer

M15

Execution Log

Guardar

Resultado

Tiempo

Lead

Contacto

HTTP Status

Correlation ID

18. Variables
Variables temporales
Variable	Origen
leadId	Webhook
stageId	Webhook
ownerId	Lead
contactId	Lead
phone	Contacto
email	Contacto
Variables derivadas
Variable	Cálculo
agentId	Data Store
dialerListId	Data Store
fullName	Nombre + Apellido
Variables globales
KOMMO_API_URL

ALOWARE_API_URL

RETRY_LIMIT

TIMEOUT

MAX_RETRIES

LOG_LEVEL
19. Data Stores
DS01

Owner Mapping

Key	Value
responsible_user_id	agent_id
DS02

Dialer Mapping

Key	Value
stage_id	dialer_list_id
DS03

Execution Log

Guardar

Correlation ID
Fecha
Resultado
Lead
HTTP
20. Filtros
F01

Stage permitido

stage_id ∈ AllowedStages
F02

Tiene teléfono

phone != null
F03

Existe Mapping

agentId != null
21. Routers
Router 1

Contacto

Existe

↓

Update

No existe

↓

Create

22. Contrato entre módulos
Módulo	Produce	Consume
Webhook	leadId	Normalize
Normalize	leadId	Get Lead
Get Lead	contactId	Get Contact
Get Contact	phone	Search Contact
Mapping	agentId	Assign Agent

Esto evita inconsistencias durante la implementación.

23. Payloads

Aquí documentaría todos los payloads.

Ejemplo

Kommo

↓

Lead

↓

JSON recibido

↓

Payload transformado

↓

JSON enviado a Aloware

Con todos los campos.

24. Convenciones
Nombres módulos
M01 Receive Webhook

M02 Normalize Payload

M03 Validate Stage

...
Variables

camelCase

leadId

contactId

ownerId

agentId
Data Store

Prefijo

DS_
Connections
KOMMO_PROD

ALOWARE_PROD
25. Estrategia de Retry
Error	Acción
429	Retry exponencial
500	Retry
502	Retry
503	Retry

Máximo

3 intentos

Espera

2 s

5 s

10 s
26. Rutas de Error

Cada módulo HTTP tendrá una Error Handler Route específica:

HTTP Error
      │
      ▼
Registrar Error
      │
      ▼
¿Reintentable?
      ├── Sí → Retry
      └── No → Finalizar