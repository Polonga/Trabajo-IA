# Proyecto Integral I - Software Requirements & Design Document

## 6.1. Identificación del proyecto
* **Nombre del proyecto:** {Nombre del programa}
* **Autor:** Pablo Lozano
* **Descripción breve de la aplicación:** Sistema de escritorio para la gestión integral de catálogo, licencias digitales, ventas, alquileres y reservas en una plataforma de videojuegos, con asistencia de IA para la catalogación técnica y la recomendación semántica.
* **Versión del documento:** v1.0
* **Fecha de desarrollo:** 10/2026 - 01/2027

---

## 6.2. Descripción General y Objetivos

### 6.2.1. Descripción de la aplicación
**{Nombre del programa}** es una plataforma de escritorio para la gestión y distribución de licencias y claves digitales de videojuegos.

La aplicación permite administrar el inventario de códigos de activación mediante dos modalidades comerciales complementarias:
1. **Adquisición definitiva:** Venta convencional del código digital con asignación permanente al usuario a precio completo.
2. **Alquiler por licencia temporal:** Acceso al título por periodos tasados (por ejemplo, tarifas semanales de 5 €), activando un código con caducidad programada que expira automáticamente al concluir el plazo contratado a menos que el cliente tramite una prórroga o renovación.

La plataforma integra una tienda para explorar el catálogo, un área de **"Mi Biblioteca"** donde el jugador gestiona sus títulos y supervisa el tiempo restante de sus alquileres, y un módulo conectado a una API de Inteligencia Artificial que facilita tanto el autocompletado de fichas técnicas para el administrador como la recomendación semántica en lenguaje natural para el usuario.

### 6.2.2. Problema o necesidad
En el mercado digital actual, los jugadores acumulan cientos de videojuegos comprados a precio completo que sólo completan una vez y quedan abandonados en sus bibliotecas digitales, encareciendo el acceso al ocio. Paralelamente, los distribuidores y tiendas de claves digitales no disponen de mecanismos estandarizados para ofrecer modelos de acceso temporal flexible (alquiler por semanas), limitándose al esquema rígido de venta definitiva. 

La gestión de claves temporales plantea retos operativos que no pueden resolverse de forma manual ni con hojas de cálculo:
* **Control de vigencia y revocación:** Necesidad de registrar y monitorear fechas y horas exactas de caducidad de cada clave prestada, deshabilitando el acceso de forma desatendida cuando el cliente no abona la renovación semanal.
* **Costes de gestión de catálogo:** La inclusión continua de lanzamientos digitales requiere catalogar sinopsis, géneros y clasificaciones de edad de forma ágil para no saturar al personal.
* **Sobrecarga de opciones para el usuario:** En tiendas con miles de claves, los motores de búsqueda basados en texto exacto impiden asesorar a clientes que buscan experiencias por sensaciones o temáticas concretas (por ejemplo: *"un RPG con protagonista femenina"* o *"un juego cooperativo corto"*).

**{Nombre del programa}** cubre esta necesidad ofreciendo una solución que centraliza el almacén de claves, automatiza el cálculo de tarifas por semanas de uso, revoca el acceso a las licencias vencidas e integra un buscador semántico por IA para orientar las decisiones de compra o alquiler.

### 6.2.3. Objetivos

#### Objetivo general
Desarrollar una aplicación de escritorio robusta en Java con persistencia relacional que centralice la gestión, distribución, venta y alquiler de licencias y claves digitales de videojuegos, asistida por capacidades de Inteligencia Artificial generativa.

#### Objetivos específicos
* Automatizar la gestión del inventario de claves digitales en tiempo real, diferenciando entre códigos de compra permanente y licencias de activación temporal por periodos tasados.
* Aplicar reglas de negocio automáticas para el cómputo de tarifas semanales, control de fechas de caducidad, revocación desatendida del acceso tras el vencimiento y asignación prioritaria de claves reservadas.
* Implementar llamadas a una API externa de IA para autocompletar la ficha técnica de los videojuegos y ofrecer un motor de recomendaciones semánticas en lenguaje natural a partir del catálogo disponible.
* Diseñar una arquitectura limpia por capas que desacople la interfaz, la lógica de negocio y el acceso a datos, facilitando el mantenimiento y la realización de pruebas automatizadas.
* Diseñar una interfaz gráfica intuitiva en JavaFX que distinga con claridad la vista de tienda, el área de "Mi Biblioteca" y las herramientas exclusivas del administrador.

