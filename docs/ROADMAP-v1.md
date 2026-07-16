# ROADMAP

---

# Fase 1 — Descubrimiento y Análisis

**Objetivo:** Comprender completamente el dominio, las plataformas y los requisitos antes de diseñar la solución técnica.

---

# 1.1 Comprensión del Dominio

**Objetivo:** Entender el rol de cada plataforma y definir el modelo conceptual de la integración.

### 1.1.1 Definir responsabilidades de las plataformas

- ~~Roles de Kommo, Make y Aloware.~~
- ~~Responsabilidades.~~
- ~~Principios arquitectónicos.~~

**Entregables**

- **Platform Responsibilities.**
- **Responsibility Matrix.**
- **Architecture Principles.**

---

### 1.1.2 Validar responsabilidades

- ~~Contrastar con la documentación oficial.~~
- ~~Registrar hallazgos.~~

**Entregables**

- **Validation Report.**
- **Functional Capabilities Matrix.**
- **Findings.**

---

### 1.1.3 Definir el modelo de propiedad de datos

- ~~Catálogo de entidades.~~
- ~~Source of Truth.~~
- ~~Lifecycle.~~
- ~~Ownership Rules.~~

**Entregables**

- **Data Ownership Model.**

---

### 1.1.4 Arquitectura conceptual de alto nivel

- ~~Context Diagram.~~
- ~~Container Diagram.~~
- ~~Architecture Overview.~~

**Entregables**

- **High-Level Architecture.**

---

### 1.1.5 Flujos de información

- Flujo Kommo → Aloware.
- Flujo Aloware → Kommo.
- Data Flow.
- Sequence Diagrams.

**Entregables**

- Information Flow.

---

### 1.1.6 Cierre del dominio

- Validación completa.
- Riesgos.
- Decisiones.

**Entregables**

- Discovery Report.

---

# 1.2 Análisis Funcional

Ahora sí empezamos a estudiar **cómo debe comportarse la integración**.

Aquí responderemos preguntas como:

- ¿Qué quiere lograr el cliente?
- ¿Qué casos de uso existen?
- ¿Qué eventos disparan automatizaciones?
- ¿Qué reglas de negocio existen?
- ¿Qué excepciones existen?
- ¿Qué escenarios deben soportarse?

## Tareas

### 1.2.1 Actores

Cliente

CRM

Agentes

Make

Administrador

---

### 1.2.2 Casos de uso

Mover Lead

Registrar llamada

Enviar SMS

Crear contacto

Etc.

---

### 1.2.3 Eventos

Lead cambia de etapa

Llamada finaliza

SMS recibido

AI Summary generado

Etc.

---

### 1.2.4 Reglas de negocio

Aquí desarrollaremos completamente la sección que en tu planificación aparecía como "Definir reglas de negocio".

---

### 1.2.5 Dependencias funcionales

Qué necesita cada flujo para funcionar.

---

### 1.2.6 Restricciones funcionales

Limitaciones del negocio.

---

# 1.3 Análisis Técnico

Aquí recién entramos en las APIs.

## 1.3.1 APIs

Kommo

Aloware

---

## 1.3.2 OAuth

---

## 1.3.3 Webhooks

---

## 1.3.4 Rate Limits

---

## 1.3.5 Objetos API

Endpoints

Payloads

IDs

---

## 1.3.6 Limitaciones técnicas

---

# 1.4 Cierre del Descubrimiento

Antes de pasar al diseño técnico verificaremos que tenemos todo.

## Checklist

### Dominio

- ☐ Entidades.
- ☐ Ownership.
- ☐ Arquitectura.
- ☐ Flujos.

### Funcional

- ☐ Casos de uso.
- ☐ Reglas.
- ☐ Eventos.
- ☐ Restricciones.

### Técnico

- ☐ APIs.
- ☐ OAuth.
- ☐ Webhooks.
- ☐ Rate Limits.
- ☐ Objetos.

### Riesgos

