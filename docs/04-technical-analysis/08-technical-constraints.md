# Technical Constraints

## Objetivo

Este documento identifica las restricciones técnicas que condicionan el diseño, la implementación y la operación de la integración entre **Kommo CRM** y **Aloware**.

Estas restricciones provienen de las capacidades y limitaciones de las plataformas involucradas, de las APIs utilizadas y de la arquitectura de integración basada en **Make**.

No representan reglas de negocio, sino condiciones técnicas que deben considerarse durante el desarrollo.

---

# Clasificación

| Categoría | Descripción |
|-----------|-------------|
| Platform Constraints | Restricciones propias de Kommo y Aloware. |
| API Constraints | Limitaciones relacionadas con las APIs. |
| Integration Constraints | Restricciones derivadas del uso de Make. |
| Data Constraints | Limitaciones sobre el intercambio de información. |
| Operational Constraints | Restricciones durante la operación de la integración. |

---

# Platform Constraints

## TC-01 — Cada plataforma mantiene su propio modelo de datos

Kommo y Aloware poseen estructuras de datos independientes.

La integración no debe asumir que las entidades son equivalentes ni que poseen los mismos atributos.

---

## TC-02 — Cada plataforma mantiene la autoridad sobre sus datos

La integración únicamente puede modificar los datos permitidos por la plataforma propietaria.

No debe intentar sincronizar información cuya administración corresponda exclusivamente al otro sistema.

---

## TC-03 — La disponibilidad de funcionalidades depende de la plataforma

No todas las capacidades del negocio están disponibles mediante las APIs.

La integración deberá adaptarse a las funcionalidades expuestas por cada plataforma.

---

# API Constraints

## TC-04 — Toda operación depende de autenticación válida

Cada solicitud requiere credenciales válidas y permisos suficientes.

La pérdida o expiración de las credenciales impide la ejecución de los procesos correspondientes.

---

## TC-05 — Las APIs pueden imponer restricciones de consumo

El volumen y la frecuencia de solicitudes pueden estar limitados por las plataformas.

La integración deberá diseñarse considerando estas restricciones.

---

## TC-06 — La información recibida puede ser parcial

Los Webhooks o respuestas de la API pueden no contener toda la información necesaria.

La integración deberá consultar información adicional cuando corresponda.

---

## TC-07 — Las APIs pueden evolucionar

Las versiones, estructuras y capacidades de las APIs pueden cambiar con el tiempo.

La integración deberá minimizar el acoplamiento con detalles específicos de implementación.

---

# Integration Constraints

## TC-08 — Make no es un sistema persistente

Make actúa como plataforma de orquestación.

No debe utilizarse como almacenamiento permanente de información de negocio.

---

## TC-09 — Cada escenario debe ser independiente

Los escenarios de Make deben minimizar las dependencias entre sí para facilitar el mantenimiento y reducir el impacto de fallos.

---

## TC-10 — El procesamiento debe ser resiliente

La integración debe tolerar:

- Reintentos.
- Eventos duplicados.
- Fallos temporales.
- Recuperación posterior a errores.

---

# Data Constraints

## TC-11 — Las transformaciones deben preservar la integridad

Las conversiones realizadas durante la sincronización no deben alterar el significado funcional de los datos.

---

## TC-12 — Debe existir una correspondencia identificable entre entidades

La integración requiere mecanismos para relacionar correctamente:

- Leads.
- Contactos.
- Usuarios.
- Agentes.
- Listas de marcación.

Cuando una correspondencia no pueda resolverse, el proceso deberá tratarse como una excepción.

---

## TC-13 — No toda la información disponible será sincronizada

La integración utilizará únicamente los datos necesarios para soportar los procesos definidos durante el análisis funcional.

---

# Operational Constraints

## TC-14 — La integración depende de servicios externos

El funcionamiento de la solución depende de la disponibilidad de:

- Kommo.
- Aloware.
- Make.

Una interrupción en cualquiera de estos servicios puede afectar parcial o totalmente la integración.

---

## TC-15 — Toda operación debe ser trazable

La integración debe registrar suficiente información para permitir el diagnóstico y la auditoría de los procesos ejecutados.

---

## TC-16 — Los errores deben aislarse

Un fallo en un flujo no debe impedir la ejecución del resto de los procesos de integración cuando sea posible.

---

# Resumen de Restricciones

| ID | Restricción |
|----|-------------|
| TC-01 | Cada plataforma mantiene su propio modelo de datos. |
| TC-02 | Cada plataforma conserva la autoridad sobre sus datos. |
| TC-03 | Las funcionalidades disponibles dependen de las capacidades de cada plataforma. |
| TC-04 | Toda operación requiere autenticación válida. |
| TC-05 | Las APIs pueden imponer restricciones de consumo. |
| TC-06 | La información recibida puede ser parcial. |
| TC-07 | Las APIs pueden evolucionar con el tiempo. |
| TC-08 | Make no es un sistema persistente. |
| TC-09 | Los escenarios deben ser independientes. |
| TC-10 | El procesamiento debe ser resiliente. |
| TC-11 | Las transformaciones deben preservar la integridad de los datos. |
| TC-12 | Debe existir correspondencia entre entidades. |
| TC-13 | Sólo se sincroniza la información necesaria. |
| TC-14 | La integración depende de servicios externos. |
| TC-15 | Todas las operaciones deben ser trazables. |
| TC-16 | Los errores deben aislarse siempre que sea posible. |

---

# Consideraciones

- Estas restricciones deben tenerse en cuenta durante el diseño técnico y la implementación.
- Las restricciones representan límites permanentes de la arquitectura y no configuraciones específicas del proyecto.
- La solución deberá minimizar el impacto de estas limitaciones mediante una arquitectura desacoplada, resiliente y orientada a eventos.

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **APIs** | Describe las capacidades generales de las plataformas. |
| **Authentication** | Define los mecanismos de acceso a las APIs. |
| **Webhooks** | Describe el mecanismo de recepción de eventos. |
| **Rate Limits** | Documenta las restricciones de consumo de las APIs. |
| **API Objects** | Define las entidades expuestas por las plataformas. |
| **API Endpoints** | Documenta las operaciones utilizadas por la integración. |
| **Technical Risks** | Identifica los riesgos derivados de estas restricciones. |
| **Technical Design** | Define las estrategias de diseño adoptadas para trabajar dentro de estas limitaciones. |

---

## Recomendación de arquitectura

A partir de este documento queda clara una distinción importante:

**Technical Constraints** → restricciones permanentes impuestas por la tecnología (qué límites existen).
**Technical Risks** → eventos que podrían ocurrir como consecuencia de esas restricciones (qué podría salir mal y cuál sería su impacto).

Esta separación evita mezclar limitaciones con riesgos y hace que la documentación sea más reutilizable para futuros proyectos de integración.