### 6.2.4. Usuarios objetivo
* **Usuario / Cliente:** Jugador que utiliza la aplicación para explorar el catálogo digital de videojuegos. Puede realizar búsquedas semánticas mediante IA, adquirir claves para propiedad definitiva, contratar alquileres temporales por semanas, consultar las fechas de caducidad de sus accesos activos desde su sección "Mi Biblioteca" y acceder a su historial de compras y puntos de fidelidad. No tiene permisos para alterar precios, inventario ni configuraciones del sistema.
* **Administrador / Gestor:** Responsable de la plataforma con privilegios de gestión total sobre la aplicación. Cuenta con paneles y controles específicos en la interfaz gráfica (invisibles para el usuario común) para dar de alta títulos, cargar paquetes de claves digitales, modificar precios de venta y tarifas semanales de alquiler, supervisar métricas de ingresos y administrar las cuentas registradas.

---

## 6.3. Alcance del Proyecto

### 6.3.1. Dentro del alcance
* Autenticación y registro local de usuarios (Clientes) y administradores mediante contraseñas cifradas con algoritmo de hashing seguro.
* Gestión completa del catálogo de videojuegos (alta, modificación, consulta y baja lógica) por parte del administrador.
* Gestión del inventario de claves digitales ficticias, permitiendo la carga de lotes de códigos y controlando su estado (`DISPONIBLE`, `ASIGNADA` de forma permanente o `EN_ALQUILER` temporal).
* **Módulo de Tienda:** catálogo visual interactivo para la compra definitiva de títulos o la contratación de licencias temporales por semanas.
* **Módulo "Mi Biblioteca":** panel personal del cliente donde visualiza los juegos adquiridos, supervisa el tiempo restante de sus alquileres activos mediante contadores y tramita extensiones/renovaciones semanales.
* **Control automatizado de caducidad:** revocación desatendida del acceso al videojuego al expirar el periodo de alquiler contratado sin renovación.
* **Sistema de reservas:** registro de solicitudes en lista de espera cuando un título agota su stock de claves, con asignación prioritaria automática al ingresar nuevos códigos.
* **Asistencia de Inteligencia Artificial mediante API externa:**
  * Autocompletado de la ficha técnica de videojuegos (sinopsis, género y clasificación PEGI) a partir del título para el administrador.
  * Buscador semántico en lenguaje natural que recomienda títulos del catálogo a partir de preferencias descriptivas del cliente.

### 6.3.2. Fuera del alcance
* Integración con pasarelas de pago telemático reales (los cobros se registrarán de forma simulada mediante confirmación directa o saldo virtual ficticio).
* Descarga, instalación o ejecución de archivos binarios ejecutables de los videojuegos reales (la aplicación valida y custodia la licencia/acceso, no actúa como cliente de descarga de datos masivos).
* Sincronización o vinculación de cuentas con plataformas externas reales (Steam, Epic Games Store, GOG).
* Tienda web accesible por navegador o sincronización multitienda en la nube (el sistema funcionará como aplicación de escritorio local monousuario/cliente-servidor local).
* Asistente conversacional de chat abierto (chatbot flotante con memoria continua de diálogo).

---