- ☐ Riesgos documentados.
- ☐ Decisiones tomadas.
- ☐ Supuestos eliminados.

---

# Fase 2 — Diseño Técnico

**Objetivo:** Diseñar completamente la integración antes de implementarla.

## Tarea 2.1 — Diseñar el mapeo de etapas → listas

Crear la matriz de correspondencias.

Ejemplo:

| Etapa Kommo | Lista Aloware |
| --- | --- |
| No Contactado | Seguimiento 48h |
| Seguimiento 30 días | Follow Up 30 |
| Reactivación | Reactivation |

**Entregable**

- Matriz de mapeo.

---

## Tarea 2.2 — Diseñar el mapeo de usuarios

Definir la relación:

```
Kommo Responsible User

↓

Aloware Agent
```

Incluir:

- IDs
- Emails
- Casos sin correspondencia

**Entregable**

- Tabla de equivalencias.

---

## Tarea 2.3 — Diseñar el modelo de sincronización

Definir:

- Campos enviados
- Campos recibidos
- Transformaciones
- Campos obligatorios
- Campos opcionales

**Entregable**

- Documento de Field Mapping.

---

## Tarea 2.4 — Diseñar manejo de errores

Definir estrategia para:

- API caída
- Timeout
- Error OAuth
- Error 429
- Contacto inexistente
- Lead eliminado
- Error en Make

**Entregable**

- Documento de Error Handling.

---

# Fase 3 — Preparación del Entorno

**Objetivo:** Dejar todos los sistemas listos para comenzar la implementación.

## Tarea 3.1 — Configurar Kommo

- OAuth
- Webhooks
- Permisos
- Usuarios

---

## Tarea 3.2 — Configurar Aloware

- API Token
- Webhooks
- Eventos
- Agentes

---

## Tarea 3.3 — Configurar Make

- Conexiones
- Variables
- Carpetas
- Convenciones de nombres

---

## Tarea 3.4 — Validar conectividad

Comprobar:

- Autenticación
- Acceso APIs
- Recepción Webhooks

---

## Fase 4 — Implementación del Flujo Kommo → Aloware

**Objetivo:** Automatizar el envío de leads al Dialer.

### Tarea 4.1 — Crear escenario de Make

---

### Tarea 4.2 — Detectar cambios de etapa

Configurar:

- Webhook
- Filtro de etapas

---

### Tarea 4.3 — Obtener información del lead

Recuperar:

- Contacto
- Responsable
- Teléfono
- Datos necesarios

---

### Tarea 4.4 — Resolver agente correspondiente

Aplicar el mapeo:

```
Responsible User

↓

Agent
```

---

### Tarea 4.5 — Crear o actualizar contacto

Implementar lógica:

```
Existe

↓

Actualizar

No existe

↓

Crear
```

---

### Tarea 4.6 — Asignar lista de marcación

Enviar al Power Dialer correcto.

---

### Tarea 4.7 — Registrar logs

Guardar:

- Fecha
- Resultado
- Errores
- IDs

---

## Fase 5 — Implementación del Flujo Aloware → Kommo

**Objetivo:** Registrar automáticamente toda la actividad de comunicación.

### Tarea 5.1 — Crear escenario receptor

Recibir Webhooks.

---

### Tarea 5.2 — Procesar eventos

Aceptar:

- Call
- SMS
- Voicemail
- Note

---

### Tarea 5.3 — Buscar Lead correspondiente

Utilizar:

- Phone Number
- Contact ID
- Mapping

---

### Tarea 5.4 — Registrar notas en Kommo

Agregar:

- Tipo
- Fecha
- Agente
- Notas
- Estado

---

### Tarea 5.5 — Adjuntar grabaciones

Guardar URL.

---

### Tarea 5.6 — Adjuntar resumen AloAI

Registrar resumen generado.

---

### Tarea 5.7 — Sincronizar SMS

Registrar:

- Entrantes
- Salientes

---

### Tarea 5.8 — Registrar errores

