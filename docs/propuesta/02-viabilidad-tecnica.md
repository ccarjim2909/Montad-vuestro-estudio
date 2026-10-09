# 1.  Análisis de requisitos funcionales.

### Funcionalidades Principales

1.  El usuario puede registrarse con un perfil de jugador .

2.  El usuario puede iniciar/cerrar sesión.

3.  El usuario puede crear un partido especificando fecha, hora, ubicación, tipo de fútbol (F5/F7) y plazas disponibles.

4.  El usuario puede definir el precio total del campo y la cuota individual por jugador.

5.  El usuario puede buscar partidos públicos filtrando por ciudad/zona, fecha, horario y nivel requerido.

6.  El usuario puede unirse a un partido público disponible realizando el pago de la plaza individual.

7.  El usuario puede cancelar la inscripción a un partido dentro del margen de tiempo permitido.

8.  El usuario puede valorar el nivel de juego de los rivales y compañeros al finalizar un partido.

9.  El usuario puede consultar el perfil de un jugador con su nivel medio ponderado y estadísticas básicas.

10. El usuario puede visualizar los partidos disponibles en una lista y en un mapa interactivo.

11. El usuario puede registrar polideportivos e instalaciones deportivas con sus campos disponibles.

12. El usuario puede reservar pistas de forma directa a través de la plataforma.

13. La aplicación puede enviar notificaciones de confirmación, avisos de plaza cubierta o cancelaciones.

14. El usuario puede consultar el historial de partidos jugados y cobros/pagos realizados.

15. El usuario puede visualizar la clasificación y ranking local de jugadores por zona.

### Priorización MoSCoWMust Have (Indispensables)

-   El usuario puede registrarse con un perfil de jugador 

-   El usuario puede iniciar/cerrar sesión.

-   El usuario puede crear un partido especificando fecha, hora, ubicación, tipo de fútbol (F5/F7) y plazas disponibles.

-   El usuario puede definir el precio total del campo y la cuota individual por jugador.

-   El usuario puede buscar partidos públicos filtrando por ciudad/zona, fecha, horario y nivel requerido.

-   El usuario puede unirse a un partido público disponible realizando el pago de la plaza individual.

#### Should Have (Importantes)

-   El usuario puede cancelar la inscripción a un partido dentro del margen de tiempo permitido.

-   El usuario puede visualizar los partidos disponibles en una lista y en un mapa interactivo.

-   La aplicación puede enviar notificaciones de confirmación, avisos de plaza cubierta o cancelaciones.

-   El usuario puede valorar el nivel de juego de los rivales y compañeros al finalizar un partido.

-   El usuario puede consultar el perfil de un jugador con su nivel medio ponderado y estadísticas básicas.

#### Could Have (Deseables)

-   El usuario puede registrar polideportivos e instalaciones deportivas con sus campos disponibles.

-   El usuario puede filtrar partidos según nivel

-   El usuario puede consultar el historial de partidos jugados y cobros/pagos realizados.

#### Won't Have (Fuera de alcance para esta versión)

-   El usuario puede visualizar la clasificación y ranking local de jugadores por zona.

-   El usuario puede reservar pistas de forma directa a través de la plataforma.


#### MVP (Minimum Viable Product - Mínimo Producto Viable)

-   Entrar a la aplicación > Registrarse con un usuario > Editar perfil

-   Iniciar sesión > Menú principal > Buscar partido > Filtro de selección > Escoger sesión (hora) > Comprobar participantes > Pagar cuota alquiler

-   Iniciar sesión > Menú principal > Crear partido > Seleccionar pista > Reservar horario disponible > Etiquetas del partido (número de jugadores, duración etc) > Comprobar participantes > Pagar cuota alquiler




# 2.  Análisis de requisitos técnicos.


### Frontend (React SPA)

-   Navegación: react-router-dom para el enrutamiento del lado del cliente y la protección de rutas privadas (panel de usuario, creación de partidos).

-   Gestión de Estado Global: zustand para un control ligero del estado de la sesión autenticada y filtros activos de búsqueda.

-   Interfaz y Estilos: tailwindcss junto a componentes de shadcn/ui para construir rápidamente una interfaz adaptable.

-   Peticiones HTTP: axios configurado con interceptores para adjuntar automáticamente el token JWT en cada solicitud.

### Infraestructura y Despliegue

-   Frontend:  Vercel o Netlify. Plan Hobby/Free (Despliegue continuo con GitHub, SSL automático, 100 GB de transferencia mensual gratuita).

-   Backend:  Render (Plan Free Web Service, 512 MB RAM)

-   Base de datos:  MongoDB Atlas. Plan M0 Shared Cluster gratuito permanente



### Backend (Node.js + Express)

-   Autenticación y Autorización: Implementación de JSON Web Tokens (JWT) mediante cookies de tipo HttpOnly para evitar ataques XSS.

-   Control de Roles:

-   Jugador: Usuario base que busca, se une y valora partidos.

-   Organizador: Usuario que crea el evento y administra sus plazas.

-   Administrador: Gestión de reportes, usuarios y catálogo de centros deportivos.

-   Servicios Externos e Integraciones:

-   Resend / Nodemailer (Emails transaccionales): Envío de confirmaciones de reserva y recordatorios.

### Base de Datos (MongoDB + Mongoose)


#### Colección: Usuarios

| Campo | Tipo | Requerido | Notas / Restricciones |
| :--- | :--- | :--- | :--- |
| `id` | String | Sí | — |
| `nombre` | String | Sí | — |
| `email` | String | Sí | Único (`unique`) |
| `contraseñaHash` | String | Sí | — |
| `ciudad` | String | Sí | — |


#### Colección: Partidos

| Campo | Tipo | Requerido | Notas / Restricciones |
| :--- | :--- | :--- | :--- |
| `id_organizador` | ObjectId | Sí | Referencia a `Usuarios` `ìd` |
| `modo` | String | Sí | Valores permitidos: `'F5'`, `'F7'`, `'F11'` |
| `nombreLocalizacion` | String | Sí | Referencia a `Pistas` `nombre` |
| `direccionLocalizacion` | String | Sí | Referencia a `Pistas` `direccion` |
| `hora` | Date | Sí | — |
| `precioTotal` | Number | Sí | — |
| `precioPorJugador` | Number | Sí | — |
| `maximoJugadores` | Number | Sí | — |
| `jugadoresConfirmados` | Array | No | Array de jugadores inscritos |
| `estadoPago` | String | No | Valores: `'pendiente'`, `'pagado'` (Valor por defecto: `'pendiente'`) |
| `estado` | String | No | Valores: `'abierta'`, `'completa'`, `'cancelada'` (Valor por defecto: `'abierta'`) |


#### Colección: Pistas

| Campo | Tipo | Requerido | Notas / Restricciones |
| :--- | :--- | :--- | :--- |
| `id` | String | Sí | — |
| `nombre` | String | Sí | — |
| `direccion` | String | Sí | Único (`unique`) |
| `ciudad` | String | Sí | — |


# 3.  Evaluación de capacidades del equipo.



# 4.  Identificación de riesgos técnicos.
