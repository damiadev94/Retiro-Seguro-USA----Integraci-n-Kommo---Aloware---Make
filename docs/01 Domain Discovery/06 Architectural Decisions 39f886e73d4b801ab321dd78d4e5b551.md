# 06. Architectural Decisions

---

## Objetivo

Registrar las principales decisiones arquitectónicas tomadas durante la fase de descubrimiento del proyecto.

Este documento resume los acuerdos que guían el diseño, la implementación y la evolución de la integración.

No sustituye a los Architecture Decision Records (ADR), sino que actúa como una referencia de alto nivel.

---

# Decisiones

| ID | Decisión | Justificación |
| --- | --- | --- |
| AD-001 | Kommo es el **Source of Truth** para la información comercial. | Centraliza la gestión del proceso de ventas y evita conflictos de actualización. |
| AD-002 | Aloware es el **Source of Truth** para la información de comunicaciones. | Todas las llamadas, SMS y eventos se originan en Aloware. |
| AD-003 | La integración se implementa mediante una **Plataforma de Integración** basada en Make. | Centraliza la orquestación y desacopla ambas plataformas. |
| AD-004 | Kommo y Aloware nunca se comunican directamente. | Reduce el acoplamiento y facilita el mantenimiento. |
| AD-005 | La Plataforma de Integración no almacena información permanente del negocio. | Mantiene una arquitectura basada en Source of Truth distribuido. |
| AD-006 | La sincronización se realiza preferentemente mediante eventos. | Reduce latencia y evita procesos de consulta innecesarios. |
| AD-007 | Los mapeos pertenecen a la Plataforma de Integración. | La lógica de integración no debe depender de las plataformas externas. |
| AD-008 | La arquitectura debe permanecer independiente de la tecnología utilizada. | Permite reemplazar Make sin rediseñar la solución. |
| AD-009 | La Plataforma de Integración se organiza mediante componentes especializados. | Favorece la reutilización y la separación de responsabilidades. |
| AD-010 | Cada entidad posee un único propietario. | Garantiza consistencia y evita duplicación de datos. |

---

# Principios Derivados

Las decisiones anteriores establecen los siguientes principios arquitectónicos:

- Single Source of Truth.
- Responsabilidad única por plataforma.
- Integración desacoplada.
- Orquestación centralizada.
- Arquitectura dirigida por eventos.
- Separación entre lógica de negocio y comunicación.
- Persistencia distribuida.
- Componentes reutilizables.
- Independencia tecnológica.
- Trazabilidad de las sincronizaciones.

---

# Impacto

Estas decisiones sirven como base para:

- Diseño Técnico.
- Field Mapping.
- Escenarios de Make.
- Manejo de errores.
- Estrategia de sincronización.
- Documentación operativa.

Cualquier cambio que contradiga estas decisiones deberá analizarse antes de su implementación.

---

# Referencias

- Platform Responsibilities
- Responsibilities Validation
- Data Ownership Model
- Architecture Overview
- System Context
- Container Diagram
- Component Diagram

---

## Estado

**Versión:** 1.0

**Estado:** Aprobado

**Fase:** 1.1 – Comprensión del Dominio