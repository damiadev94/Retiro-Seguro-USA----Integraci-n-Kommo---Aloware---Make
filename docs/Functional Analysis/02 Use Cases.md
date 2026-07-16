# Use Cases

## Objetivo

Este documento describe las funcionalidades que la integración entre **Kommo CRM** y **Aloware** debe soportar desde la perspectiva del negocio.

Cada caso de uso representa un comportamiento esperado del sistema, independientemente de su implementación técnica.

---

# Clasificación

Los casos de uso se agrupan según la dirección del flujo de información.

| Categoría | Descripción |
|-----------|-------------|
| **Kommo → Aloware** | Automatización de la operación del Power Dialer a partir de eventos comerciales. |
| **Aloware → Kommo** | Registro automático de las comunicaciones realizadas con los clientes. |

---

# UC-01 — Sincronizar Lead con Aloware

## Objetivo

Enviar un Lead desde Kommo hacia Aloware cuando su estado comercial requiera iniciar una gestión telefónica.

## Actor iniciador

- Kommo CRM

## Disparador

Cambio de etapa del Lead.

## Flujo

1. Se detecta el cambio de etapa.
2. Se valida que la etapa sea sincronizable.
3. Se obtiene la información del Lead.
4. Se identifica el agente responsable.
5. Se crea o actualiza el contacto en Aloware.

## Resultado esperado

El contacto queda disponible para ser gestionado desde Aloware.

---

# UC-02 — Asignar Lead a una Lista de Marcación

## Objetivo

Ubicar automáticamente el contacto en la lista de marcación correspondiente según la etapa del proceso comercial.

## Actor iniciador

- Kommo CRM

## Disparador

Lead sincronizado correctamente.

## Flujo

1. Se identifica la etapa del Lead.
2. Se consulta la matriz Stage → Dialing List.
3. Se asigna el contacto a la lista correspondiente.

## Resultado esperado

El Lead queda incorporado al flujo de llamadas adecuado.

---

# UC-03 — Asignar Agente Responsable

## Objetivo

Relacionar el responsable del Lead en Kommo con el agente correspondiente en Aloware.

## Actor iniciador

- Kommo CRM

## Disparador

Creación o actualización del contacto.

## Flujo

1. Se obtiene el usuario responsable.
2. Se consulta la tabla de equivalencias.
3. Se asigna el agente correspondiente.

## Resultado esperado

Las llamadas son gestionadas por el agente correcto.

---

# UC-04 — Registrar Llamada

## Objetivo

Registrar automáticamente una llamada realizada desde Aloware dentro del Lead correspondiente en Kommo.

## Actor iniciador

- Aloware

## Disparador

Finalización de una llamada.

## Flujo

1. Aloware genera el evento.
2. Se identifica el Lead.
3. Se registra la actividad en Kommo.

## Resultado esperado

La llamada queda asociada al historial del Lead.

---

# UC-05 — Registrar SMS

## Objetivo

Registrar automáticamente los mensajes SMS enviados o recibidos.

## Actor iniciador

- Aloware

## Disparador

Envío o recepción de un SMS.

## Flujo

1. Se recibe el evento.
2. Se identifica el Lead.
3. Se registra el mensaje.

## Resultado esperado

El historial de comunicaciones permanece centralizado en Kommo.

---

# UC-06 — Registrar Nota

## Objetivo

Incorporar notas generadas durante una interacción telefónica.

## Actor iniciador

- Aloware

## Disparador

Creación de una nota.

## Flujo

1. Se recibe la nota.
2. Se identifica el Lead.
3. Se registra como actividad.

## Resultado esperado

La información queda disponible para el equipo comercial.

---

# UC-07 — Registrar Grabación

## Objetivo

Asociar la grabación de una llamada al Lead correspondiente.

## Actor iniciador

- Aloware

## Disparador

Disponibilidad de una grabación.

## Flujo

1. Se recibe el enlace de la grabación.
2. Se identifica el Lead.
3. Se registra el enlace en Kommo.

## Resultado esperado

La grabación queda disponible desde el CRM.

---

# UC-08 — Registrar Resumen Generado por IA

## Objetivo

Registrar automáticamente el resumen generado por AloAI después de una llamada.

## Actor iniciador

- Aloware

## Disparador

Generación del AI Summary.

## Flujo

1. Se recibe el resumen.
2. Se identifica el Lead.
3. Se registra como nota o actividad.

## Resultado esperado

El equipo comercial dispone del resumen sin intervención manual.

---

# UC-09 — Actualizar Información del Contacto

## Objetivo

Mantener sincronizada la información necesaria para la operación entre ambas plataformas.

## Actor iniciador

- Kommo CRM

## Disparador

Modificación de datos relevantes del contacto.

## Flujo

1. Se detecta el cambio.
2. Se validan los datos.
3. Se actualiza el contacto en Aloware.

## Resultado esperado

La información operativa permanece actualizada.

---

# UC-10 — Gestionar Errores de Sincronización

## Objetivo

Detectar y registrar fallos durante los procesos de sincronización.

## Actor iniciador

- Make

## Disparador

Error durante cualquier flujo.

## Flujo

1. Se detecta el error.
2. Se registra el incidente.
3. Se finaliza el proceso o se ejecutan las políticas de recuperación definidas.

## Resultado esperado

Los errores son trazables y pueden resolverse sin pérdida de información.

---

# Resumen de Casos de Uso

| ID | Caso de Uso | Actor Iniciador |
|----|-------------|-----------------|
| UC-01 | Sincronizar Lead con Aloware | Kommo |
| UC-02 | Asignar Lead a Lista de Marcación | Kommo |
| UC-03 | Asignar Agente Responsable | Kommo |
| UC-04 | Registrar Llamada | Aloware |
| UC-05 | Registrar SMS | Aloware |
| UC-06 | Registrar Nota | Aloware |
| UC-07 | Registrar Grabación | Aloware |
| UC-08 | Registrar Resumen Generado por IA | Aloware |
| UC-09 | Actualizar Información del Contacto | Kommo |
| UC-10 | Gestionar Errores de Sincronización | Make |

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **Actors** | Define los actores que participan en cada caso de uso. |
| **Domain Events** | Describe los eventos que disparan cada caso de uso. |
| **Business Rules** | Define las reglas que condicionan el comportamiento de cada caso de uso. |
| **Information Flow** | Describe el recorrido de la información durante la ejecución de los casos de uso. |