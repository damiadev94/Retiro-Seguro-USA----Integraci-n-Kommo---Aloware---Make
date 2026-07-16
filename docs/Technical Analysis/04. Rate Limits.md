# Rate Limits

## Objetivo

Este documento describe las restricciones de consumo (**Rate Limits**) que pueden afectar la integración entre **Kommo CRM** y **Aloware**, así como las estrategias que la solución deberá adoptar para garantizar un funcionamiento estable y confiable.

El objetivo no es documentar los valores específicos de cada plataforma, ya que éstos pueden variar con el tiempo, sino definir las consideraciones arquitectónicas que deberán respetarse durante la implementación.

---

# ¿Qué es un Rate Limit?

Un **Rate Limit** es una restricción impuesta por una API para controlar la cantidad de solicitudes que un cliente puede realizar durante un período determinado.

Cuando dicho límite se supera, la plataforma puede:

- Rechazar solicitudes.
- Retrasar respuestas.
- Bloquear temporalmente el acceso.
- Aplicar mecanismos de protección.

---

# Plataformas

| Plataforma | Puede aplicar Rate Limits |
|------------|--------------------------|
| **Kommo CRM** | Sí |
| **Aloware** | Sí |
| **Make** | Sí (según el plan y las operaciones disponibles) |

---

# Impacto en la Integración

Los límites de consumo pueden afectar:

- Sincronización de Leads.
- Consultas adicionales después de un Webhook.
- Creación o actualización de contactos.
- Registro de actividades.
- Procesamiento de grandes volúmenes de eventos.

---

# Escenarios de Riesgo

## Alta frecuencia de eventos

Un gran número de eventos generados en un corto período puede producir un volumen elevado de solicitudes hacia las APIs.

Ejemplos:

- Actualización masiva de Leads.
- Importaciones.
- Campañas de llamadas de alto volumen.

---

## Consultas consecutivas

Un único evento puede requerir múltiples consultas para completar el proceso de sincronización.

Ejemplo:

```text
Webhook recibido

↓

Consultar Lead

↓

Consultar Contacto

↓

Consultar Usuario

↓

Actualizar Aloware
```

Cada operación incrementa el consumo de la API.

---

## Procesamiento concurrente

La ejecución simultánea de múltiples escenarios puede aumentar significativamente la cantidad de solicitudes realizadas en un mismo intervalo de tiempo.

---

# Estrategias de Mitigación

La implementación deberá considerar las siguientes prácticas.

## Minimizar llamadas

Evitar consultas innecesarias reutilizando la información disponible cuando sea suficiente para completar el proceso.

---

## Priorizar Webhooks

Utilizar eventos enviados por las plataformas como mecanismo principal de activación, reduciendo el uso de consultas periódicas (*Polling*).

---

## Reintentos Controlados

Cuando una solicitud no pueda completarse debido a un límite temporal, la integración deberá reintentar la operación utilizando una política de espera adecuada.

---

## Procesamiento Idempotente

Los reintentos no deben producir efectos duplicados sobre los datos sincronizados.

---

## Manejo de Errores

Los límites alcanzados deberán registrarse para facilitar el monitoreo y el diagnóstico de incidencias.

---

# Consideraciones para Make

La implementación deberá diseñarse para optimizar el consumo de operaciones.

Buenas prácticas:

- Evitar consultas redundantes.
- Centralizar operaciones repetitivas.
- Procesar únicamente los eventos necesarios.
- Reducir llamadas consecutivas a una misma API cuando sea posible.

---

# Riesgos

| Riesgo | Consecuencia |
|---------|--------------|
| Exceso de solicitudes | Rechazo temporal de operaciones. |
| Procesamiento masivo | Retrasos en la sincronización. |
| Reintentos simultáneos | Incremento del consumo de la API. |
| Diseño ineficiente | Mayor utilización de operaciones en Make. |

---

# Recomendaciones de Diseño

La arquitectura de la integración deberá:

- Favorecer un modelo orientado a eventos.
- Reducir el número de solicitudes por flujo.
- Agrupar operaciones cuando sea posible.
- Evitar consultas repetidas sobre la misma información.
- Diseñar escenarios resilientes frente a limitaciones temporales.

---

# Fuera del Alcance

Este documento no define:

- Valores específicos de Rate Limits.
- Cuotas contratadas por cada cliente.
- Restricciones particulares de un plan comercial.

Estos aspectos deberán verificarse durante la implementación utilizando la documentación oficial de cada plataforma y la configuración disponible en el entorno del cliente.

---

# Consideraciones

- Los Rate Limits forman parte de las restricciones técnicas de las APIs y pueden cambiar sin previo aviso.
- La integración no debe asumir límites fijos ni depender de configuraciones específicas de una cuenta.
- Las estrategias de recuperación deben diseñarse para mantener la consistencia del proceso de sincronización aun cuando una API limite temporalmente el acceso.

---

# Relación con otros documentos

| Documento | Propósito |
|-----------|-----------|
| **APIs** | Describe las capacidades generales de las plataformas. |
| **Authentication** | Define cómo se autentican las solicitudes antes de consumir las APIs. |
| **Webhooks** | Reduce la necesidad de consultas periódicas mediante un modelo orientado a eventos. |
| **API Endpoints** | Documenta las operaciones que consumen cuota de las APIs. |
| **Technical Constraints** | Describe otras limitaciones técnicas que afectan la implementación. |
| **Technical Risks** | Identifica los riesgos derivados de las restricciones de consumo. |