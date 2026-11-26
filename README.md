# ProjectVTT — Documentación de producto y arquitectura

Documentación pública del caso de estudio **ProjectVTT**, una mesa virtual para campañas de juegos de rol. El código fuente del proyecto es privado; este repositorio recoge la definición del producto, las decisiones técnicas y la planificación para que el trabajo sea auditable y verificable.

> Estado: la documentación recogida aquí corresponde a la revisión del **10 de noviembre de 2026**. Las decisiones marcadas como `Propuesta` o `Pendiente` no deben interpretarse como cerradas.

## Documentos

| Documento | Contenido |
|---|---|
| [PROJECT_SPEC.md](PROJECT_SPEC.md) | Visión, alcance, requisitos y criterios de aceptación. |
| [ARCHITECTURE.md](ARCHITECTURE.md) | Arquitectura propuesta y límites entre componentes. |
| [DECISIONS.md](DECISIONS.md) | Registro de decisiones arquitectónicas (ADR) y cuestiones pendientes. |
| [ROADMAP.md](ROADMAP.md) | Hitos y planificación orientativa. |
| [BACKLOG.md](BACKLOG.md) | Primeras tareas implementables. |
| [AGENTS.md](AGENTS.md) | Convenciones de trabajo para agentes de IA y personas colaboradoras. |

## Arquitectura resumida

Stack propuesto en la documentación, pendiente de confirmación (ver `ARCHITECTURE.md` y los ADR):

```text
Cliente web (React 19 · TypeScript · PixiJS 8)
Cliente escritorio (Godot 4.7.2 / .NET · C#)
              │  API / SignalR
              ▼
Servidor autoritativo (ASP.NET Core 10 · EF Core)
              │  Persistencia
              ▼
SQLite en desarrollo · PostgreSQL como destino documentado
```

## Principios de trabajo

1. Priorizar un producto pequeño que funcione de extremo a extremo.
2. El servidor es la autoridad sobre el estado compartido de la partida.
3. Los clientes web y escritorio comparten contratos y reglas de negocio.
4. No introducir complejidad distribuida antes de necesitarla.
5. Ninguna tarea se considera terminada solo porque compile: debe cumplir sus criterios y tener pruebas apropiadas.
6. No inventar decisiones del propietario del proyecto: preguntar o registrar como pendiente.

## Caso de estudio

La presentación visual del proyecto, con capturas reales etiquetadas y estado MVP/post-MVP, está publicada en el [portfolio](https://ethanmorenodev.github.io/portfolio/#projectvtt).

## Licencia y uso

La licencia del producto está pendiente de decisión del propietario (`PROJECT_SPEC.md`), por lo que este repositorio no aplica una licencia propia. La documentación se publica para consulta y revisión del caso de estudio; su reproducción requiere el permiso del propietario del proyecto.
