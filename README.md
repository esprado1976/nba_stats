# 🏀 NBA Play-by-Play Analytics & Feature Engineering (NBA Finals 2026)

Este proyecto expone un flujo de trabajo analítico en Python para extraer, auditar y visualizar métricas avanzadas de rendimiento a partir del endpoint `PlayByPlayV3` de la API oficial de la NBA, utilizando como caso de estudio el Juego 2 de las Finales entre New York Knicks y San Antonio Spurs.

## 🚀 Desafíos de Datos & Troubleshooting

El objetivo principal mutó de una simple visualización a un proceso de **limpieza y auditoría de datos** debido a las restricciones de diseño del backend de la NBA:

* **Puntos Fantasma (0-0):** Corrección de la lógica de indexación global del partido. Se evitó el sesgo de filtrado previo por equipo para mantener la consistencia de las variables acumuladas (`scoreHome` / `scoreAway`).
* **Ausencia de Variables de Asistencia:** Ante la falta de columnas nativas como `assistPlayerName`, se desarrolló un motor de extracción basado en **Expresiones Regulares (Regex)** sobre el string de la descripción oficial de la jugada.
* **Auditoría de Tiros Libres:** Implementación de filtros lógicos basados en el análisis de texto (`'MISS' not in description`) para asegurar la veracidad de los porcentajes de efectividad.

## 📊 Módulos del Proyecto

El código está estructurado en scripts independientes dentro del notebook para resolver tareas analíticas específicas:

1.  **Progression Shot Charts:** Gráficos de línea por cuadrantes que miden la evolución de la eficiencia (`FG%`, `FT%`, `2PT%`, `3PT%`) de los jugadores con mayor volumen de juego a lo largo de los cuatro cuartos.
2.  **Marcador Continuo:** Línea de tiempo que mapea el ritmo del partido y los quiebres de racha (*runs*).
3.  **Matriz de Flujo de Asistencias (Heatmap):** Un mapa de calor cruzado desarrollado con `Seaborn` que identifica las sociedades de pases de los New York Knicks mediante el parseo de descripciones.
4.  **Custom Box Score:** Un agregador dinámico que compila puntos, asistencias y tasas de conversión en formato clásico (`M-A`) y porcentual por jugador.

## 🛠️ Tecnologías Utilizadas

* **Python 3.12**
* **Pandas:** Manipulación de DataFrames y tablas de contingencia (`crosstab`).
* **Matplotlib & Seaborn:** Diseño de tableros de visualización y mapas de calor.
* **Re (Regular Expressions):** Extracción de datos no estructurados en strings de descripción.
* **NBA API:** Cliente de conexión con los endpoints estadísticos oficiales.
