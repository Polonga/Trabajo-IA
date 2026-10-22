# Registro y Evaluación Crítica del uso de Inteligencia Artificial

## 6.15. Registro del uso de inteligencia artificial

| ID | Tarea | Herramienta | Objetivo | Resultado | Decisión tomada |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **IA-01** | Definición de reglas de negocio | ChatGPT / Gemini | Plantear restricciones reales para el flujo de licencias temporales y alquileres. | Sugirió recargos tasados por horas exactas y firma digital de contratos por cada préstamo. | Se simplificó a un cómputo por semanas completas (7 días naturales) con recargo fijo por día de mora (1,50 €/día) para garantizar la viabilidad del desarrollo. |
| **IA-02** | Análisis de casos límite | Gemini | Identificar situaciones de concurrencia y conflicto en la rotación de licencias. | Detectó el conflicto de liberar claves al público general cuando existen usuarios aguardando en cola. | Se incorporó la regla de negocio **RN-04** para priorizar automáticamente la reasignación de claves a la lista de reservas FIFO antes de devolverlas a la tienda. |
| **IA-03** | Revisión del modelo de datos | Claude / Gemini | Evaluar cardinalidades y normalización de compras frente a alquileres. | Propuso una única tabla de transacciones agrupando ventas y alquileres mediante múltiples campos nulos opcionales. | Se rechazó la estructura de tabla única; se diseñó la entidad satélite normalizada `AlquilerDetalle` (relación 1:1) para aislar fechas límite, claves asignadas, estados de licencia y penalizaciones. |
| **IA-04** | Integración de IA en el software | Gemini | Diseñar una funcionalidad asistida por IA útil y viable sin implementar un chatbot complejo. | Planteó asistentes conversacionales abiertos con memoria de diálogo continua o motores pesados locales. | Se seleccionó una integración ligera vía API REST con la API de Google Gemini: autocompletado de fichas técnicas para el administrador y buscador semántico de catálogo para el cliente. |

---

## 6.16. Evaluación crítica del uso de IA

### 6.16.1. ¿En qué tareas te ha resultado útil la IA?
Ha resultado especialmente productiva para contrastar escenarios operativos y detectar casos límite no contemplados inicialmente, tales como la concurrencia entre revocaciones automáticas de licencias por mora y colas de espera FIFO. Asimismo, ha servido de catalizador para agilizar la redacción estructurada de especificaciones formales de casos de uso y la organización modular de los requisitos funcionales y no funcionales.

### 6.16.2. ¿Qué propuestas de la IA has rechazado?
Se descartaron sugerencias que añadían una complejidad técnica desproporcionada para un proyecto individual de ámbito formativo, como implementar un asistente conversacional tipo chatbot flotante con persistencia de contexto, la integración con pasarelas de pago telemático reales (Stripe o PayPal) o la sincronización multi-tienda con plataformas externas como Steam o Epic Games.

### 6.16.3. ¿Has detectado algún error o propuesta inadecuada?
En la fase de diseño relacional, la IA intentó unificar las ventas definitivas y los contratos de alquiler temporal en una única tabla con numerosos campos opcionales nulos. Esto vulneraba las formas normales de bases de datos e introducía inconsistencias operativas graves, como permitir valores nulos en el control de fechas de caducidad o asociar estados de expiración a títulos adquiridos de forma permanente.

### 6.16.4. ¿Qué decisiones has tomado tú directamente?
Se determinó el alcance exacto de la plataforma (sistema nativo de licencias y claves digitales), la elección del stack técnico basado en JavaFX y persistencia directa JDBC con HikariCP frente a frameworks de mayor sobrecarga, la fijación precisa de tarifas y penalizaciones (recargo de 1,50 €/día tras 3 días de gracia) y el diseño de la interfaz orientado a un catálogo digital de escritorio con el panel personal de "Mi Biblioteca".

### 6.16.5. ¿Ha cambiado el diseño inicial de tu proyecto como consecuencia de utilizar IA?
Sí, pero no en su concepto de partida, sino en la profundidad y blindaje de su lógica interna. La idea original siempre fue una plataforma propia e independiente de distribución de licencias digitales. Sin embargo, en las primeras iteraciones la IA malinterpretó el enfoque sugiriendo integraciones con tiendas externas (como Steam) y dinámicas propias de mostrador físico. 

Tras corregir y reconducir a la herramienta hacia un ecosistema cerrado y nativo, la IA resultó clave para evolucionar el sistema: ayudó a diseñar la gestión avanzada de estados para el inventario interno (`ClaveDigital`), estructuró el ciclo de vida del alquiler temporal en "Mi Biblioteca" con suspensiones por mora, e introdujo el sistema de reservas automáticas FIFO ante roturas de stock. Como resultado, el proyecto mantuvo intacta su esencia original, pero ganó una arquitectura técnica y unas reglas de negocio mucho más sólidas y consistentes.