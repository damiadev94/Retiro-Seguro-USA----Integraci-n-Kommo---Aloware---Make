# Functional Constraints

## Objetivo

Este documento define las restricciones funcionales que limitan el comportamiento de la integración entre **Kommo CRM** y **Aloware**.

A diferencia de las reglas de negocio, que establecen cómo debe comportarse la integración, las restricciones funcionales describen **qué no puede hacer** o **qué condiciones deben respetarse** para preservar la coherencia del proceso de negocio.

Estas restricciones son independientes de la implementación técnica y representan límites propios del dominio.

---

# Clasificación

| Categoría | Descripción |
|-----------|-------------|
| Ownership Constraints | Restricciones relacionadas con la propiedad de los datos. |
| Synchronization Constraints | Limitaciones sobre los procesos de sincronización. |
| Data Constraints | Restricciones sobre la información intercambiada. |
| Operational Constraints | Restricciones del funcionamiento general de la integración. |

---

# Ownership Constraints

## FC-01 — La integración no modifica la lógica de negocio de las plataformas

La integración no altera el funcionamiento interno de Kommo ni de Aloware.

Su responsabilidad se limita a sincronizar información entre ambos sistemas.

---

## FC-02 — La propiedad de los datos debe respetarse en todo momento

Cada entidad sólo puede ser modificada por su sistema propietario.

La integración no debe sobrescribir información cuya autoridad corresponda a otra plataforma.

---

# Synchronization Constraints

## FC-03 — Sólo se sincronizan procesos definidos

La integración únicamente ejecuta los flujos de negocio previamente configurados.

Eventos fuera del alcance funcional deben ser ignorados.

---

## FC-04 — Cada evento se procesa una única vez

Un mismo evento no debe generar múltiples sincronizaciones equivalentes.

La integración debe evitar duplicados durante el procesamiento.

---

## FC-05 — La sincronización no modifica procesos comerciales

La integración automatiza tareas operativas, pero no cambia el flujo comercial definido por la organización.

Las decisiones comerciales continúan siendo responsabilidad de los usuarios.

---

# Data Constraints

## FC-06 — Sólo se procesan datos mínimos requeridos

Cada flujo utilizará únicamente la información necesaria para cumplir su objetivo.

No deben sincronizarse datos sin una finalidad funcional.

---

## FC-07 — No se crean relaciones ambiguas

Cada Lead, contacto, agente y lista de marcación debe poder identificarse de forma unívoca.

La integración no debe operar sobre entidades cuya correspondencia no pueda determinarse.

---

## FC-08 — Las transformaciones conservan el significado del dato

Las conversiones de formato o estructura no deben alterar el valor funcional de la información.

---

# Operational Constraints

## FC-09 — Make no constituye una fuente de información

Make actúa únicamente como plataforma de integración.

No almacena información de negocio como fuente permanente.

---

## FC-10 — La integración debe ser transparente para el usuario

Los procesos de sincronización deben ejecutarse automáticamente sin requerir intervención manual durante la operación normal.

---

## FC-11 — Toda operación debe ser auditable

Cada proceso ejecutado debe poder rastrearse mediante registros que permitan reconstruir el flujo de ejecución.

---

## FC-12 — Los errores no deben comprometer la consistencia funcional

Ante un fallo, la integración debe evitar generar estados inconsistentes entre Kommo y Aloware.

Los errores deben registrarse y gestionarse de forma controlada.

---

# Restricciones Generales

La integración no contempla las siguientes funcionalidades:

- Modificar pipelines de Kommo.
- Administrar usuarios o agentes.
- Crear lógica comercial propia.
- Almacenar información histórica fuera de las plataformas propietarias.
- Reemplazar las funcionalidades nativas de Kommo o Aloware.

---

# Resumen de Restricciones

| ID | Restricción |
|----|-------------|
| FC-01 | No modifica la lógica de negocio de las plataformas. |
| FC-02 | Respeta la propiedad de los datos. |
| FC-03 | Sólo sincroniza procesos definidos. |
| FC-04 | Cada evento se procesa una única vez. |
| FC-05 | No modifica el proceso comercial. |
| FC-06 | Sólo procesa la información necesaria. |
| FC-07 | Requiere correspondencias unívocas entre entidades. |
| FC-08 | Conserva el significado de los datos durante las transformaciones. |
| FC-09 | Make no es una fuente permanente de información. |
| FC-10 | La operación es transparente para el usuario. |
| FC-11 | Todas las operaciones son auditables. |
| FC-12 | Los errores no deben comprometer la consistencia funcional. |

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **Actors** | Identifica los actores sujetos a estas restricciones. |
| **Use Cases** | Describe los procesos limitados por estas restricciones. |
| **Business Rules** | Define las reglas que gobiernan el comportamiento dentro de estos límites. |
| **Functional Dependencies** | Establece los requisitos necesarios antes de ejecutar cada proceso. |
| **Technical Analysis** | Documentará las restricciones técnicas adicionales (APIs, autenticación, Webhooks y Rate Limits). |