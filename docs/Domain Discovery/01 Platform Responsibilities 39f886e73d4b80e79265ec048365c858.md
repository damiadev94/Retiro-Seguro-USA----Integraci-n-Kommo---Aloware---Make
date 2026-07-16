# 01. Platform Responsibilities

## Objetivo

Definir las responsabilidades de cada plataforma participante en la integración y establecer una separación clara entre los dominios funcionales del sistema.

Este documento constituye la base conceptual sobre la cual se construye la arquitectura de integración.

---

# Descripción

La solución está compuesta por tres plataformas independientes, cada una especializada en un dominio específico.

La arquitectura adopta el principio de **Responsabilidad Única**, donde cada plataforma administra exclusivamente las funciones para las cuales fue diseñada.

Ninguna plataforma reemplaza las responsabilidades de otra.

---

# Plataformas

## Kommo CRM

### Dominio

Gestión Comercial

### Responsabilidad

Administrar el proceso comercial y mantener la información del cliente.

### Funciones

- Gestión de Leads.
- Gestión de Contactos.
- Gestión de Empresas.
- Gestión de Pipelines.
- Gestión de Etapas (Status).
- Gestión de Usuarios Responsables.
- Historial comercial.
- Disparador de procesos comerciales.

### No es responsable de

- Telefonía.
- SMS.
- Grabaciones.
- Marcación automática.
- Resúmenes de IA.

---

## Plataforma de Integración

**Implementación actual:** Make

### Dominio

Integración y Orquestación

### Responsabilidad

Coordinar la comunicación entre Kommo y Aloware mediante la aplicación de reglas de negocio y sincronización de datos.

### Funciones

- Recibir eventos.
- Aplicar reglas de negocio.
- Transformar datos.
- Sincronizar plataformas.
- Resolver mapeos.
- Gestionar errores.
- Registrar logs técnicos.

### No es responsable de

- Administrar información comercial.
- Administrar comunicaciones.
- Almacenar información permanente del negocio.

---

## Aloware

### Dominio

Comunicaciones

### Responsabilidad

Ejecutar todas las interacciones telefónicas con los contactos.

### Funciones

- Gestión de Agentes.
- Gestión de Líneas Telefónicas.
- Gestión de Secuencias de Marcación.
- Llamadas.
- SMS.
- Grabaciones.
- Voicemails.
- Resúmenes generados mediante AloAI.

### No es responsable de

- Gestión del Pipeline comercial.
- Gestión de Leads.
- Gestión del CRM.

---

# Matriz de Responsabilidades

| Funcionalidad | Kommo | Integración | Aloware |
| --- | --- | --- | --- |
| Gestión de Leads | ✅ | ❌ | ❌ |
| Gestión de Contactos | ✅ | ❌ | ❌ |
| Gestión de Empresas | ✅ | ❌ | ❌ |
| Gestión de Pipelines | ✅ | ❌ | ❌ |
| Gestión de Etapas | ✅ | ❌ | ❌ |
| Gestión de Usuarios Responsables | ✅ | ❌ | ❌ |
| Reglas de Integración | ❌ | ✅ | ❌ |
| Transformación de Datos | ❌ | ✅ | ❌ |
| Sincronización | ❌ | ✅ | ❌ |
| Mapeos | ❌ | ✅ | ❌ |
| Logging Técnico | ❌ | ✅ | ❌ |
| Manejo de Errores | ❌ | ✅ | ❌ |
| Gestión de Agentes | ❌ | ❌ | ✅ |
| Gestión de Líneas | ❌ | ❌ | ✅ |
| Secuencias de Marcación | ❌ | ❌ | ✅ |
| Llamadas | ❌ | ❌ | ✅ |
| SMS | ❌ | ❌ | ✅ |
| Grabaciones | ❌ | ❌ | ✅ |
| Voicemails | ❌ | ❌ | ✅ |
| Resúmenes IA | ❌ | ❌ | ✅ |

---

# Principios Arquitectónicos

La arquitectura se basa en los siguientes principios:

- Cada plataforma posee una responsabilidad única.
- Cada entidad tiene un único **Source of Truth**.
- La Plataforma de Integración actúa únicamente como orquestador.
- Kommo y Aloware no se comunican directamente.
- Toda sincronización se realiza a través de la Plataforma de Integración.
- La arquitectura debe permanecer independiente de la tecnología utilizada para implementar la integración.

---

# Resumen

| Plataforma | Rol Principal |
| --- | --- |
| Kommo | Gestión Comercial (CRM) |
| Plataforma de Integración | Orquestación y Sincronización |
| Aloware | Comunicaciones |

---

# Referencias

- Responsibilities Validation
- Data Ownership Model
- Architecture Overview
- System Context

---

## Estado

**Versión:** 1.0

**Estado:** Aprobado

**Fase:** 1.1 – Comprensión del Dominio