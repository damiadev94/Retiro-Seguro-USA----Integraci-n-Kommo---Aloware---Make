# 05. System Context

---

## Objetivo

Definir el contexto de la solución de integración, identificando los actores, plataformas y relaciones principales entre ellos.

Este documento corresponde al **Nivel 1 del modelo C4 (System Context)**.

Su propósito es mostrar los límites del sistema y cómo interactúa con su entorno, sin describir detalles internos de implementación.

---

# Sistema Bajo Diseño

El sistema corresponde a una **Plataforma de Integración**, implementada mediante Make, cuya función es conectar **Kommo CRM** y **Aloware** para sincronizar información comercial y operativa de forma bidireccional.

La plataforma actúa como intermediario entre ambos sistemas, manteniendo separadas sus responsabilidades y garantizando la consistencia de los datos.

---

# Actores

## Usuario Comercial

Opera diariamente sobre Kommo CRM.

### Responsabilidades

- Gestionar Leads.
- Gestionar Contactos.
- Actualizar el Pipeline.
- Consultar el historial comercial.

---

## Agente Telefónico

Opera diariamente sobre Aloware.

### Responsabilidades

- Realizar llamadas.
- Enviar y recibir SMS.
- Gestionar comunicaciones.

---

## Administrador de la Integración

Responsable de mantener la solución operativa.

### Responsabilidades

- Configurar la integración.
- Gestionar credenciales.
- Administrar mapeos.
- Monitorear sincronizaciones.
- Resolver incidencias.

---

# Sistemas

## Kommo CRM

Sistema responsable de la gestión comercial.

Administra:

- Leads
- Contactos
- Empresas
- Pipelines
- Etapas
- Usuarios
- Historial comercial

---

## Plataforma de Integración

Implementada mediante Make.

Responsable de:

- Orquestación.
- Sincronización.
- Reglas de negocio.
- Transformación de datos.
- Logging técnico.
- Manejo de errores.

---

## Aloware

Sistema responsable de las comunicaciones.

Administra:

- Agentes.
- Líneas telefónicas.
- Secuencias de marcación.
- Llamadas.
- SMS.
- Grabaciones.
- Voicemails.
- AloAI.

---

# Relaciones

## Actores ↔ Sistemas

| Origen | Destino | Relación |
| --- | --- | --- |
| Usuario Comercial | Kommo CRM | Gestiona el proceso comercial. |
| Agente Telefónico | Aloware | Ejecuta comunicaciones. |
| Administrador | Plataforma de Integración | Configura y monitorea la solución. |

---

## Sistemas ↔ Sistemas

| Origen | Destino | Relación |
| --- | --- | --- |
| Kommo CRM | Plataforma de Integración | Envía eventos comerciales. |
| Plataforma de Integración | Kommo CRM | Actualiza información comercial. |
| Plataforma de Integración | Aloware | Sincroniza contactos y ejecuta automatizaciones. |
| Aloware | Plataforma de Integración | Envía eventos de comunicación. |

---

# Diagrama de Contexto

```
                 ┌───────────────────────────┐
                 │   Usuario Comercial       │
                 └─────────────┬─────────────┘
                               │
                               ▼
                     ┌──────────────────┐
                     │    Kommo CRM     │
                     └────────┬─────────┘
                              │
                    Eventos comerciales
                              │
                              ▼
      ┌──────────────────────────────────────────────┐
      │        Plataforma de Integración             │
      │          (Implementada con Make)             │
      └──────────────┬───────────────────────────────┘
                     │
           Sincronización bidireccional
                     │
                     ▼
              ┌──────────────────┐
              │     Aloware      │
              └────────┬─────────┘
                       │
                       ▼
             ┌────────────────────┐
             │ Agente Telefónico  │
             └────────────────────┘

                    ▲
                    │
        Configuración y monitoreo
                    │
        ┌──────────────────────────┐
        │ Administrador Integración│
        └──────────────────────────┘
```

---

# Límites del Sistema

| Dominio | Plataforma | Responsabilidad |
| --- | --- | --- |
| Comercial | Kommo CRM | Gestión del proceso comercial. |
| Integración | Plataforma de Integración | Orquestación y sincronización. |
| Comunicaciones | Aloware | Gestión de llamadas y mensajería. |

Cada dominio mantiene un único **Source of Truth** para las entidades bajo su responsabilidad.

---

# Principios

- Los usuarios trabajan únicamente sobre la plataforma correspondiente a su función.
- Kommo y Aloware nunca se comunican directamente.
- Toda interacción pasa por la Plataforma de Integración.
- Cada plataforma conserva la propiedad de sus datos.
- La Plataforma de Integración únicamente coordina la sincronización.

---

# Referencias

- Platform Responsibilities
- Responsibilities Validation
- Data Ownership Model
- Architecture Overview
- Container Diagram
- Component Diagram

---

## Estado

**Versión:** 1.0

**Estado:** Aprobado

**Fase:** 1.1 – Comprensión del Dominio