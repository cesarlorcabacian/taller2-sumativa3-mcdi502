# Taller II · Sumativa 3 — Integración de fuentes heterogéneas con Apache Spark

[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/cesarlorcabacian/taller2-sumativa3-mcdi502/blob/main/mcdi502_s3_grupox.ipynb)

### **Curso:** Gestión de Datos y Tecnologías Big Data (MCDI502) · Universidad Andrés Bello (UNAB) · Semana 3

##### **Grupo:** 6 · **Integrantes:** Fernanda Ovalle Román · Sebastián Cajales Cid · Jorge Álvarez Ossandón · César Lorca Bacian

Pipeline en **Apache Spark 3.5.7 / PySpark** que integra cuatro fuentes heterogéneas, aplica transformaciones y responde 7 consultas con Spark SQL.

## Fuentes y DataFrames (100 registros c/u)

| Fuente | DataFrame | Variables |
|---|---|---|
| OpenMeteo (API) | `df_openmeteo` | temperatura 2m, humedad relativa 2m, precipitación, viento 10m (velocidad y dirección), índice UV |
| AQICN (API) | `df_aqicn` | PM2.5, PM10, O3, NO2, SO2 |
| MongoDB (ESP32) | `df_mongo_bpm` | alturaft, presión atmosférica, monóxido de carbono |
| MySQL vía API REST PHP (ESP32) | `df_mysql_dht` | temperatura_interior, humedad |

## Contenido del notebook
1. Configuración del entorno (Java 8, Spark, conectores, `SparkSession`, `SparkContext`)
2. Ingesta y creación de DataFrames (ID3.1)
3. Preprocesamiento: `altura_metros` (pies × 0.3048) y `condicion_clima` (RA4, ID4.2)
4. Integración: `df_unificado` por índice (`row_number` + `INNER JOIN`), con justificación (RA3)
5. Consultas C1–C7 con Spark SQL sobre tablas temporales (ID3.1, ID4.1)
6. Verificación final

## Cómo ejecutarlo
1. Abrir el notebook en Google Colab (botón superior).
2. En **Secretos 🔑** de Colab crear:
   - `MONGO_URI`: URI de MongoDB entregada por el docente (no se publica en este repo).
   - `AQICN_TOKEN` *(recomendado)*: token gratuito de <https://aqicn.org/data-platform/token/>. Con `demo` la API siempre devuelve Shanghai.
3. *Entorno de ejecución → Ejecutar todo*. La ingesta de AQICN tarda ~2 min.

Para otra ciudad, editar `CIUDAD`, `LATITUD` y `LONGITUD` en la celda 2.0 (por defecto: Santiago de Chile).

## Estructura
```
├── mcdi502_s3_grupox.ipynb   # notebook ejecutable
├── requirements.txt          # dependencias para ejecución local
├── docs/guion_video.md       # guion del video explicativo (7–10 min)
└── README.md
```

## Notas
- Las credenciales se leen desde Secretos/variables de entorno; nunca se versionan.
- La integración es un emparejamiento por secuencia (las fuentes no comparten clave ni reloj); la justificación completa está en la sección 4 del notebook.
- Fuentes: [OpenMeteo](https://open-meteo.com/en/docs) · [AQICN](https://aqicn.org/api/) · [Spark 3.5.7](https://spark.apache.org/docs/3.5.7/) · notebooks base del curso MCDI502.
