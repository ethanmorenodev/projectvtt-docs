# ProjectVTT — Registro de decisiones (ADR)

Este documento registra decisiones arquitectónicas. Una propuesta no se considera aceptada hasta que su estado sea **Aceptada**.

## ADR-001 — Monolito modular para el MVP

**Estado:** Propuesta  
**Contexto:** el producto necesita varios dominios, pero el equipo inicial es pequeño y la integración distribuida añadiría complejidad.  
**Decisión propuesta:** desplegar un backend único organizado por módulos de dominio.  
**Consecuencias:** despliegue y depuración más simples; los límites de módulos deben mantenerse para evitar acoplamiento.

## ADR-002 — Backend autoritativo

**Estado:** Propuesta  
**Contexto:** varios usuarios pueden modificar una partida simultáneamente.  
**Decisión propuesta:** el servidor valida permisos y acciones, persiste el estado y publica eventos.  
**Consecuencias:** más trabajo de servidor, pero comportamiento consistente y menor riesgo de manipulación del cliente.

## ADR-003 — Clientes web y escritorio con contratos comunes

**Estado:** Propuesta  
**Contexto:** se desean clientes web y escritorio sin duplicar reglas de negocio.  
**Decisión propuesta:** contratos HTTP/eventos compartidos; web con React/TypeScript/PixiJS y escritorio con Godot/C#, sujeto a confirmación.  
**Consecuencias:** dos interfaces que mantener; contratos y pruebas de integración son críticos.

## ADR-004 — PostgreSQL como persistencia principal

**Estado:** Propuesta  
**Contexto:** se necesitan relaciones, permisos, consistencia y datos variables de Rulesets.  
**Decisión propuesta:** PostgreSQL, usando JSONB solo para partes variables y validadas del dominio.  
**Consecuencias:** modelo relacional para entidades principales y flexibilidad controlada para datos de sistema.

## ADR-005 — Primer Ruleset

**Estado:** Pendiente de decisión del propietario  
**Pregunta:** ¿Qué sistema de rol debe soportar primero ProjectVTT?  
**Restricción:** no diseñar automatizaciones concretas ni cerrar el modelo de datos específico hasta conocer el sistema.

## ADR-006 — Cliente de escritorio

**Estado:** Pendiente de confirmación  
**Propuesta actual:** Godot 4 + C# como cliente de escritorio, conectado al backend común.  
**Pregunta:** ¿Se requiere paridad completa con la web en el MVP o puede llegar en una fase posterior?

## ADR-007 — Alojamiento

**Estado:** Propuesta  
**Objetivo de producto:** cloud gestionado y self-hosted.  
**Propuesta de implementación:** primero entorno reproducible con Docker Compose; después separar despliegue cloud y guías self-hosted sin bifurcar la aplicación.

## Cómo registrar una decisión

Para cada nueva ADR:
- ID y título.
- Estado: Propuesta / Aceptada / Rechazada / Sustituida.
- Contexto.
- Decisión.
- Alternativas consideradas.
- Consecuencias y riesgos.
- Fecha y responsable, cuando se conozcan.