## 6.4. Requisitos funcionales
* **RF-01 - Gestión de catálogo de videojuegos:** El sistema permitirá al administrador dar de alta, consultar, modificar y dar de baja lógica títulos en el catálogo, definiendo título, género, clasificación PEGI, precio de compra definitiva y tarifa de alquiler semanal.
* **RF-02 - Gestión del almacén de claves digitales:** El sistema permitirá al administrador cargar y custodiar lotes de claves de activación internas, gestionando de forma automática su estado (disponible, asignada en propiedad o en alquiler temporal).
* **RF-03 - Autocompletado de fichas técnicas con IA:** El sistema permitirá al administrador consultar una API externa de IA para autocompletar la sinopsis comercial, el género principal y la edad recomendada (PEGI) a partir del título del videojuego introducido.
* **RF-04 - Búsqueda semántica con IA:** El sistema permitirá a los clientes realizar consultas en lenguaje natural (ej. *"juego de rol por turnos relajante"*) para que la IA filtre y recomiende los títulos más afines del catálogo disponible.
* **RF-05 - Registro y gestión de usuarios:** El sistema permitirá el autorregistro e inicio de sesión de clientes, almacenando sus credenciales cifradas, datos de contacto, saldo/puntos acumulados y estado de cuenta.
* **RF-06 - Adquisición permanente de licencias:** El sistema permitirá al cliente procesar la compra definitiva de un videojuego, asignándole una clave única de inventario y vinculando el título a su biblioteca personal de forma permanente.
* **RF-07 - Contratación y revocación de alquileres temporales:** El sistema permitirá al cliente alquilar un videojuego por semanas tasadas. La plataforma calculará la fecha de vencimiento, habilitará el acceso temporal en su biblioteca y revocará automáticamente el permiso si el usuario no abona una renovación al concluir el plazo.
* **RF-08 - Panel "Mi Biblioteca":** El sistema dispondrá de un espacio personal para el cliente donde visualizará todos sus títulos disponibles, identificando si son de propiedad definitiva o alquiler temporal, mostrando en estos últimos un contador de días restantes y la opción de extender el alquiler.
* **RF-09 - Gestión de cola de reservas:** El sistema permitirá a los clientes apuntarse a una lista de espera cuando un título no disponga de claves libres, asignando automáticamente la licencia al primer usuario en cola en cuanto el administrador reponga existencias.
* **RF-10 - Control de acceso y roles:** El sistema restringirá el acceso a las funciones de administración (gestión de stock de claves, alta de títulos y métricas globales) según el rol autenticado (Cliente o Administrador).

---

## 6.5. Requisitos no funcionales
* **RNF-01 - Seguridad en credenciales:** Las contraseñas de las cuentas de usuario y administradores nunca se almacenarán en texto claro en la base de datos; deberán procesarse mediante un algoritmo de hashing robusto unidireccional con salting (como BCrypt).
* **RNF-02 - Rendimiento y tiempo de respuesta:** Las consultas de catálogo, filtrado de biblioteca local y comprobación de claves deberán completarse y representarse en la interfaz gráfica en menos de 1 segundo en condiciones normales de funcionamiento local.
* **RNF-03 - Integridad transaccional (ACID):** Todas las operaciones compuestas que involucren cambios en múltiples registros (por ejemplo, registrar una transacción de compra, cambiar el estado de una clave a 'asignada' y vincular el juego a la biblioteca del cliente) deberán ejecutarse bajo una transacción atómica mediante JDBC para evitar estados inconsistentes o pérdida de claves.
* **RNF-04 - Mantenibilidad y arquitectura desacoplada:** El código fuente se estructurará siguiendo una arquitectura en capas estricta (Presentación JavaFX, Lógica de Negocio/Servicios y Persistencia DAO), garantizando que las reglas de negocio sean independientes de la interfaz gráfica y faciliten la implementación de pruebas automatizadas.
* **RNF-05 - Tolerancia a fallos en servicios externos (IA):** Las llamadas HTTP a la API externa de IA se ejecutarán de forma asíncrona o con un tiempo de espera límite (*timeout* máximo de 4 segundos). Si el servicio no responde o se pierde la conexión a internet, la aplicación capturará la excepción sin bloquear la interfaz: en la catalogación permitirá el alta manual de datos y en la tienda ofrecerá el filtrado estándar por texto y género.
* **RNF-06 - Usabilidad y claridad visual:** La interfaz de usuario deberá ofrecer retroalimentación visual inmediata sobre el estado de las licencias en "Mi Biblioteca", mostrando de forma intuitiva los días restantes de los alquileres activos mediante etiquetas o barras de estado diferenciadas por color.

---

