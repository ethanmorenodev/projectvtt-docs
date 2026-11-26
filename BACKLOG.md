# ProjectVTT — Backlog inicial

Prioridades:
- **P0:** bloquea el primer vertical slice o el MVP.
- **P1:** importante para una primera experiencia completa.
- **P2:** posterior al MVP.

Cada tarea debe convertirse en una issue pequeña antes de asignarse a un agente.

## Épica A — Preparación

- [ ] **P0** Confirmar sistema de reglas inicial.
- [ ] **P0** Confirmar cliente escritorio y versión objetivo de Godot.
- [ ] **P0** Confirmar alcance de paridad web/escritorio.
- [ ] **P0** Crear monorepo y convenciones.
- [ ] **P0** Añadir CI con build y tests.
- [ ] **P0** Añadir Docker Compose para desarrollo.
- [ ] **P0** Crear ADRs para decisiones confirmadas.

## Épica B — Backend y acceso

- [ ] **P0** Crear API ASP.NET Core.
- [ ] **P0** Configurar PostgreSQL y migraciones.
- [ ] **P0** Implementar autenticación.
- [ ] **P0** Crear campañas.
- [ ] **P0** Implementar membresías e invitaciones.
- [ ] **P0** Implementar roles y autorización por recurso.
- [ ] **P0** Añadir pruebas de acceso no autorizado.

## Épica C — Tiempo real

- [ ] **P0** Configurar SignalR.
- [ ] **P0** Asociar conexiones a campañas autorizadas.
- [ ] **P0** Definir primer contrato de comando/evento.
- [ ] **P0** Implementar movimiento de token validado en servidor.
- [ ] **P0** Persistir el movimiento antes de confirmarlo.
- [ ] **P0** Gestionar comandos duplicados.
- [ ] **P0** Reconectar y resincronizar estado.
- [ ] **P0** Probar dos clientes simultáneos.

## Épica D — Cliente web y mapa

- [ ] **P0** Crear aplicación web.
- [ ] **P0** Integrar PixiJS.
- [ ] **P0** Crear vista de campaña/escena.
- [ ] **P0** Importar mapa con validación.
- [ ] **P0** Implementar zoom y pan.
- [ ] **P0** Dibujar grid cuadrado.
- [ ] **P0** Crear, seleccionar y mover token.
- [ ] **P0** Sincronizar con backend.
- [ ] **P1** Añadir grid hexagonal.

## Épica E — Actores y reglas

- [ ] **P0** Definir modelo genérico Actor.
- [ ] **P0** Definir esquema de atributos y recursos.
- [ ] **P0** Crear interfaz del Ruleset tras elegir el sistema.
- [ ] **P0** Implementar primera tirada.
- [ ] **P0** Implementar modificadores.
- [ ] **P1** Inventario.
- [ ] **P1** Efectos y condiciones.
- [ ] **P1** Automatización específica del Ruleset.

## Épica F — Herramientas de sesión

- [ ] **P1** Chat de campaña.
- [ ] **P1** Mensajes privados.
- [ ] **P1** Iniciativa y turnos.
- [ ] **P1** Niebla de guerra manual.
- [ ] **P1** Notas privadas de GM.
- [ ] **P1** Historial de cambios.

## Épica G — Escritorio

- [ ] **P0/P1** Crear proyecto Godot si se confirma como cliente separado.
- [ ] **P0/P1** Implementar autenticación y conexión.
- [ ] **P0/P1** Consumir contratos compartidos.
- [ ] **P0/P1** Abrir campaña y escena.
- [ ] **P0/P1** Renderizar mapa y tokens.
- [ ] **P0/P1** Sincronizar movimientos.
- [ ] **P1** Alcanzar paridad funcional acordada.

## Épica H — Operación y calidad

- [ ] **P0** Logs estructurados.
- [ ] **P0** Gestión segura de configuración y secretos.
- [ ] **P0** Límites de subida de archivos.
- [ ] **P0** Pruebas de integración.
- [ ] **P0** Pruebas E2E del vertical slice.
- [ ] **P1** Docker Compose self-hosted.
- [ ] **P1** Backups y restauración.
- [ ] **P1** Monitorización básica.
- [ ] **P1** Pruebas de rendimiento.

## Primeras cinco tareas recomendadas

1. Resolver las decisiones pendientes de `DECISIONS.md`.
2. Inspeccionar el entorno real y crear el monorepo mínimo.
3. Preparar CI y Docker Compose.
4. Definir contratos de campaña, escena y movimiento de token.
5. Construir el flujo de dos usuarios moviendo un token en una escena compartida.