Guardar fallos de sincronización.

---

## Fase 6 — Validaciones Técnicas

**Objetivo:** Verificar el correcto funcionamiento de la integración.

### Tarea 6.1 — Validar flujo Kommo → Aloware

Comprobar:

- Cambio de etapa
- Creación
- Actualización
- Lista correcta
- Agente correcto

---

### Tarea 6.2 — Validar flujo Aloware → Kommo

Comprobar:

- Llamadas
- SMS
- Notas
- Grabaciones
- IA

---

### Tarea 6.3 — Validar escenarios de error

Probar:

- Contacto inexistente
- Usuario inexistente
- API caída
- Timeout
- Datos incompletos

---

### Tarea 6.4 — Validar duplicados

Verificar que no existan registros duplicados.

---

### Tarea 6.5 — Validar rendimiento

Evaluar:

- Tiempo de sincronización
- Reintentos
- Consumo de operaciones en Make

---

## Fase 7 — Documentación

**Objetivo:** Facilitar el mantenimiento y la operación futura.

### Tarea 7.1 — Documentar arquitectura

---

### Tarea 7.2 — Documentar escenarios de Make

---

### Tarea 7.3 — Documentar mapeos

---

### Tarea 7.4 — Documentar configuración

---

### Tarea 7.5 — Elaborar guía operativa

Incluir:

- Cómo agregar nuevos agentes.
- Cómo agregar nuevas listas.
- Cómo modificar etapas.
- Cómo regenerar credenciales.
- Procedimiento ante errores comunes.

---

## Fase 8 — Entrega

**Objetivo:** Poner la solución en producción.

### Tarea 8.1 — Implementar en ambiente productivo

---

### Tarea 8.2 — Ejecutar pruebas finales

---

### Tarea 8.3 — Capacitar al cliente

Explicar:

- Funcionamiento.
- Limitaciones.
- Mantenimiento.

---

### Tarea 8.4 — Entregar documentación

---

## Fase 9 — Soporte Post Implementación

**Objetivo:** Ajustar el sistema durante el período acordado.

### Tarea 9.1 — Monitorear sincronizaciones

---

### Tarea 9.2 — Corregir incidencias

---

### Tarea 9.3 — Ajustar reglas de negocio

---

### Tarea 9.4 — Cerrar implementación

Emitir informe final con:

- Integraciones implementadas.
- Casos validados.
- Incidencias resueltas.
- Recomendaciones de mantenimiento.

---

# Dependencias principales

| Dependencia | Requiere |
| --- | --- |
| Diseño técnico | Descubrimiento completado |
| Preparación del entorno | Diseño técnico aprobado |
| Flujo Kommo → Aloware | APIs configuradas y mapeos definidos |
| Flujo Aloware → Kommo | Webhooks y autenticación operativos |
| Validaciones | Ambos flujos implementados |
| Documentación | Implementación estabilizada |
| Producción | Validaciones completadas |
| Soporte | Despliegue en producción |

# Riesgos identificados

| Riesgo | Mitigación |
| --- | --- |
| Cambios en APIs | Documentar versiones y aislar llamadas en Make |
| Rate limits | Implementar reintentos y manejo de errores |
| Mapeos incorrectos de agentes | Mantener una tabla única de equivalencias y validarla antes del despliegue |
| Duplicación de contactos | Definir una clave única (teléfono, ID externo u otro identificador consistente) |
| Fallos de autenticación | Monitorear expiración de credenciales y centralizar su renovación |
| Pérdida de eventos | Registrar logs y configurar reintentos automáticos en Make |

# Hitos del proyecto

1. Arquitectura y reglas de negocio definidas.
2. Mapeos técnicos aprobados.
3. Entornos y conexiones configurados.
4. Flujo Kommo → Aloware operativo.
5. Flujo Aloware → Kommo operativo.
6. Validación integral completada.
7. Documentación entregada.
8. Despliegue en producción.
9. Cierre del período de soporte.