## 6.6. Reglas de negocio
* **RN-01 (Límite de licencias temporales simultáneas):** Un usuario no podrá mantener activos más de 2 alquileres temporales al mismo tiempo, garantizando la rotación del inventario de claves entre los miembros de la plataforma.
* **RN-02 (Cómputo, suspensión de acceso y recargo por demora):** Los alquileres se computan en periodos semanales exactos (7 días naturales). Al cumplirse la fecha límite sin haber abonado la prórroga, el acceso al juego queda automáticamente suspendido en "Mi Biblioteca". Si el usuario solicita reactivar la licencia dentro del periodo de cortesía posterior al vencimiento, se le aplicará un recargo por mora de 1,50 € por cada día natural transcurrido fuera de plazo adicional a la cuota semanal.
* **RN-03 (Bloqueo y liberación de clave por impago prolongado):** Si transcurren más de 3 días naturales en estado de suspensión por retraso sin que el usuario liquide la tarifa de reactivación y sus recargos, la clave digital se desvincula de su cuenta, vuelve a estar disponible para el público o para la cola de reservas, y la cuenta del cliente queda temporalmente restringida para tramitar nuevos alquileres.
* **RN-04 (Prioridad estricta en cola de reservas):** Al liberarse una clave (por caducidad de alquiler) o al ingresar un nuevo lote por parte del administrador, la clave se asignará automáticamente al primer cliente en espera según orden de solicitud (FIFO), bloqueando su compra al público general.
* **RN-05 (Canje de puntos de fidelización):** Por cada compra definitiva o alquiler realizado, el usuario acumulará puntos (1 punto por cada euro gastado). Al alcanzar 100 puntos, podrá canjearlos por un descuento directo de 5,00 € aplicable a cualquier transacción dentro de la tienda.
* **RN-06 (Restricción de duplicidad en biblioteca):** Un usuario no podrá adquirir ni alquilar un videojuego si ya posee una licencia activa (permanente o temporal) de ese mismo título en su biblioteca personal.

---

## 6.7. Casos de Uso Generales

### 6.7.1. Actores del sistema
* **Cliente (Usuario):** Jugador registrado que accede a la plataforma para explorar el catálogo digital, realizar búsquedas semánticas asistidas por IA, comprar licencias permanentes, contratar alquileres semanales, gestionar sus accesos desde el panel "Mi Biblioteca" (renovaciones o pagos de recargos por demora) y apuntarse a colas de reserva cuando un título agota sus claves.
* **Administrador:** Responsable de la plataforma con acceso a las funciones de gestión interna. Posee privilegios para dar de alta y editar videojuegos apoyándose en el autocompletado por IA, cargar lotes de claves digitales ficticias en el inventario, fijar precios de venta y tarifas semanales, y auditar las transacciones globales.

### 6.7.2. Tabla general de casos de uso

| ID | Caso de uso | Actor principal | Descripción |
| :--- | :--- | :--- | :--- |
| **CU-01** | Iniciar sesión / Registro | Cliente / Administrador | Valida las credenciales cifradas del usuario y carga la interfaz correspondiente a su rol. |
| **CU-02** | Catalogar videojuego con IA y cargar claves | Administrador | Da de alta un título autocompletando su ficha técnica mediante la API de IA e inyecta un lote de claves digitales en el almacén. |
| **CU-03** | Contratar alquiler temporal | Cliente | Procesa el alquiler por semanas de un videojuego, asignando una clave temporal con fecha de caducidad a "Mi Biblioteca". |
| **CU-04** | Prorrogar o reactivar alquiler en Biblioteca | Cliente | Extiende las semanas de una licencia activa o reactiva un alquiler vencido en plazo de cortesía. |
| **CU-05** | Reservar título sin claves disponibles | Cliente | Inscribe al usuario en la cola de espera (FIFO) de un juego agotado para asignarle la primera clave que quede libre. |
| **CU-06** | Comprar licencia permanente | Cliente | Efectúa la adquisición definitiva de un videojuego, descontando una clave del stock, vinculándola para siempre a su biblioteca y sumando puntos. |
| **CU-07** | Buscar juegos con IA semántica | Cliente | Envía una descripción en lenguaje natural a la API de IA para recibir recomendaciones personalizadas del catálogo. |

---

## 6.8. Especificación detallada de casos de uso

### CU-03: Contratar alquiler temporal
* **Actor principal:** Cliente (Usuario registrado)
* **Objetivo:** Formalizar el alquiler temporal de un videojuego por semanas tasadas, asignando una clave digital activa al panel "Mi Biblioteca" del usuario.
* **Precondiciones:**
  * El cliente ha iniciado sesión en la plataforma.
  * El videojuego existe en el catálogo activo y cuenta con al menos una clave digital en estado “DISPONIBLE”.
