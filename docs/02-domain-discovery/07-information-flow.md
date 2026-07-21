# 07. Information Flow

---

## Objetivo

Este documento describe cómo fluye la información entre **Kommo**, **Make** y **Aloware**, definiendo el recorrido de cada evento, las transformaciones realizadas y las responsabilidades de cada plataforma durante la sincronización.

No describe la implementación técnica de los escenarios de Make, sino el comportamiento conceptual de la integración.

---

# 1. Participantes

| Sistema | Rol |
| --- | --- |
| **Kommo CRM** | Sistema de registro principal (Source of Truth para ventas y clientes). |
| **Make** | Orquestador de eventos, validaciones y transformaciones. |
| **Aloware** | Plataforma de telefonía, marcación y comunicación con el cliente. |

---

# 2. Principios del Flujo

- Los datos siempre tienen un sistema propietario.
- Make no almacena información de negocio de forma permanente.
- Cada flujo tiene un único sistema iniciador.
- Las transformaciones ocurren únicamente dentro de Make.
- Los eventos deben propagarse una sola vez para evitar duplicados.
- Cada sincronización debe ser trazable mediante logs.

---

# 3. Flujo Maestro

```
                 ┌─────────────┐
                 │   Kommo     │
                 └──────┬──────┘
                        │
              Lead / Stage Change
                        │
                        ▼
                 ┌─────────────┐
                 │    Make     │
                 └──────┬──────┘
                        │
      Transformación y Validaciones
                        │
                        ▼
                 ┌─────────────┐
                 │  Aloware    │
                 └─────────────┘

                 ┌─────────────┐
                 │  Aloware    │
                 └──────┬──────┘
                        │
           Call / SMS / Notes / AI
                        │
                        ▼
                 ┌─────────────┐
                 │    Make     │
                 └──────┬──────┘
                        │
           Registro de actividad
                        │
                        ▼
                 ┌─────────────┐
                 │   Kommo     │
                 └─────────────┘
```

---

# 4. Flujo Kommo → Aloware

## Disparador

Cambio de etapa del Lead en Kommo.

## Origen

Kommo CRM.

## Proceso

1. Kommo genera el evento.
2. Make recibe el webhook.
3. Se valida que la etapa requiera sincronización.
4. Se obtiene la información completa del Lead.
5. Se determina el agente correspondiente.
6. Se identifica la lista de marcación.
7. Se crea o actualiza el contacto en Aloware.
8. Se asigna el contacto a la lista correspondiente.

## Resultado

El Lead queda preparado para ser gestionado por el equipo de llamadas.

---

# 5. Flujo Aloware → Kommo

## Disparador

Evento generado por Aloware.

Ejemplos:

- Llamada finalizada.
- SMS enviado.
- SMS recibido.
- Nota creada.
- Grabación disponible.
- Resumen AloAI generado.

## Origen

Aloware.

## Proceso

1. Aloware envía un webhook.
2. Make identifica el tipo de evento.
3. Se localiza el Lead correspondiente.
4. Se transforma el evento al formato de Kommo.
5. Se registra la actividad en el CRM.

## Resultado

Toda la actividad telefónica queda centralizada dentro de Kommo.

---

# 6. Transformaciones de Datos

Durante la sincronización, Make puede realizar las siguientes transformaciones:

| Transformación | Descripción |
| --- | --- |
| Stage → Dialing List | Conversión de una etapa de Kommo en una lista de marcación de Aloware. |
| Responsible User → Agent | Conversión del responsable del Lead en un agente de Aloware. |
| Phone Formatting | Normalización del número telefónico. |
| Event Mapping | Conversión de eventos de Aloware al modelo de actividades de Kommo. |
| Payload Transformation | Adaptación del formato de datos entre ambas APIs. |

---

# 7. Flujo de Datos

| Dirección | Información |
| --- | --- |
| Kommo → Make | Lead, Contacto, Responsable, Etapa, Datos del cliente. |
| Make → Aloware | Contacto, Lista, Agente, Datos necesarios para llamadas. |
| Aloware → Make | Eventos de llamadas, SMS, notas, grabaciones y resúmenes IA. |
| Make → Kommo | Actividades, notas, enlaces a grabaciones y comunicaciones registradas. |

---

# 8. Límites del Flujo

La integración **no** modifica directamente:

- La lógica interna de Kommo.
- La lógica interna de Aloware.
- Los procesos comerciales definidos por el cliente.

Make únicamente coordina y sincroniza la información entre ambos sistemas.

---

# 9. Consideraciones

- Cada evento debe procesarse una única vez.
- La sincronización debe ser idempotente.
- Los errores deben registrarse para permitir su seguimiento.
- Los datos deben mantenerse consistentes entre ambos sistemas.
- El flujo debe minimizar la intervención manual.

---

# Relación con otros documentos

| Documento | Propósito |
| --- | --- |
| **Platform Responsibilities** | Define el rol de cada plataforma. |
| **Data Ownership Model** | Define el propietario de cada dato. |
| **Architecture Overview** | Presenta la arquitectura general de la integración. |
| **System Context** | Describe los sistemas participantes y sus relaciones. |
| **Container Diagram** | Muestra los contenedores principales de la solución. |
| **Component Diagram** | Describe los componentes internos de la integración. |
| **Architectural Decisions** | Documenta las decisiones de diseño adoptadas. |