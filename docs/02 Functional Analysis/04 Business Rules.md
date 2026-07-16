# Business Rules

## Objetivo

Este documento define las reglas de negocio que gobiernan el comportamiento de la integración entre **Kommo CRM** y **Aloware**.

Las Business Rules establecen las condiciones que deben cumplirse para que los procesos de sincronización sean válidos y consistentes con la operación comercial del cliente.

Estas reglas son independientes de la implementación técnica y representan decisiones propias del dominio del negocio.

---

# Clasificación

Las reglas se agrupan según el aspecto funcional que controlan.

| Categoría | Descripción |
|-----------|-------------|
| Ownership Rules | Propiedad y autoridad sobre los datos. |
| Synchronization Rules | Condiciones para sincronizar información. |
| Mapping Rules | Correspondencia entre entidades de ambas plataformas. |
| Communication Rules | Gestión de llamadas y mensajes. |
| Data Integrity Rules | Consistencia y calidad de la información. |
| Operational Rules | Reglas generales de funcionamiento. |

---

# Ownership Rules

## BR-01 — Kommo es el sistema de referencia para la información comercial

Kommo mantiene la propiedad de:

- Leads
- Contactos
- Pipelines
- Etapas
- Usuarios responsables

La integración nunca debe sobrescribir esta información utilizando datos provenientes de Aloware.

---

## BR-02 — Aloware es el sistema de referencia para las comunicaciones

Aloware mantiene la propiedad de:

- Llamadas
- SMS
- Grabaciones
- Notas de llamadas
- Resúmenes generados por IA

Kommo únicamente registra estas actividades como parte del historial comercial.

---

# Synchronization Rules

## BR-03 — Sólo las etapas configuradas generan sincronización

No todos los cambios de etapa requieren enviar información hacia Aloware.

La integración únicamente procesará las etapas definidas dentro de la matriz de mapeo Stage → Dialing List.

---

## BR-04 — Toda sincronización debe originarse a partir de un evento válido

Cada proceso de sincronización debe iniciarse únicamente cuando ocurra un evento del dominio reconocido por la integración.

---

## BR-05 — La sincronización debe ser idempotente

El procesamiento repetido del mismo evento no debe producir efectos duplicados ni inconsistencias.

---

# Mapping Rules

## BR-06 — Cada etapa corresponde a una única lista de marcación

Una etapa del pipeline sólo puede asociarse a una lista de marcación activa.

La relación se define mediante una matriz de configuración.

---

## BR-07 — Cada usuario responsable debe tener un agente equivalente

Para asignar correctamente las comunicaciones, el usuario responsable del Lead debe tener una correspondencia válida con un agente de Aloware.

Si no existe dicha correspondencia, la sincronización deberá tratarse como una excepción.

---

# Communication Rules

## BR-08 — Toda llamada debe registrarse

Cada llamada finalizada debe quedar registrada en el historial del Lead correspondiente.

---

## BR-09 — Todo SMS debe conservarse

Los mensajes enviados y recibidos forman parte del historial comercial y deben registrarse en Kommo.

---

## BR-10 — Las grabaciones deben conservarse mediante referencia

La integración registrará la referencia o URL de la grabación disponible en Aloware.

No almacenará copias del archivo de audio.

---

## BR-11 — Los resúmenes generados por IA deben incorporarse al historial

Cuando Aloware genere un resumen automático, éste deberá quedar asociado al Lead correspondiente.

---

# Data Integrity Rules

## BR-12 — No deben crearse contactos duplicados

La integración debe identificar correctamente un contacto existente antes de crear uno nuevo.

La estrategia de identificación se definirá durante el diseño técnico.

---

## BR-13 — Sólo se sincronizan datos válidos

La integración procesará únicamente registros que contengan la información mínima requerida para cada flujo.

---

## BR-14 — Las transformaciones no modifican el significado del dato

Durante la sincronización pueden cambiar el formato o la estructura de los datos, pero nunca su significado funcional.

---

# Operational Rules

## BR-15 — Make no almacena información de negocio

Make actúa únicamente como plataforma de integración.

No constituye una fuente permanente de datos del negocio.

---

## BR-16 — Todas las operaciones deben ser trazables

Cada sincronización debe poder auditarse mediante registros que permitan conocer:

- Evento procesado.
- Fecha y hora.
- Resultado.
- Error, en caso de existir.

---

## BR-17 — Los errores no deben comprometer la consistencia

Ante un fallo, la integración debe evitar estados inconsistentes entre plataformas y registrar la incidencia para su posterior análisis.

---

# Resumen de Reglas

| ID | Regla |
|----|--------|
| BR-01 | Kommo es el sistema de referencia para la información comercial. |
| BR-02 | Aloware es el sistema de referencia para las comunicaciones. |
| BR-03 | Sólo las etapas configuradas generan sincronización. |
| BR-04 | Toda sincronización parte de un evento válido. |
| BR-05 | La sincronización debe ser idempotente. |
| BR-06 | Cada etapa corresponde a una única lista de marcación. |
| BR-07 | Cada usuario responsable debe tener un agente equivalente. |
| BR-08 | Toda llamada debe registrarse. |
| BR-09 | Todo SMS debe conservarse. |
| BR-10 | Las grabaciones se almacenan mediante referencia. |
| BR-11 | Los resúmenes generados por IA deben registrarse. |
| BR-12 | No deben crearse contactos duplicados. |
| BR-13 | Sólo se sincronizan datos válidos. |
| BR-14 | Las transformaciones preservan el significado del dato. |
| BR-15 | Make no almacena información de negocio. |
| BR-16 | Todas las operaciones deben ser trazables. |
| BR-17 | Los errores no deben comprometer la consistencia. |

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **Actors** | Define quién participa en la aplicación de las reglas. |
| **Use Cases** | Describe los procesos regulados por estas reglas. |
| **Domain Events** | Define los eventos que activan las reglas de negocio. |
| **Data Ownership Model** | Establece la propiedad de los datos utilizada por las Ownership Rules. |
| **Information Flow** | Describe el recorrido de la información sujeto a estas reglas. |
| **Technical Analysis** | Documentará cómo se implementan técnicamente estas reglas durante la integración. |