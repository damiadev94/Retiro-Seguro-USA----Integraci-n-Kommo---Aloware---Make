# Functional Dependencies

## Objetivo

Este documento identifica las dependencias funcionales de la integración entre **Kommo CRM** y **Aloware**, definiendo qué condiciones, información y capacidades deben existir para que cada proceso de negocio pueda ejecutarse correctamente.

Las dependencias funcionales representan requisitos del dominio y no detalles de implementación técnica.

---

# ¿Qué es una Dependencia Funcional?

Una dependencia funcional es una condición que debe cumplirse para que un caso de uso pueda ejecutarse correctamente.

Puede tratarse de:

- Información existente.
- Configuración previa.
- Relaciones entre entidades.
- Capacidades de las plataformas.
- Reglas de negocio.

Si una dependencia no se cumple, el proceso funcional no puede completarse de forma satisfactoria.

---

# Clasificación

| Categoría | Descripción |
|-----------|-------------|
| Data Dependencies | Información necesaria para ejecutar un proceso. |
| Configuration Dependencies | Configuraciones requeridas previamente. |
| Platform Dependencies | Capacidades proporcionadas por cada plataforma. |
| Integration Dependencies | Elementos necesarios para la coordinación entre sistemas. |

---

# FD-01 — Sincronización de Lead

## Caso de uso

UC-01 — Sincronizar Lead con Aloware.

### Requiere

- Lead existente en Kommo.
- Contacto asociado al Lead.
- Número telefónico válido.
- Etapa del pipeline configurada para sincronización.
- Usuario responsable asignado.

### Resultado

El Lead puede sincronizarse correctamente con Aloware.

---

# FD-02 — Asignación de Lista de Marcación

## Caso de uso

UC-02 — Asignar Lead a una Lista de Marcación.

### Requiere

- Lead sincronizado.
- Etapa válida.
- Matriz de mapeo Stage → Dialing List.

### Resultado

El contacto puede incorporarse a la lista correspondiente.

---

# FD-03 — Asignación de Agente

## Caso de uso

UC-03 — Asignar Agente Responsable.

### Requiere

- Usuario responsable definido en Kommo.
- Correspondencia válida entre usuario y agente.
- Agente disponible en Aloware.

### Resultado

El contacto queda asignado al agente correcto.

---

# FD-04 — Registro de Llamadas

## Caso de uso

UC-04 — Registrar Llamada.

### Requiere

- Evento de llamada recibido.
- Contacto identificable.
- Lead asociado en Kommo.

### Resultado

La llamada puede registrarse correctamente.

---

# FD-05 — Registro de SMS

## Caso de uso

UC-05 — Registrar SMS.

### Requiere

- Evento SMS recibido.
- Número telefónico identificable.
- Lead asociado.

### Resultado

El mensaje queda incorporado al historial comercial.

---

# FD-06 — Registro de Notas

## Caso de uso

UC-06 — Registrar Nota.

### Requiere

- Nota generada en Aloware.
- Lead identificado.

### Resultado

La nota puede asociarse al historial del Lead.

---

# FD-07 — Registro de Grabaciones

## Caso de uso

UC-07 — Registrar Grabación.

### Requiere

- Grabación disponible.
- URL accesible.
- Lead identificado.

### Resultado

La grabación queda referenciada desde Kommo.

---

# FD-08 — Registro de AI Summary

## Caso de uso

UC-08 — Registrar Resumen Generado por IA.

### Requiere

- Resumen generado.
- Lead identificado.

### Resultado

El resumen queda disponible para el equipo comercial.

---

# FD-09 — Actualización de Contactos

## Caso de uso

UC-09 — Actualizar Información del Contacto.

### Requiere

- Contacto existente.
- Datos válidos.
- Evento de actualización.

### Resultado

La información permanece sincronizada.

---

# FD-10 — Gestión de Errores

## Caso de uso

UC-10 — Gestionar Errores de Sincronización.

### Requiere

- Detección de una condición de error.
- Registro del proceso en ejecución.

### Resultado

El incidente puede registrarse y gestionarse sin comprometer la consistencia del sistema.

---

# Dependencias Globales

Las siguientes dependencias aplican a todos los procesos de la integración.

| Dependencia | Propósito |
|-------------|-----------|
| Plataforma Kommo disponible | Acceso a la información comercial. |
| Plataforma Aloware disponible | Acceso a los eventos de comunicación. |
| Make operativo | Coordinación de los flujos de integración. |
| Reglas de negocio definidas | Validación de cada proceso. |
| Mapeos configurados | Resolución de listas y agentes. |
| Identificadores consistentes | Relacionar correctamente entidades entre plataformas. |

---

# Dependencias entre Casos de Uso

| Caso de Uso | Depende de |
|--------------|------------|
| UC-02 Asignar Lista | UC-01 Sincronizar Lead |
| UC-03 Asignar Agente | UC-01 Sincronizar Lead |
| UC-04 Registrar Llamada | Existencia previa del Lead |
| UC-05 Registrar SMS | Existencia previa del Lead |
| UC-06 Registrar Nota | Existencia previa del Lead |
| UC-07 Registrar Grabación | UC-04 Registrar Llamada |
| UC-08 Registrar AI Summary | UC-04 Registrar Llamada |

---

# Consideraciones

- Las dependencias funcionales representan requisitos del negocio y no detalles técnicos de implementación.
- Una dependencia incumplida puede impedir la ejecución total o parcial de un caso de uso.
- La validación de estas dependencias debe realizarse antes de ejecutar cualquier sincronización.
- Las dependencias técnicas (APIs, autenticación, Webhooks o Rate Limits) se documentarán durante la fase de **Technical Analysis**.

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **Actors** | Identifica los participantes involucrados en cada dependencia. |
| **Use Cases** | Define los procesos que requieren estas dependencias. |
| **Domain Events** | Describe los eventos que activan cada proceso. |
| **Business Rules** | Establece las reglas que validan las dependencias. |
| **Technical Analysis** | Documentará cómo se satisfacen técnicamente estas dependencias. |