* **Flujo principal:**
  1. El cliente explora el catálogo de la tienda y selecciona un videojuego.
  2. El cliente elige la modalidad "Alquilar por semanas" e indica el número de semanas deseadas.
  3. El sistema verifica en tiempo real que el cliente no supere el límite de 2 alquileres activos simultáneos (RN-01), que no posea ya ese título en su biblioteca (RN-06) y que su cuenta no esté bloqueada por impagos previos (RN-03).
  4. El sistema comprueba en la base de datos la disponibilidad de claves libres en el inventario digital para ese título.
  5. El sistema calcula la fecha y hora exacta de vencimiento (bloques de 7 días naturales por semana) y muestra el importe total de la operación (aplicando descuento por puntos si el usuario decide canjearlos según RN-05).
  6. El cliente confirma la transacción de alquiler.
  7. El sistema ejecuta una transacción atómica: asigna una clave digital cambiándola a estado "EN_ALQUILER", registra la operación comercial, vincula el título a la sección "Mi Biblioteca" con su contador de tiempo activo y suma los puntos de fidelidad correspondientes.
* **Flujos alternativos:**
  * **FA-01 (Cancelación por el usuario):** El cliente cancela la operación en la ventana de confirmación antes de procesar el cobro; el sistema descarta el proceso y no altera el estado de ninguna clave.
* **Excepciones:**
  * **E-01 (Cupo de alquileres excedido, título duplicado o cuenta restringida):** El sistema muestra un aviso en pantalla indicando que el usuario ya tiene 2 alquileres activos, ya posee el juego o tiene una restricción por mora; la operación queda bloqueada.
  * **E-02 (Sin claves disponibles en inventario):** El sistema notifica que todas las licencias del título están ocupadas y habilita el botón para inscribirse en la cola de reservas (CU-05).
  * **E-03 (Error de persistencia en base de datos):** Si ocurre un fallo SQL durante el registro, se ejecuta un rollback automático para garantizar que la clave siga disponible y no se genere un cargo fantasma.
* **Postcondiciones:**
  * Una clave digital del inventario pasa de "DISPONIBLE" a "EN_ALQUILER".
  * El videojuego aparece habilitado en "Mi Biblioteca" del cliente con la fecha límite de caducidad programada.

---

### CU-04: Prorrogar o reactivar alquiler en Biblioteca (y revocación por vencimiento)
* **Actor principal:** Cliente (y Sistema de forma automatizada al comprobar vencimientos).
* **Objetivo:** Extender la vigencia de una licencia temporal activa, reactivar una licencia suspendida abonando el recargo por demora dentro del plazo de cortesía, o revocar definitivamente la clave si se supera el límite de impago.
* **Precondiciones:**
  * El cliente está autenticado en la aplicación.
  * Existe un registro de alquiler asociado al cliente en su sección "Mi Biblioteca" (en estado "ACTIVO" o "SUSPENDIDO").
* **Flujo principal (Prórroga dentro de plazo):**
  1. El cliente accede a su panel "Mi Biblioteca", donde visualiza sus juegos alquilados y el contador de días restantes.
  2. El cliente selecciona un título cuyo alquiler sigue en vigor (demora = 0 días) y pulsa en "Extender alquiler".
  3. El cliente selecciona la cantidad de semanas adicionales que desea contratar.
  4. El sistema calcula la nueva fecha de caducidad sumando 7 días naturales por cada semana contratada a la fecha límite actual y muestra el importe estándar sin recargos.
  5. El cliente confirma el abono de la renovación.
  6. El sistema actualiza la fecha de vencimiento de la licencia, mantiene la misma clave asignada y suma los puntos de fidelidad generados.
* **Flujos alternativos:**
  * **FA-01 (Reactivación con recargo durante el periodo de cortesía):** Al entrar a "Mi Biblioteca", el sistema detecta que la fecha límite ha vencido hace menos de 3 días naturales. La licencia aparece con el acceso bloqueado ("SUSPENDIDO"). Si el cliente pulsa "Reactivar licencia", el sistema calcula los días naturales de retraso, suma el recargo fijo de 1,50 € por día de retraso (RN-02) a la tarifa semanal y solicita confirmación. Una vez abonado, el juego vuelve a estado "ACTIVO".
  * **FA-02 (Revocación definitiva por impago prolongado y asignación a reservas):** Si transcurren más de 3 días naturales desde el vencimiento sin que el cliente renueve (RN-03), el sistema revoca automáticamente la licencia: desvincula el juego de la biblioteca del usuario, restringe su cuenta para nuevos alquileres y libera la clave. Acto seguido, comprueba si existen clientes en la cola de reservas para ese título (RN-04): si hay lista de espera, asigna la clave de inmediato al primero de la fila; en caso contrario, la clave vuelve al estado "DISPONIBLE" en la tienda.
