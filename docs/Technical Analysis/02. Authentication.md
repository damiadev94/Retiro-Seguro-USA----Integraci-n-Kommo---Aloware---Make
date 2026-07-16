# Authentication

## Objetivo

Este documento describe los mecanismos de autenticación utilizados por la integración entre **Kommo CRM** y **Aloware**, definiendo cómo la plataforma de integración obtiene acceso seguro a las APIs de cada sistema.

No documenta la configuración de credenciales específicas ni valores sensibles. Su propósito es describir el modelo de autenticación requerido para implementar la integración.

---

# Resumen

| Plataforma | Método de Autenticación | Uso |
|------------|-------------------------|-----|
| **Kommo CRM** | OAuth 2.0 | Acceso a la API del CRM. |
| **Aloware** | API Token | Acceso a la API de telefonía. |
| **Make** | Conexiones Seguras | Almacenamiento y gestión de credenciales. |

---

# Principios

La autenticación de la integración debe cumplir los siguientes principios:

- Las credenciales nunca deben almacenarse dentro de los escenarios de Make.
- Cada plataforma mantiene su propio mecanismo de autenticación.
- Las credenciales deben tener únicamente los permisos necesarios para la integración.
- La renovación de credenciales debe realizarse antes de su vencimiento.
- Toda información sensible debe almacenarse de forma segura.

---

# Kommo Authentication

## Método

OAuth 2.0

## Propósito

Autorizar a la integración para acceder a los recursos del CRM en nombre de la organización.

## Capacidades requeridas

- Leer Leads.
- Leer Contactos.
- Leer Usuarios.
- Leer Pipelines.
- Actualizar Leads.
- Registrar Notas y Actividades.
- Recibir eventos mediante Webhooks.

## Consideraciones

- La autorización está asociada a una cuenta específica de Kommo.
- Los permisos dependen del usuario que autoriza la integración.
- El acceso puede requerir la renovación periódica del token.

---

# Aloware Authentication

## Método

API Token

## Propósito

Permitir que la integración consuma la API de Aloware para gestionar contactos, listas y eventos de comunicación.

## Capacidades requeridas

- Consultar Contactos.
- Crear o actualizar Contactos.
- Gestionar Listas de Marcación.
- Consultar Agentes.
- Recibir Webhooks.
- Acceder a eventos de llamadas y SMS.

## Consideraciones

- El token debe mantenerse confidencial.
- Debe limitarse a los permisos necesarios para la integración.
- La rotación del token debe realizarse de forma controlada cuando sea necesario.

---

# Make Authentication

## Rol

Make centraliza la gestión de las credenciales utilizadas para acceder a las APIs externas.

## Responsabilidades

- Almacenar credenciales de forma segura.
- Utilizar conexiones reutilizables entre escenarios.
- Evitar la exposición de información sensible en módulos o logs.

## Consideraciones

Las conexiones deben configurarse una única vez y reutilizarse en todos los escenarios de integración.

---

# Gestión de Credenciales

Las credenciales necesarias para la integración incluyen:

| Credencial | Plataforma | Finalidad |
|-------------|------------|-----------|
| OAuth Client ID | Kommo | Identificación de la aplicación. |
| OAuth Client Secret | Kommo | Autenticación de la aplicación. |
| Access Token | Kommo | Acceso a la API. |
| Refresh Token | Kommo | Renovación del Access Token. |
| API Token | Aloware | Acceso a la API de Aloware. |

Los valores concretos de estas credenciales no forman parte de la documentación y deben gestionarse mediante un repositorio seguro de secretos.

---

# Flujo General de Autenticación

## Kommo

```text
Make

↓

OAuth Authorization

↓

Access Token

↓

Kommo API
```

---

## Aloware

```text
Make

↓

API Token

↓

Aloware API
```

---

# Requisitos de Seguridad

La integración debe cumplir las siguientes prácticas:

- No almacenar credenciales en texto plano.
- No incluir tokens en logs o mensajes de error.
- Limitar los permisos al mínimo necesario.
- Proteger las credenciales frente a accesos no autorizados.
- Revisar periódicamente la vigencia de las credenciales.

---

# Riesgos

| Riesgo | Impacto |
|---------|---------|
| Expiración de Access Token | Interrupción temporal de la integración. |
| Revocación de permisos | Pérdida de acceso a la API. |
| Exposición de credenciales | Riesgo de acceso no autorizado. |
| Rotación no controlada de credenciales | Fallos de autenticación en los escenarios de Make. |

---

# Consideraciones

- La autenticación es un requisito previo para cualquier interacción con las APIs.
- Cada plataforma mantiene su propio mecanismo de autorización.
- La implementación deberá contemplar la renovación y validación de credenciales antes de ejecutar operaciones críticas.
- La configuración específica de las conexiones se documentará durante la fase **Environment Preparation**.

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **APIs** | Describe las capacidades generales de cada API. |
| **Webhooks** | Documenta los mecanismos de recepción de eventos. |
| **Rate Limits** | Describe las restricciones de consumo de las APIs. |
| **API Objects** | Define las entidades disponibles a través de las APIs. |
| **API Endpoints** | Documenta las operaciones utilizadas por la integración. |
| **Environment Preparation** | Describe la configuración práctica de las credenciales y conexiones en Make. |