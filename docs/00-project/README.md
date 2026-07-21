README - Convenciones de documentación

Este README resume las convenciones establecidas para la documentación del proyecto.

Principios:
- Estructura numerada y secuencial para seguir el flujo de lectura del proyecto.
- Nombres de carpetas y archivos: kebab-case exclusivamente.
- Archivos fuente: .md (Markdown). PDFs y diagramas se almacenan en docs/12-assets/.
- Escenarios de implementación en docs/08-implementation/scenarios/ con prefijo sXX-.
- Documentos temporales y duplicados se mueven a docs/99-archive/. No se eliminan sin aprobación.

Flujo para cambios grandes en docs:
1. Crear una rama feature/docs/xxx
2. Ejecutar renombres con git mv para preservar historial
3. Actualizar enlaces relativos dentro de los MD
4. Crear PR y pedir revisión de al menos un reviewer

Contacto y mantenimiento:
- Mantener este README actualizado con cambios en convenciones.
