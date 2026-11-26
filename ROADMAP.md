# ProjectVTT — Roadmap inicial

Las duraciones son hipótesis de planificación. Se deben recalibrar después del primer vertical slice y según la disponibilidad real del equipo.

## Fase 0 — Preparación (3–7 días)

- Confirmar decisiones críticas.
- Crear monorepo y estructura mínima.
- Configurar Git, ramas y CI.
- Crear Docker Compose de desarrollo.
- Definir convenciones y contratos iniciales.
- Preparar pruebas y documentación para agentes.

**Salida:** cualquier agente puede clonar, ejecutar, probar y entender el proyecto.

## Fase 1 — Vertical slice online (2–4 semanas)

- Autenticación mínima.
- Crear campaña y añadir dos usuarios.
- Conexión en tiempo real.
- Crear escena y cargar mapa.
- Mostrar mapa en cliente web.
- Crear y mover token.
- Sincronizar movimiento entre dos clientes.
- Persistir posición.
- Reconectar y restaurar estado.
- Probar permisos.

**Salida:** primera escena compartida funcional.

## Fase 2 — Núcleo de partida (3–5 semanas)

- Actores y fichas.
- Atributos y recursos configurables.
- Tiradas y modificadores.
- Primer Ruleset.
- Inventario básico.
- Mejoras de UX y errores.

**Salida:** sesión sencilla con personajes y tiradas.

## Fase 3 — Herramientas de sesión (3–5 semanas)

- Chat.
- Combate e iniciativa.
- Turnos y condiciones.
- Niebla de guerra manual.
- Notas privadas del GM.
- Historial básico.

**Salida:** MVP de mesa más completo.

## Fase 4 — Escritorio y alojamiento (3–6 semanas, parcialmente en paralelo)

- Cliente Godot conectado al mismo backend.
- Paridad de las funciones acordadas.
- Docker Compose self-hosted.
- Almacenamiento de assets.
- Backups y restauración.
- Configuración y documentación de despliegue.

**Salida:** cliente de escritorio y despliegue reproducible.

## Fase 5 — Estabilización (2–4 semanas)

- Pruebas de concurrencia y carga.
- Seguridad y revisión de permisos.
- Recuperación ante desconexiones.
- Migraciones y backups probados.
- Optimización de mapas y tokens.
- Pruebas con usuarios.
- Corrección de bugs prioritarios.

**Salida:** MVP apto para un grupo pequeño de usuarios de prueba.

## Regla de planificación

No comprometer una fecha comercial basándose solo en la velocidad de generación de código. Reestimar al terminar cada fase, usando tareas cerradas, defectos encontrados y tiempo de integración real.
