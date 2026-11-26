# AGENTS.md — Instrucciones para agentes de ProjectVTT

## 1. Misión

Trabaja como parte de un equipo de ingeniería que construye ProjectVTT. Tu prioridad es entregar cambios pequeños, correctos, comprobables y fáciles de mantener. No optimices para producir mucho código; optimiza para producir software que funcione y pueda evolucionar.

## 2. Antes de modificar código

1. Lee `README.md`, `PROJECT_SPEC.md`, `ARCHITECTURE.md`, `ROADMAP.md`, `BACKLOG.md` y `DECISIONS.md` cuando estén disponibles.
2. Inspecciona el estado real del repositorio. No presupongas que la estructura o las dependencias descritas ya existen.
3. Identifica el módulo y los contratos afectados.
4. Comprueba si existe una decisión arquitectónica que gobierne el cambio.
5. Si falta una decisión esencial, detente y pregunta al coordinador/propietario o registra la cuestión como pendiente. No inventes una decisión irreversible.

## 3. Reglas obligatorias

- No cambies contratos compartidos sin coordinarlo con los demás componentes.
- No dupliques reglas de negocio en web, escritorio y backend.
- El servidor valida permisos, reglas y cambios de estado compartido.
- No confíes en validaciones hechas únicamente en el cliente.
- No introduzcas microservicios para el MVP.
- No añadas dependencias sin explicar por qué son necesarias.
- No actualices versiones principales de dependencias sin autorización.
- No guardes secretos, tokens, claves ni credenciales en el repositorio.
- No ejecutes código arbitrario de plugins de terceros en el backend.
- No borres ni sobrescribas trabajo ajeno.
- No reformatees archivos completos si el cambio no lo requiere.
- No afirmes que una prueba ha pasado si no la has ejecutado.
- No ocultes errores, limitaciones ni tareas incompletas.

## 4. Flujo de trabajo

Para cada tarea:
1. Resume el objetivo y los archivos que esperas modificar.
2. Revisa el código y patrones existentes.
3. Propón un plan breve.
4. Implementa el cambio mínimo completo.
5. Añade o actualiza pruebas.
6. Ejecuta build, lint y pruebas pertinentes.
7. Revisa el diff buscando regresiones, secretos o cambios accidentales.
8. Actualiza documentación si cambia el comportamiento o un contrato.
9. Informa de archivos modificados, comandos ejecutados, resultados y riesgos pendientes.

## 5. Definición de terminado

Una tarea solo está terminada cuando:
- Cumple todos sus criterios de aceptación.
- Compila/build correctamente en el ámbito afectado.
- Las pruebas relevantes pasan.
- Los errores se manejan de forma explícita.
- La autorización y validación están implementadas donde corresponda.
- La documentación/contratos están actualizados.
- No quedan `TODO`, mocks o datos ficticios en el camino funcional, salvo que estén claramente etiquetados y aceptados.
- El resumen final distingue lo probado de lo que no se ha podido probar.

## 6. Coordinación multiagente

- Un agente coordinador mantiene el backlog, define interfaces y resuelve conflictos.
- Asigna a cada agente un módulo o conjunto de archivos claramente delimitado.
- Evita que dos agentes editen simultáneamente el mismo archivo.
- El agente que modifica contratos compartidos debe anunciar el cambio y obtener aprobación.
- Integra cambios mediante ramas/commits pequeños y revisables.
- No hagas cherry-pick, merge, push ni operaciones destructivas sin autorización explícita del propietario, salvo que el flujo del repositorio lo autorice claramente.

## 7. Roles recomendados

### Coordinator / Architect
- Mantiene arquitectura, decisiones, contratos y prioridades.
- Descompone historias en tareas pequeñas.
- Revisa integración entre módulos.
- No implementa grandes funcionalidades en paralelo con los demás agentes.

### Backend
- API, identidad, campañas, permisos, persistencia y tiempo real.
- Mantiene el servidor como autoridad del estado compartido.
- Añade pruebas unitarias e integración.

### Web
- React/TypeScript/PixiJS, interfaz, mapa, interacción y accesibilidad.
- Consume API/SDK/contratos; no implementa reglas autoritativas.

### Godot Desktop
- Cliente de escritorio Godot + C# si se confirma esta decisión.
- Consume los mismos contratos y servicios que el cliente web.
- No crea una segunda implementación de reglas de negocio.

### QA
- Diseña casos de prueba, automatiza flujos E2E y busca regresiones.
- Comprueba permisos, reconexión, concurrencia y estados límite.
- No modifica arquitectura sin coordinarlo.

## 8. Seguridad

- Verifica autorización por recurso y por acción.
- Valida tamaño, formato y contenido de archivos subidos.
- Evita path traversal, inyección, IDOR y exposición de información entre campañas.
- Usa hashing de contraseñas con una solución mantenida y estándar; nunca inventes criptografía.
- Mantén secretos fuera de logs y commits.
- Añade rate limits a endpoints sensibles cuando corresponda.
- No confíes en IDs enviados por el cliente como prueba de autorización.

## 9. Comunicación del agente

Al terminar, responde con:
- **Resultado:** qué se ha implementado.
- **Archivos:** lista de archivos modificados.
- **Verificación:** comandos y pruebas ejecutados con resultado real.
- **Pendiente:** limitaciones, decisiones necesarias y riesgos.
- **Siguiente tarea:** propuesta concreta, sin empezar trabajo adicional no solicitado.
