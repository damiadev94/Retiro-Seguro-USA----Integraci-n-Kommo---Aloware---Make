# Functional Summary

## Objetivo

Este documento resume los resultados obtenidos durante la fase de **Functional Analysis**, consolidando el comportamiento esperado de la integración entre **Kommo CRM** y **Aloware** desde la perspectiva del negocio.

El objetivo de esta fase fue definir **qué debe hacer la integración**, **quién participa**, **qué eventos la impulsan** y **qué reglas gobiernan su funcionamiento**, antes de abordar el diseño técnico y la implementación.

---

# Alcance

Durante esta fase se documentaron los siguientes aspectos funcionales:

- Actores del dominio.
- Casos de uso.
- Eventos del dominio.
- Reglas de negocio.
- Dependencias funcionales.
- Restricciones funcionales.

---

# Actores Identificados

Se identificaron los participantes involucrados en la operación de la integración.

### Actores Humanos

- CRM Administrator
- Sales Manager
- Sales Agent

### Actores del Sistema

- Kommo CRM
- Aloware
- Make

Cada actor posee responsabilidades claramente definidas y participa en uno o más procesos de negocio.

---

# Casos de Uso

Se definieron los principales procesos funcionales soportados por la integración.

## Kommo → Aloware

- Sincronizar Lead.
- Asignar Lead a una lista de marcación.
- Asignar agente responsable.
- Actualizar información del contacto.

## Aloware → Kommo

- Registrar llamadas.
- Registrar SMS.
- Registrar notas.
- Registrar grabaciones.
- Registrar resúmenes generados por IA.

## Operación

- Gestionar errores de sincronización.

---

# Eventos del Dominio

Se identificaron los eventos de negocio que impulsan el comportamiento de la integración.

### Eventos originados en Kommo

- Lead Stage Changed
- Lead Updated
- Contact Updated

### Eventos originados en Aloware

- Call Completed
- SMS Sent
- SMS Received
- Note Created
- Recording Available
- AI Summary Generated

### Eventos de Integración

- Synchronization Started
- Synchronization Completed
- Synchronization Failed

---

# Reglas de Negocio

Las principales políticas funcionales definidas son:

- Kommo es el sistema de referencia para la información comercial.
- Aloware es el sistema de referencia para las comunicaciones.
- Sólo los procesos configurados participan en la sincronización.
- Cada etapa del pipeline corresponde a una única lista de marcación.
- Cada usuario responsable debe corresponder a un agente de Aloware.
- La sincronización debe ser idempotente.
- Toda comunicación debe quedar registrada en el historial del Lead.
- La integración debe preservar la consistencia de los datos entre plataformas.

---

# Dependencias Funcionales

Se identificaron los requisitos que deben cumplirse antes de ejecutar cada proceso.

Entre las dependencias principales se encuentran:

- Existencia del Lead.
- Contacto asociado.
- Número telefónico válido.
- Usuario responsable asignado.
- Mapeos de etapas y agentes.
- Eventos válidos.
- Correspondencias entre entidades.

---

# Restricciones Funcionales

La integración debe respetar los siguientes límites:

- No modifica la lógica interna de Kommo ni de Aloware.
- No altera el proceso comercial definido por la organización.
- No actúa como sistema de almacenamiento permanente.
- Sólo procesa información necesaria para cada flujo.
- Todas las operaciones deben ser auditables.
- Los errores no deben comprometer la consistencia entre plataformas.

---

# Resultado del Análisis Funcional

La integración quedó definida desde el punto de vista del negocio.

Se establecieron:

- Los participantes del sistema.
- Las funcionalidades esperadas.
- Los eventos que impulsan los procesos.
- Las reglas que gobiernan el dominio.
- Las dependencias necesarias.
- Las restricciones que limitan el comportamiento.

Esta información constituye la base funcional sobre la cual se diseñará la solución técnica.

---

# Estado de la Fase

| Área | Estado |
|------|--------|
| Actors | ✅ Completo |
| Use Cases | ✅ Completo |
| Domain Events | ✅ Completo |
| Business Rules | ✅ Completo |
| Functional Dependencies | ✅ Completo |
| Functional Constraints | ✅ Completo |

---

# Criterio de Finalización

La fase de análisis funcional se considera finalizada cuando:

- Los actores del dominio están identificados.
- Los casos de uso representan todos los procesos soportados.
- Los eventos de negocio están definidos.
- Las reglas de negocio han sido documentadas.
- Las dependencias funcionales son conocidas.
- Las restricciones funcionales están establecidas.
- Existe una comprensión compartida del comportamiento esperado de la integración.

---

# Próximo Paso

Con el comportamiento funcional completamente definido, el proyecto continúa con la **Fase 1.3 – Technical Analysis**, donde se documentarán los aspectos técnicos necesarios para implementar la integración, incluyendo:

- APIs.
- Autenticación.
- Webhooks.
- Rate Limits.
- Objetos y entidades expuestas por cada API.
- Restricciones técnicas.
- Limitaciones de las plataformas.