# 04. Architecture Overview

---

## Objetivo

Presentar una visión general de la arquitectura de la integración entre Kommo CRM y Aloware mediante una Plataforma de Integración implementada con Make.

Este documento describe la estructura de la solución, los sistemas participantes, sus responsabilidades y los principios arquitectónicos que gobiernan la integración.

No incluye detalles de implementación, APIs, Webhooks ni configuraciones específicas.

---

# Descripción

La solución conecta dos plataformas especializadas mediante una capa de integración que coordina el intercambio de información.

Cada plataforma mantiene un dominio funcional claramente definido y un único **Source of Truth** para las entidades bajo su responsabilidad.

La Plataforma de Integración actúa como intermediario, aplicando reglas de negocio, transformando datos y sincronizando información entre ambos sistemas.

---

# Arquitectura General

```
                    Usuario Comercial
                           │
                           ▼
                    ┌──────────────┐
                    │  Kommo CRM   │
                    └──────┬───────┘
                           │
                Eventos comerciales
                           │
                           ▼
        ┌────────────────────────────────┐
        │   Plataforma de Integración    │
        │     (Implementada con Make)    │
        └──────────────┬─────────────────┘
                       │
          Sincronización y reglas de negocio
                       │
                       ▼
                 ┌──────────────┐
                 │   Aloware    │
                 └──────┬───────┘
                        │
        Llamadas • SMS • IA • Eventos
                        │
                        ▼
        ┌────────────────────────────────┐
        │   Plataforma de Integración    │
        └──────────────┬─────────────────┘
                       │
                       ▼
                  Actualización
                    de Kommo
```

---

# Plataformas

## Kommo CRM

### Dominio

Gestión Comercial

### Responsabilidad

Administrar el proceso comercial y actuar como Source of Truth de toda la información relacionada con clientes y oportunidades.

---

## Plataforma de Integración

### Dominio

Integración y Orquestación

### Implementación

Make

### Responsabilidad

Coordinar la comunicación entre Kommo y Aloware mediante:

- Recepción de eventos.
- Aplicación de reglas de negocio.
- Transformación de datos.
- Sincronización.
- Manejo de errores.
- Registro técnico.

No administra información permanente del negocio.

---

## Aloware

### Dominio

Comunicaciones

### Responsabilidad

Ejecutar todas las interacciones telefónicas con los contactos.

Administra:

- Llamadas.
- SMS.
- Grabaciones.
- Voicemails.
- Resúmenes AloAI.
- Agentes.
- Líneas telefónicas.
- Secuencias de marcación.

---

# Principios Arquitectónicos

La arquitectura se basa en los siguientes principios.

## Responsabilidad Única

Cada plataforma mantiene una responsabilidad claramente definida.

---

## Single Source of Truth

Cada entidad posee un único sistema propietario.

---

## Integración Desacoplada

Kommo y Aloware nunca se comunican directamente.

Toda interacción pasa por la Plataforma de Integración.

---

## Orquestación Centralizada

Las reglas de negocio y transformaciones residen exclusivamente en la Plataforma de Integración.

---

## Arquitectura Dirigida por Eventos

La sincronización utiliza preferentemente eventos generados por las plataformas para mantener la consistencia de la información.

---

## Independencia Tecnológica

La arquitectura conceptual no depende de Make.

La Plataforma de Integración podría implementarse con otra tecnología sin modificar el diseño arquitectónico.

---

# Dominios

| Dominio | Plataforma | Responsabilidad |
| --- | --- | --- |
| Comercial | Kommo CRM | Gestión del proceso comercial |
| Integración | Plataforma de Integración | Orquestación y sincronización |
| Comunicaciones | Aloware | Gestión de llamadas y mensajería |

---

# Alcance

La arquitectura contempla los siguientes procesos:

- Sincronización de Leads y Contactos hacia Aloware.
- Asignación de contactos a secuencias de marcación.
- Sincronización de llamadas.
- Sincronización de SMS.
- Registro de grabaciones.
- Registro de voicemails.
- Registro de resúmenes generados por IA.
- Aplicación de reglas de negocio durante la sincronización.

---

# Fuera del Alcance

Este documento no describe:

- APIs REST.
- OAuth.
- Webhooks.
- Endpoints.
- Payloads.
- Escenarios de Make.
- Field Mapping.
- Configuración técnica.
- Manejo detallado de errores.

Estos aspectos serán desarrollados en las fases de Diseño Técnico e Implementación.

---

# Referencias

- Platform Responsibilities
- Responsibilities Validation
- Data Ownership Model
- System Context
- Container Diagram
- Component Diagram
- Architectural Decisions

---

## Estado

**Versión:** 1.0

**Estado:** Aprobado

**Fase:** 1.1 – Comprensión del Dominio