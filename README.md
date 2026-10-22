# Sistema de Gestión de Licencias Digitales de Videojuegos

**Autor:** Pablo Lozano
**Curso:** 2º DAM - Desarrollo de Aplicaciones Multiplataforma
**Fecha:** 10/2026 - 01/2027

## Descripción del Proyecto
Plataforma de escritorio nativa desarrollada en JavaFX para la gestión, venta y alquiler temporal de licencias y claves digitales de videojuegos. El sistema integra reglas de negocio avanzadas (suspensión de licencias, recargos por mora de 1,50 €/día y colas de reserva FIFO) junto a capacidades de IA para catalogación automática y búsqueda semántica.

## Documentación del Proyecto
Toda la especificación técnica se encuentra organizada en la carpeta `/docs`:

1. [Documento de Análisis y Diseño v1.0](docs/01-analisis-y-diseno-v1.0.md): Requisitos, Alcance, Reglas de Negocio, Casos de Uso, Modelo de Datos, Arquitectura y Stack Tecnológico.
2. [Registro y Evaluación Crítica del uso de IA](docs/02-registro-y-evaluacion-ia.md): Tabla de tareas apoyadas por IA y evaluación crítica del proceso.

## Stack Tecnológico
* **Lenguaje:** Java 17/21 LTS
* **Interfaz:** JavaFX 21 + Scene Builder
* **Base de Datos:** MySQL 8.0
* **Persistencia:** JDBC directo + HikariCP
* **IA:** API REST de Google Gemini
* **Seguridad:** BCrypt para credenciales