* **Excepciones:**
  * **E-01 (Intento de prórroga sobre licencia ya revocada):** Si el cliente intenta renovar cuando ya han pasado más de 3 días de retraso y la clave ha sido liberada (CL-02), el sistema informa de que la licencia expiró definitivamente y debe tramitar un nuevo alquiler desde la tienda tras regularizar su cuenta.
* **Postcondiciones:**
  * **Si se renueva o reactiva:** la fecha límite del alquiler se amplía y el acceso al juego permanece habilitado en "Mi Biblioteca".
  * **Si expira el periodo de gracia sin pago:** la licencia queda revocada y la clave pasa al primer usuario en reserva o al inventario libre.

---

## 6.9. Casos límite y situaciones excepcionales
* **CL-01 (Intento de compra o alquiler sin claves disponibles):** El sistema deshabilitará los botones de adquisición/alquiler en la interfaz y validará en la capa de negocio que existan claves en estado 'DISPONIBLE' antes de procesar la operación, ofreciendo en su lugar el botón de acceso a la cola de reservas.
* **CL-02 (Solicitud de prórroga fuera del plazo de cortesía o doble cobro):** Control de estado para impedir que un usuario renueve un alquiler pasados los 3 días de gracia tras el vencimiento (cuando la clave ya ha sido revocada y liberada), así como el bloqueo temporal del botón de pago tras el primer clic para evitar cobros o extensiones duplicadas.
* **CL-03 (Duplicidad de cuentas o claves digitales):** El sistema validará mediante lógica de formulario y restricciones SQL (`UNIQUE`) que no puedan registrarse dos usuarios con el mismo correo electrónico o nombre de usuario, ni inyectarse en el inventario dos claves de activación con el mismo código alfanumérico.
* **CL-04 (Pérdida de conectividad o fallo en la API de IA):** Se establecerá un tiempo de espera máximo (*timeout* de 4 segundos). Si la API externa no responde o no hay conexión a internet, se capturará la excepción (`IOException` / `HttpTimeoutException`), mostrando un aviso no intrusivo: al administrador se le habilitará la edición manual de la ficha y al cliente se le redirigirá al buscador tradicional por filtros de texto y género.
* **CL-05 (Cierre inesperado durante la asignación de licencias):** El manejo de transacciones JDBC mediante `setAutoCommit(false)`, `commit()` y `rollback()` garantizará que, si el programa se cierra o falla a mitad de una compra o alquiler, no queden claves bloqueadas en el limbo ni cobros registrados sin su correspondiente licencia en "Mi Biblioteca".

---

## 6.10. Modelo de Datos

### 6.10.1. Entidades del sistema
* **Videojuego:** Representa los títulos disponibles en el catálogo nativo de la plataforma, sus fichas técnicas, precios de compra y tarifas semanales de alquiler.
* **ClaveDigital:** Representa los códigos de activación individuales e internos asociados a un videojuego de la plataforma, controlando su estado (`DISPONIBLE`, `ASIGNADA` o `EN_ALQUILER`).
* **Cliente:** Almacena la información de los usuarios registrados, sus credenciales cifradas, historial de puntos de fidelidad y estado de su cuenta.
* **Transaccion:** Cabecera de la operación comercial realizada (venta definitiva o contrato de alquiler), fecha, importe total y cliente asociado.
* **LineaTransaccion:** Detalle individual de cada videojuego incluido en una transacción (cantidad y precio aplicado).
* **AlquilerDetalle:** Registro dependiente de la transacción de alquiler para controlar la fecha límite de caducidad, el estado de la licencia (`ACTIVO`, `SUSPENDIDO` o `REVOCADO`) y los recargos acumulados por demora.
* **Reserva:** Registro en lista de espera (FIFO) para clientes que aguardan la liberación de claves de un título agotado.
* **UsuarioSistema:** Credenciales y privilegios exclusivos del rol de Administrador para la gestión global de la plataforma.

