# ProjectVTT — Arquitectura inicial

**Estado:** propuesta, no decisión definitiva.  
**Objetivo:** compartir dominio, contratos y backend entre cliente web y escritorio.

## 1. Vista general propuesta

```text
                 ┌─────────────────────┐
                 │     Web Client      │
                 │ React + TS + PixiJS │
                 └──────────┬──────────┘
                            │ HTTPS / WebSocket
                 ┌──────────▼──────────┐
                 │   ASP.NET Core API  │
                 │ Auth / Modules      │
                 │ Rules / Permissions │
                 └──────┬────────┬────┘
                        │        │
                ┌───────▼───┐ ┌──▼────────────┐
                │PostgreSQL│ │ Object Storage│
                └───────────┘ └───────────────┘
                            ▲
                 ┌──────────┴──────────┐
                 │   Godot Desktop     │
                 │    C# Client        │
                 └─────────────────────┘
```

## 2. Stack candidato

| Área | Propuesta | Estado |
|---|---|---|
| Cliente web | React + TypeScript + PixiJS | Propuesto |
| Escritorio | Godot 4 + C# | Propuesto; confirmar |
| Backend | ASP.NET Core / C# | Propuesto |
| Tiempo real | SignalR sobre WebSockets | Propuesto |
| Base de datos | PostgreSQL | Propuesto |
| Archivos cloud | Almacenamiento compatible con S3 | Propuesto |
| Archivos self-hosted | MinIO o almacenamiento compatible | Propuesto |
| Entorno local | Docker Compose | Propuesto |
| Contratos | OpenAPI + JSON Schema/event schemas | Propuesto |
| Tests .NET | xUnit | Propuesto |
| E2E web | Playwright | Propuesto |
| CI | GitHub Actions | Propuesto |

Antes de fijar versiones, comprobar compatibilidad y soporte vigentes. No actualizar paquetes automáticamente a versiones mayores.

## 3. Forma de despliegue

Empezar con un **monolito modular**:
- Un backend desplegable.
- Una base PostgreSQL.
- Módulos separados por dominio.
- Límites internos claros.
- Sin microservicios en el MVP.

Cloud y self-hosted deben utilizar el mismo artefacto de aplicación y configuración por entorno, evitando bifurcar el código.

## 4. Límites de responsabilidad

### Core
Conceptos comunes: campañas, miembros, permisos, escenas, tokens, actores, documentos, recursos, efectos y tiradas como conceptos genéricos.

El Core no debe interpretar el significado de atributos específicos de un sistema de rol.

### Ruleset
Implementa las reglas de un juego concreto:
- Validación de acciones.
- Resolución de tiradas.
- Aplicación de efectos.
- Interpretación de atributos y recursos.
- Serialización y validación de datos propios del sistema.

El Ruleset inicial está pendiente de elección.

### Modules
Funciones opcionales que amplían el producto. En el MVP, solo extensiones internas o confiables. No ejecutar scripts arbitrarios de usuarios en el servidor.

## 5. Backend modular sugerido

- Identity: usuarios y sesiones.
- Campaigns: campañas.
- Membership: miembros, invitaciones y roles.
- Scenes: escenas y mapas.
- Tokens: tokens y movimiento.
- Actors: personajes y actores.
- Rules: integración de Ruleset.
- Combat: iniciativa, turnos y estados.
- Chat: mensajes.
- FogOfWar: visibilidad.
- Assets: archivos y metadatos.

No es necesario crear un proyecto independiente por módulo al principio. Mantener una solución y límites de código claros.

## 6. Servidor autoritativo

Para cualquier acción que cambie el estado compartido:
1. El cliente envía un comando con identificador único.
2. El servidor autentica al usuario.
3. El servidor valida permisos, datos y reglas.
4. Comprueba la versión esperada del estado cuando proceda.
5. Persiste el cambio.
6. Publica un evento a los clientes autorizados.
7. Los clientes actualizan su representación.

El cliente puede predecir visualmente un movimiento para mejorar la respuesta, pero el servidor confirma o rechaza el resultado.

## 7. Comandos y eventos

Ejemplos de comandos:
- `MoveToken`
- `CreateToken`
- `UpdateActor`
- `RequestRoll`
- `AdvanceTurn`

Ejemplos de eventos:
- `TokenMoved`
- `TokenCreated`
- `ActorUpdated`
- `RollResolved`
- `TurnAdvanced`

Cada evento debería incluir, según corresponda:
- `eventId`
- `campaignId`
- `sceneId` o `aggregateId`
- `actorUserId`
- `occurredAt`
- `schemaVersion`
- `aggregateVersion`
- datos del cambio

Los nombres y esquemas son ejemplos, no contratos aprobados.

Diseñar idempotencia para comandos repetidos y una estrategia de publicación fiable (por ejemplo, transactional outbox) cuando el flujo de eventos esté definido.

## 8. Persistencia

- Relacional para usuarios, campañas, membresías, escenas, tokens, relaciones y permisos.
- JSONB solo para datos variables de Actors/Rulesets que necesiten flexibilidad.
- Validar el JSON según el Ruleset activo.
- Versionar los datos y la versión del Ruleset de cada campaña.
- Usar migraciones revisables y probadas.

No guardar todo el dominio como un único documento JSON.

## 9. Contratos compartidos

OpenAPI para endpoints HTTP y esquemas versionados para eventos/comandos.
Generar o mantener SDKs TypeScript y .NET a partir de contratos cuando sea viable.

Los clientes no deben inventar modelos paralelos. Los cambios incompatibles requieren versionado o migración coordinada.

## 10. Estructura de repositorio sugerida

```text
ProjectVTT/
├── apps/
│   ├── web/
│   └── desktop/
├── backend/
│   ├── Api/
│   ├── Realtime/
│   ├── Modules/
│   ├── Infrastructure/
│   └── Shared/
├── packages/
│   ├── contracts/
│   ├── sdk-typescript/
│   └── sdk-dotnet/
├── tests/
│   ├── Unit/
│   ├── Integration/
│   ├── E2E/
│   └── Performance/
├── infra/
│   ├── docker/
│   ├── deployment/
│   └── monitoring/
└── docs/
```

La estructura se debe adaptar al repositorio real; no crear todos los directorios vacíos por anticipado.

## 11. Riesgos técnicos principales

- Duplicar comportamiento entre web y Godot.
- Diseñar un sistema multisistema demasiado abstracto antes de probar un Ruleset real.
- Concurrencia y movimientos simultáneos de tokens.
- Reconexión y resincronización incorrecta.
- Permisos incompletos o comprobados solo en cliente.
- Cargas de mapas grandes y consumo de memoria.
- Diferencias entre cloud y self-hosted.
- Complejidad de mantener dos clientes desde el primer día.

Mitigación: vertical slice temprano, contratos compartidos, servidor autoritativo y pruebas E2E con dos clientes.
