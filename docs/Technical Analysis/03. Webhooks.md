# Webhooks

## Objetivo

Este documento describe el uso de **Webhooks** dentro de la integración entre **Kommo CRM** y **Aloware**, definiendo cómo los eventos generados por ambas plataformas son recibidos y procesados por **Make**.

Los Webhooks constituyen el mecanismo principal para implementar una arquitectura orientada a eventos, permitiendo que la integración responda automáticamente a los cambios ocurridos en cada sistema.

No se documentan aquí los payloads específicos ni la configuración técnica de los endpoints, ya que esos aspectos se desarrollarán durante la implementación.

---

# ¿Qué es un Webhook?

Un Webhook es un mecanismo mediante el cual una plataforma envía automáticamente una notificación HTTP cuando ocurre un evento determinado.

En lugar de consultar periódicamente una API (Polling), la plataforma emisora informa inmediatamente a la integración cuando sucede un cambio relevante.

---

# Rol dentro de la Arquitectura

```text
            Evento

      Kommo / Aloware
             │
             ▼
      HTTP Webhook Request
             │
             ▼
            Make
             │
     Validación y Procesamiento
             │
             ▼
      API de destino
```

Los Webhooks representan el punto de entrada de los flujos de integración.

---

# Arquitectura General

| Plataforma | Función |
|------------|---------|
| **Kommo** | Emite eventos relacionados con la actividad comercial. |
| **Aloware** | Emite eventos relacionados con llamadas y comunicaciones. |
| **Make** | Recibe, valida y procesa todos los Webhooks. |

---

# Webhooks de Kommo

## Propósito

Notificar a la integración cuando ocurre un cambio relevante dentro del CRM.

## Eventos utilizados

- Cambio de etapa del Lead.
- Actualización de Lead.
- Actualización de Contacto.

## Objetivo

Permitir que la integración sincronice automáticamente la información necesaria hacia Aloware.

---

# Webhooks de Aloware

## Propósito

Notificar automáticamente los eventos generados durante la comunicación con los clientes.

## Eventos utilizados

- Llamada finalizada.
- SMS enviado.
- SMS recibido.
- Nota creada.
- Grabación disponible.
- Resumen generado por IA.

## Objetivo

Registrar automáticamente la actividad correspondiente dentro de Kommo.

---

# Flujo General

## Kommo → Make

```text
Lead cambia de etapa

↓

Kommo genera Webhook

↓

Make recibe el evento

↓

Validación

↓

Sincronización hacia Aloware
```

---

## Aloware → Make

```text
Llamada finalizada

↓

Aloware genera Webhook

↓

Make recibe el evento

↓

Validación

↓

Registro en Kommo
```

---

# Procesamiento de Eventos

Una vez recibido un Webhook, la integración debe ejecutar las siguientes etapas:

1. Recepción del evento.
2. Validación del origen.
3. Identificación del tipo de evento.
4. Validación de reglas de negocio.
5. Obtención de información adicional cuando sea necesaria.
6. Transformación de datos.
7. Ejecución del flujo correspondiente.
8. Registro del resultado.

---

# Requisitos Funcionales

Todo Webhook recibido debe cumplir las siguientes condiciones:

- Corresponder a un evento soportado por la integración.
- Contener la información mínima necesaria para su procesamiento.
- Poder asociarse con una entidad existente.
- Generar una única ejecución del flujo correspondiente.

---

# Seguridad

Los Webhooks deben procesarse únicamente cuando provengan de fuentes confiables.

La implementación deberá contemplar mecanismos para:

- Validar el origen del evento.
- Proteger el endpoint receptor.
- Evitar solicitudes no autorizadas.
- Rechazar eventos inválidos o malformados.

La estrategia específica de validación dependerá de las capacidades ofrecidas por cada plataforma.

---

# Confiabilidad

La integración debe considerar que un Webhook puede:

- Llegar más de una vez.
- Llegar fuera de orden.
- No llegar debido a fallos temporales.
- Contener información parcial.

Por este motivo, el procesamiento debe ser:

- Idempotente.
- Tolerante a duplicados.
- Resistente a fallos.
- Capaz de registrar errores para su posterior análisis.

---

# Consideraciones

- Los Webhooks constituyen el mecanismo principal de activación de la integración.
- No toda la información necesaria estará presente en el evento recibido; en algunos casos será necesario consultar la API correspondiente.
- Los Webhooks no reemplazan las validaciones de negocio.
- La lógica de procesamiento debe permanecer desacoplada del mecanismo de recepción del evento.

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **APIs** | Describe las capacidades generales de las APIs utilizadas. |
| **Authentication** | Define cómo se autentican las plataformas antes de consumir las APIs. |
| **Rate Limits** | Documenta las limitaciones de consumo que afectan el procesamiento posterior de los Webhooks. |
| **API Objects** | Describe las entidades referenciadas por los eventos recibidos. |
| **API Endpoints** | Documenta los endpoints utilizados para consultar información adicional tras recibir un Webhook. |
| **Domain Events** | Define los eventos de negocio representados por los Webhooks. |
| **Information Flow** | Describe cómo los eventos recorren la arquitectura de integración. |