### 6.10.2. Atributos principales
* **Videojuego:** `id` (PK), `titulo`, `genero`, `pegi`, `sinopsis`, `precio_venta`, `precio_alquiler_semana`, `activo`.
* **ClaveDigital:** `id` (PK), `videojuego_id` (FK), `codigo_activacion` (UNIQUE), `estado` (`DISPONIBLE` / `ASIGNADA` / `EN_ALQUILER`).
* **Cliente:** `id` (PK), `username` (UNIQUE), `password_hash`, `email` (UNIQUE), `telefono`, `puntos_fidelidad`, `sancionado`.
* **Transaccion:** `id` (PK), `cliente_id` (FK), `usuario_sistema_id` (FK), `fecha_hora`, `tipo` (`VENTA` / `ALQUILER`), `total`.
* **LineaTransaccion:** `id` (PK), `transaccion_id` (FK), `videojuego_id` (FK), `cantidad`, `precio_unitario`.
* **AlquilerDetalle:** `id` (PK), `transaccion_id` (FK, UNIQUE), `clave_digital_id` (FK), `fecha_limite`, `recargo_demora`, `estado_licencia`.
* **Reserva:** `id` (PK), `cliente_id` (FK), `videojuego_id` (FK), `fecha_reserva`, `estado_reserva` (`PENDIENTE` / `COMPLETADA`).
* **UsuarioSistema:** `id` (PK), `username` (UNIQUE), `password_hash`, `rol`.

### 6.10.3 y 6.10.4. Relaciones y cardinalidades
* Un **Videojuego** contiene muchos (`1..*`) códigos en el inventario de **ClaveDigital**; cada **ClaveDigital** pertenece exactamente a un (`1..1`) **Videojuego**.
* Un **Cliente** puede realizar muchas (`0..*`) **Transacciones**; cada **Transaccion** pertenece exactamente a un (`1..1`) **Cliente**.
* Una **Transaccion** contiene una o muchas (`1..*`) **LineaTransacciones**; cada línea referencia exactamente a un (`1..1`) **Videojuego**.
* Una **Transaccion** de tipo alquiler tiene asociado exactamente un (`1..1`) registro de **AlquilerDetalle**, el cual vincula la licencia temporal con su **ClaveDigital** específica.
* Un **Cliente** puede registrar muchas (`0..*`) **Reservas**; cada **Reserva** involucra a un (`1..1`) **Videojuego** de la lista de espera.
* Un **UsuarioSistema** (Administrador) puede supervisar o registrar operaciones y altas en el sistema.

### 6.10.5. Diagrama Entidad-Relación Conceptual

| Entidad Origen | Cardinalidad | Entidad Destino | Tipo de Relación / Descripción |
| :--- | :---: | :--- | :--- |
| **Videojuego** | `1 : N` | **ClaveDigital** | Un videojuego posee múltiples códigos de activación individuales en el inventario. |
| **Cliente** | `1 : N` | **Transaccion** | Un cliente puede realizar múltiples operaciones comerciales a lo largo del tiempo. |
| **Transaccion** | `1 : N` | **LineaTransaccion** | Una transacción comercial contiene una o varias líneas de detalle con los juegos adquiridos. |
| **Transaccion (Alquiler)** | `1 : 1` | **AlquilerDetalle** | Una transacción de alquiler genera un registro satélite exclusivo con fechas y estado de licencia. |
| **Cliente** | `1 : N` | **Reserva** | Un cliente puede apuntarse a varias listas de espera simultáneas para juegos agotados. |
| **Videojuego** | `1 : N` | **Reserva** | Un videojuego agotado agrupa múltiples solicitudes en su cola de espera FIFO. |

---

## 6.11. Arquitectura de la aplicación

