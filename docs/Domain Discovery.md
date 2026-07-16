# Domain Discovery

---

[01. Platform Responsibilities](Domain%20Discovery/01%20Platform%20Responsibilities%2039f886e73d4b80e79265ec048365c858.md)

[02. Responsibilities Validation](Domain%20Discovery/02%20Responsibilities%20Validation%2039f886e73d4b80cb9bb7c037c1db4b78.md)

[03. Data Ownership Model](Domain%20Discovery/03%20Data%20Ownership%20Model%2039f886e73d4b80ec867de844b63b0cb9.md)

[04. Architecture Overview](Domain%20Discovery/04%20Architecture%20Overview%2039f886e73d4b8073ad6bc361261b6e21.md)

[05. System Context](Domain%20Discovery/05%20System%20Context%2039f886e73d4b80e8a854f242cf2d8d3d.md)

[06. Architectural Decisions](Domain%20Discovery/06%20Architectural%20Decisions%2039f886e73d4b801ab321dd78d4e5b551.md)

[07. Information Flow](Domain%20Discovery/07%20Information%20Flow%2039f886e73d4b8015b9b7e52ce7775b54.md)

## Discovery Report

### Objetivo

Este documento resume los resultados de la fase de descubrimiento del proyecto de integración entre **Kommo CRM** y **Aloware**, consolidando el conocimiento obtenido sobre el dominio, las responsabilidades de cada plataforma, la arquitectura propuesta y los principales riesgos identificados.

La finalización de esta fase permite avanzar al diseño funcional y técnico con una comprensión compartida del problema y una base arquitectónica consistente.

---

## Alcance del Descubrimiento

Durante esta fase se analizaron los siguientes aspectos:

- Objetivos del negocio.
- Plataformas involucradas.
- Responsabilidades de cada sistema.
- Propiedad de los datos.
- Arquitectura conceptual.
- Flujo de información.
- Capacidades de las plataformas.
- Restricciones conocidas.
- Riesgos iniciales.

---

## Plataformas Analizadas

| Plataforma | Rol |
| --- | --- |
| **Kommo CRM** | Sistema principal para la gestión comercial y de clientes. |
| **Make** | Plataforma de integración responsable de la orquestación y sincronización. |
| **Aloware** | Plataforma de telefonía encargada de la ejecución de llamadas y comunicaciones. |

---

## Hallazgos Principales

### Responsabilidades

Se definieron claramente las responsabilidades de cada plataforma para evitar superposición de funciones y establecer límites de responsabilidad durante la integración.

### Propiedad de los Datos

Se identificó el sistema propietario para cada entidad de negocio, estableciendo reglas claras de sincronización y actualización.

### Arquitectura

Se diseñó una arquitectura basada en eventos donde Make actúa como orquestador entre Kommo y Aloware mediante APIs y Webhooks.

### Flujos de Información

Se identificaron dos flujos principales:

- **Kommo → Aloware**
    - Automatización de listas de marcación.
    - Asignación de agentes.
    - Creación y actualización de contactos.
- **Aloware → Kommo**
    - Registro de llamadas.
    - Registro de SMS.
    - Notas.
    - Grabaciones.
    - Resúmenes generados por IA.

---

## Riesgos Identificados

| Riesgo | Impacto | Mitigación |
| --- | --- | --- |
| Cambios en las APIs | Alto | Documentar versiones y desacoplar la lógica mediante Make. |
| Rate Limits | Medio | Implementar reintentos y manejo de errores. |
| Mapeos incorrectos de agentes | Alto | Mantener una tabla única de equivalencias validada. |
| Duplicación de contactos | Alto | Definir un identificador único para cada contacto. |
| Errores de autenticación | Medio | Centralizar la gestión de credenciales y monitorear su vigencia. |
| Pérdida de eventos | Alto | Registrar logs y configurar mecanismos de reintento. |

---

## Decisiones Arquitectónicas

Durante la fase de descubrimiento se adoptaron las siguientes decisiones:

- Kommo será el sistema de referencia para la gestión comercial.
- Aloware será responsable exclusivamente de la ejecución de comunicaciones.
- Make actuará únicamente como capa de integración y transformación.
- La comunicación entre plataformas se realizará mediante APIs REST y Webhooks.
- La sincronización será orientada a eventos.
- La lógica de negocio permanecerá en las plataformas propietarias siempre que sea posible.

---

## Supuestos Validados

- Ambas plataformas exponen APIs suficientes para soportar la integración.
- Los eventos necesarios pueden obtenerse mediante Webhooks o consultas a la API.
- Es posible establecer una correspondencia entre usuarios de Kommo y agentes de Aloware.
- Los procesos comerciales del cliente pueden representarse mediante reglas de mapeo entre etapas y listas de marcación.

---

## Entregables Generados

- Platform Responsibilities
- Responsibility Validation
- Data Ownership Model
- Architecture Overview
- System Context
- Container Diagram
- Component Diagram
- Architectural Decisions
- Information Flow

---

## Estado del Descubrimiento

| Área | Estado |
| --- | --- |
| Comprensión del dominio | Completa |
| Responsabilidades | Definidas |
| Propiedad de los datos | Definida |
| Arquitectura conceptual | Completa |
| Flujos de información | Documentados |
| Riesgos iniciales | Identificados |
| Supuestos principales | Validados |

---

## Criterio de Finalización

La fase de descubrimiento se considera finalizada cuando:

- Existe una comprensión compartida del dominio.
- Las responsabilidades de cada plataforma están definidas.
- La arquitectura conceptual ha sido aprobada.
- Los flujos principales están documentados.
- Los riesgos conocidos han sido identificados.
- No existen supuestos críticos sin validar.

---

## Próximo Paso

Con el dominio y la arquitectura definidos, el proyecto continúa con la **Fase 1.2 – Análisis Funcional**, donde se modelarán los actores, casos de uso, eventos, reglas de negocio, dependencias y restricciones funcionales que gobernarán el comportamiento de la integración.