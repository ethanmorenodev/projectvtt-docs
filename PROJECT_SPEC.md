# ProjectVTT — Especificación del producto

**Versión:** 0.1  
**Estado:** borrador de trabajo  
**Propietario:** equipo ProjectVTT

## 1. Visión

ProjectVTT es una plataforma Virtual Tabletop (VTT) para organizar y jugar partidas de rol online. Busca ofrecer una experiencia accesible y fluida, con herramientas potentes para directores de juego y jugadores, personalización y extensibilidad, buen rendimiento y estabilidad.

El proyecto aspira a ofrecer:
- Cliente web.
- Aplicación de escritorio.
- Alojamiento cloud gestionado.
- Instalación self-hosted.
- Soporte multisistema, comenzando por un primer sistema de reglas.

Estas metas describen la dirección del producto; no implican que todas las capacidades deban estar en el primer MVP.

## 2. Objetivos del MVP

El MVP debe permitir realizar una sesión básica compartida sin depender de herramientas externas para las funciones esenciales.

### P0 — imprescindible
- Registro/inicio de sesión y gestión básica de identidad.
- Crear campañas y unirse mediante invitación.
- Roles iniciales: propietario/Director de Juego y jugador.
- Permisos básicos para campaña, escena, tokens y documentos.
- Crear y abrir escenas.
- Importar y mostrar una imagen de mapa.
- Zoom y desplazamiento del mapa.
- Cuadrícula cuadrada; la hexagonal puede entrar en P0 si no retrasa la experiencia principal.
- Crear, seleccionar y mover tokens.
- Ajuste opcional al grid.
- Sincronización en tiempo real entre al menos dos usuarios.
- Persistencia de escenas y posiciones.
- Recuperación del estado al reconectar.
- Ficha de personaje básica con atributos y recursos.
- Tiradas de dados y modificadores básicos.
- Un primer Ruleset, pendiente de elección.

### P1 — siguiente prioridad
- Chat de campaña y mensajes privados.
- Combate, iniciativa, turnos y condiciones.
- Niebla de guerra manual.
- Notas privadas del Director de Juego.
- Historial básico de cambios.
- Backups y restauración.
- Instalación self-hosted documentada mediante Docker Compose.
- Cliente de escritorio con las funciones esenciales del cliente web.

### Fuera del primer MVP
- Marketplace público.
- Ejecución arbitraria de código de terceros en el servidor.
- Audio/vídeo integrado.
- Iluminación dinámica avanzada.
- Automatización compleja de todos los sistemas.
- IA que dirija partidas autónomamente.
- Editor avanzado de mapas y animaciones complejas.

## 3. Principios de producto

- **Multisistema:** el núcleo no debe asumir que todos los juegos usan Fuerza, Clase de Armadura, puntos de golpe u otras convenciones concretas.
- **Accesibilidad:** las tareas habituales deben ser fáciles de descubrir y ejecutar.
- **Rendimiento:** mapas y tokens deben seguir siendo utilizables en escenas grandes.
- **Fiabilidad:** las acciones compartidas deben validarse y persistirse correctamente.
- **Extensibilidad:** diseñar puntos de extensión explícitos, sin permitir plugins inseguros en el MVP.
- **Autonomía de alojamiento:** cloud y self-hosted son objetivos del producto, aunque pueden desplegarse en fases.

## 4. Usuarios y permisos iniciales

Roles mínimos propuestos:
- **Owner:** propietario de campaña; administra miembros y configuración.
- **GM:** dirige la partida y controla escenas/documentos según permisos.
- **Player:** participa y controla únicamente los actores/tokens autorizados.

No asumir que Owner y GM siempre son la misma persona. El modelo debe permitir separarlos más adelante.

## 5. Requisitos funcionales

### Campañas
- Crear, renombrar y archivar una campaña.
- Invitar y retirar miembros.
- Consultar los miembros y sus roles.
- Impedir el acceso a usuarios no autorizados.

### Escenas y mapas
- Crear una escena con nombre, imagen de fondo y configuración de grid.
- Subir/importar un mapa con validación de tipo y tamaño.
- Mostrar el mapa sin deformar su relación de aspecto.
- Hacer zoom y pan.
- Guardar la configuración de escena.

### Tokens
- Crear tokens vinculados o no a un Actor.
- Seleccionar y mover tokens.
- Validar en servidor que el usuario puede mover el token.
- Sincronizar movimientos a los demás participantes.
- Guardar posición y versión del estado.
- Evitar que una reconexión restaure una posición obsoleta.

### Actores y tiradas
- Crear un Actor con datos generales y atributos definidos por el Ruleset.
- Representar recursos como valores actuales/máximos cuando proceda.
- Solicitar una tirada al servidor.
- Validar la petición y devolver un resultado reproducible/auditable según el diseño del Ruleset.
- No codificar reglas específicas en el Core.

## 6. Requisitos no funcionales

- Autorización comprobada en servidor, nunca solo en interfaz.
- Validación de todos los datos entrantes.
- Contratos API versionados.
- Migraciones de base de datos reproducibles.
- Logs estructurados sin filtrar secretos ni datos privados innecesarios.
- Manejo de errores consistente.
- Reconexión y resincronización.
- Pruebas unitarias, integración y E2E para flujos críticos.
- Límites configurables de subida de archivos.
- Protección contra acceso a campañas/activos de otros usuarios.
- Documentación de instalación y configuración.

## 7. Criterio de éxito del primer vertical slice

Se considera logrado cuando:
1. Dos usuarios autenticados pueden entrar en la misma campaña.
2. Ambos pueden abrir la misma escena.
3. Un usuario mueve un token y el otro ve el movimiento en tiempo real.
4. El movimiento queda guardado.
5. Si un cliente se desconecta y vuelve, recupera el estado actual.
6. Un usuario sin permisos no puede modificar el token.
7. Hay pruebas automatizadas que cubren el flujo principal y los permisos.

## 8. Decisiones pendientes del propietario

No tomar estas decisiones por inferencia:
- **Sistema de reglas inicial:** PENDIENTE.
- **Motor definitivo del cliente de escritorio:** propuesta Godot 4 + C#, pendiente de confirmación.
- **Tecnología del cliente web:** propuesta React + TypeScript + PixiJS.
- **Paridad de funcionalidades web/escritorio en el MVP:** PENDIENTE.
- **Proveedor cloud inicial y modelo de costes:** PENDIENTE.
- **Nombre comercial, identidad visual y licencia:** PENDIENTE.