* **Capa de Presentación (Presentación / UI):** Construida con JavaFX y archivos FXML, se encarga de la interacción visual con el usuario. Los controladores recogen las acciones realizadas en la interfaz (como pulsar en *"Comprar clave"*, *"Alquilar por semanas"* o *"Consultar Biblioteca"*), muestran notificaciones no intrusivas y delegan el procesamiento real a los servicios inferiores.
* **Capa de Lógica de Negocio (Servicios / Services):** Es el núcleo funcional de la aplicación. Contiene la implementación estricta de las reglas de negocio del sistema (por ejemplo, el control de límite de 2 alquileres simultáneos de la regla **RN-01**, el cómputo de semanas y el recargo de 1,50 € por día de retraso de la **RN-02**, o la priorización FIFO en la cola de reservas de la **RN-04**). Asimismo, integra el cliente HTTP asíncrono para gestionar las consultas a la API de IA con un límite de tiempo (*timeout*) de 4 segundos.
* **Capa de Acceso a Datos (DAO / Repositorios):** Actúa como pasarela intermedia entre la lógica de negocio y la base de datos. Encapsula las sentencias SQL puras ejecutadas mediante JDBC, gestiona el pool de conexiones y asegura la integridad transaccional mediante el control explícito de `setAutoCommit(false)`, asegurando que las operaciones compuestas se ejecuten de manera totalmente atómica o se desagan (`rollback()`) en caso de fallo inesperado.
* **Capa de Persistencia (Base de Datos):** Compuesta por el motor relacional MySQL 8.x, almacena de forma permanente la información estructurada de usuarios, catálogo, lotes de claves digitales, transacciones y listas de espera.

**Justificación técnica:** Esta separación estricta en capas aísla la interfaz gráfica y el motor de almacenamiento. Como resultado, las reglas de negocio y los servicios son completamente independientes de la interfaz de usuario, lo que facilita enormemente el mantenimiento del código fuente y la realización de pruebas unitarias automatizadas.

---

## 6.12. Diseño inicial de clases
* **Videojuego:** Encapsula los atributos técnicos y descriptivos de cada título nativo de la plataforma. Se vincula con el inventario a través de la agregación de instancias de `ClaveDigital`.
* **ClaveDigital:** Modifica su estado de manera dinámica (`DISPONIBLE`, `ASIGNADA`, `EN_ALQUILER`) según las transacciones procesadas.
* **Cliente:** Modela al usuario autenticado, gestiona su saldo acumulado de puntos de fidelización y valida si cumple las condiciones para tramitar nuevos alquileres (`puedeAlquilar()`).
* **Transaccion** y **LineaTransaccion:** Representan de forma atómica la operación comercial (cabecera y desglose), encapsulando el cálculo de importes y subtotales.
* **AlquilerDetalle:** Custodia el ciclo de vida del alquiler temporal y ejecuta el cómputo de recargos por demora (`calcularPenalizacion()`) aplicando 1,50 € por cada día transcurrido tras el vencimiento.
* **Reserva:** Gestiona la posición en cola de espera (FIFO) para títulos que han agotado sus claves disponibles.

---

## 6.13. Diseño de la interfaz de usuario
La interfaz se estructura bajo el paradigma de una plataforma de distribución digital y biblioteca de juegos de escritorio, ofreciendo una experiencia fluida e intuitiva tanto para el jugador como para el administrador a través de tres áreas principales:

1. **Pantalla de Tienda y Catálogo Digital:**
   * Vista en cuadrícula con tarjetas visuales de los títulos disponibles, indicando carátula, género, clasificación PEGI y opciones duales de adquisición: botón de *"Compra definitiva"* y botón de *"Alquiler temporal por semanas"*.
   * Barra superior con buscador en lenguaje natural conectado al motor semántico de IA y filtros tradicionales (género, rango de precio).
   * Panel de confirmación modal: desglosa semanas a contratar, cálculo automático de fecha límite, canje opcional de puntos de fidelidad y aviso de pase a cola de reserva si el título se encuentra agotado.

2. **Pantalla de "Mi Biblioteca" y Gestión de Licencias:**
   * Panel personal del cliente que lista exclusivamente los títulos adquiridos.
   * Segmentación visual clara entre licencias permanentes y temporales. Los alquileres activos muestran un contador decreciente de días restantes con código de semáforo visual (verde: > 2 días restantes; naranja: último día / vence hoy; rojo: suspendido por demora en periodo de cortesía).
   * Acciones contextuales por título: botón *"Extender alquiler"* (dentro de plazo) o *"Reactivar licencia"* (calculando y cobrando el recargo acumulado de 1,50 €/día).

3. **Panel de Administración y Catalogación Asistida:**
   * Entorno con acceso restringido para la gestión del inventario global y catálogo nativo.
   * Formulario de alta y edición de videojuegos asistido por el botón *"Autocompletar con IA"*.