📌 Introducción

Este documento describe el proyecto de Sistema de Viajes y Recargas, su diseño de base de datos, las mejoras implementadas y ejemplos de consultas SQL que validan su correcto funcionamiento. Está pensado como guía rápida para desarrolladores y analistas.

🎯 Objetivos Generales

Diseño y normalización de una base de datos relacional que soporte operaciones de recarga y registro de viajes.

Implementar mecanismos de auditoría y histórico para seguimiento de cambios de estado.

Añadir soporte a promociones en recargas, con forma de bonos o descuentos.

Registrar la fuente de validación de cada viaje (dispositivo físico o móvil).

Proponer y añadir una mejora adicional que aporte valor al análisis de la operación.

📂 Estructura de la Base de Datos

USUARIOS: datos personales y fecha de registro.

TARJETAS: relación con usuario, fechas de adquisición y actualización, estado actual.

RECARGAS: monto, fecha, punto de recarga, tarjeta y promoción aplicada.

VIAJES: fecha, estación de abordaje, tarifa y tarjeta usada.

PUNTOS_RECARGA: ubicación y localidad.

ESTACIONES: detalle de estaciones, su localidad y geolocalización.

TARIFAS: valores asociados a cada viaje.

LOCALIDADES: nombres y claves primarias.

🛠 Mejoras Implementadas

1. Auditoría del Estado de Tarjetas

Tabla: tarjeta_auditoria (guarda cambios de estado con sellos de tiempo).

Consultas clave:

Cambios por mes (último año).

Top 5 tarjetas con más movimientos.

2. Promociones en Recargas

Tabla: promociones (nombre, descripción).

Campo añadido: promocion_id en recargas.

Consultas clave:

Recargas con detalle de promoción.

Total recargado por promoción (últimos 3 meses).

Promociones que incluyan “bonus”.

3. Registro de Dispositivos de Validación

Tablas: dispositivos (tipo, ubicación), validaciones (viaje, dispositivo, fecha).

Consultas clave:

Viajes sin validación.

Validaciones por móviles en abril/2025.

Dispositivo con más validaciones.

4. Mejora Adicional: Retroalimentación de Usuarios

Tabla: retroalimentacion (viaje, usuario, rating, comentario, fecha).

Consultas clave:

Promedio de rating por estación.

Top 3 usuarios con más comentarios.

Comentarios que contengan “queja”.

🚀 Población de Datos de Prueba

Se incluyen scripts INSERT con datos de ejemplo para:

Estados de tarjetas (auditoría).

Promociones y recargas.

Dispositivos y validaciones.

Retroalimentación de usuarios.

Estos datos permiten verificar que las consultas arrojan resultados coherentes.

📋 Ejecución de Consultas

Importar el DDL de creación de tablas en PostgreSQL.

Ejecutar los INSERT de datos de ejemplo.

Correr las consultas descritas en la sección de mejoras.

Verificar los resultados y analizar la información.

🔍 Ejemplo de Consulta

-- Top 5 tarjetas con más cambios de estado
SELECT tarjeta_id, COUNT(*) AS cambios
FROM tarjeta_auditoria
GROUP BY tarjeta_id
ORDER BY cambios DESC
LIMIT 5;

📈 Conclusiones

La ampliación del modelo de datos con auditorías, promociones, validaciones y retroalimentación permite:

Trazabilidad completa de cambios y eventos.

Análisis comercial de promociones.

Estadísticas de uso según dispositivo y retroalimentación.

Facilita la toma de decisiones operativas y de negocio.

Este README sirve como base para extender aún más el sistema y adaptarlo a nuevos requerimientos.
