# 01. Container Diagram

---

## Objetivo

Describir la arquitectura de contenedores de la solución de integración entre Kommo CRM y Aloware.

Este documento corresponde al **Nivel 2 del modelo C4 (Container Diagram)** y muestra cómo está compuesta la solución desde una perspectiva lógica, identificando los principales contenedores y sus responsabilidades.

No describe componentes internos ni detalles de implementación.

---

# Arquitectura de Contenedores

La solución está compuesta por tres contenedores principales:

- Kommo CRM
- Plataforma de Integración
- Aloware

Cada contenedor posee una responsabilidad claramente definida y se comunica únicamente a través de la Plataforma de Integración.

---

# Diagrama de Contenedores

```
                 ┌──────────────────────┐
                 │      Kommo CRM       │
                 │  Gestión Comercial   │
                 └──────────┬───────────┘
                            │
                 Eventos y consultas
                            │
                            ▼
      ┌────────────────────────────────────────────┐
      │      Plataforma de Integración             │
      │      (Implementada mediante Make)          │
      │                                            │
      │ • Orquestación                             │
      │ • Reglas de negocio                        │
      │ • Transformación de datos                  │
      │ • Sincronización                           │
      │ • Logging                                 │
      │ • Manejo de errores                        │
      └──────────────┬─────────────────────────────┘
                     │
          Sincronización bidireccional
                     │
                     ▼
             ┌──────────────────────┐
             │       Aloware        │
             │    Comunicaciones    │
             └──────────────────────┘
```

---

# Contenedores

## Kommo CRM

**Tipo:** Sistema Externo

### Responsabilidad

Gestionar el proceso comercial.

### Funciones

- Leads
- Contactos
- Empresas
- Pipelines
- Etapas
- Usuarios
- Historial comercial

### Source of Truth

Información comercial.

---

## Plataforma de Integración

**Tipo:** Aplicación de Integración

**Implementación:** Make

### Responsabilidad

Coordinar la comunicación entre Kommo y Aloware.

### Funciones

- Recepción de eventos.
- Aplicación de reglas de negocio.
- Transformación de datos.
- Sincronización.
- Logging técnico.
- Manejo de errores.

### Source of Truth

No posee información de negocio.

Solo administra información técnica necesaria para la integración.

---

## Aloware

**Tipo:** Sistema Externo

### Responsabilidad

Gestionar todas las comunicaciones con los contactos.

### Funciones

- Agentes.
- Líneas telefónicas.
- Secuencias de marcación.
- Llamadas.
- SMS.
- Grabaciones.
- Voicemails.
- AloAI.

### Source of Truth

Información relacionada con comunicaciones.

---

# Relaciones entre Contenedores

| Origen | Destino | Propósito |
| --- | --- | --- |
| Kommo CRM | Plataforma de Integración | Publicación de eventos comerciales y consulta de datos. |
| Plataforma de Integración | Kommo CRM | Actualización del historial comercial. |
| Plataforma de Integración | Aloware | Sincronización de contactos y ejecución de automatizaciones. |
| Aloware | Plataforma de Integración | Publicación de eventos de comunicación. |

---

# Responsabilidades

| Contenedor | Responsabilidad Principal |
| --- | --- |
| Kommo CRM | Gestión Comercial |
| Plataforma de Integración | Orquestación y Sincronización |
| Aloware | Comunicaciones |

---

# Principios

- Cada contenedor posee una responsabilidad única.
- Kommo y Aloware no se comunican directamente.
- Toda comunicación pasa por la Plataforma de Integración.
- Cada contenedor mantiene su propio Source of Truth.
- La Plataforma de Integración no almacena información permanente del negocio.

---

# Referencias

- Architecture Overview
- System Context
- Data Ownership Model
- Component Diagram
- Architectural Decisions

---

## Estado

**Versión:** 1.0

**Estado:** Aprobado

**Fase:** 1.1 – Comprensión del Dominio