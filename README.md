# 📊 Movilidad Urbana y Productividad Económica en Ciudades de LATAM y el Mundo — IDB

> *Contexto formativo: Este proyecto forma parte de la ruta de especialización en Data Analysis de TripleTen.*

---

## 1. Resumen Ejecutivo (BLUF)
* **Impacto Directivo:** El análisis unificado de los datos de tráfico en tiempo real de **TomTom Traffic Index** y los indicadores económicos de la **OECD** permite al *Inter-American Development Bank (IDB)* evaluar cómo la congestión urbana y los tiempos de viaje impactan la productividad económica (PIB per cápita y desempleo).
* **Decisión Estratégica:** Se identificó que la congestión vehicular no guarda una correlación lineal directa con la riqueza promedio (*PIB per cápita*), sino que está impulsada fuertemente por la escala poblacional. Sin embargo, metrópolis específicas (como Bogotá y Lima) muestran combinaciones críticas de altos retrasos y menor velocidad de desplazamiento, posicionándose como prioritarias para futuras inversiones en infraestructura de transporte público y movilidad sostenible.

---

## 2. Estructura y Datos del Proyecto
* **Origen de los Datos:** Fuentes combinadas de tráfico en tiempo real y estadísticas económicas urbanas de la OECD.
* **Datasets Utilizados:**
  1. **`tomtom_traffic.csv`**: Registros puntuales de congestión, retrasos totales (`jams_delay`, `mins_delay`), longitud de embotellamientos (`jams_length_in_kms`, `jams_count`) y tiempos actuales vs. históricos por cada 10 km.
  2. **`oecd_city_economy.csv`**: Indicadores anuales de la OECD incluyendo Producto Interno Bruto per cápita (`city_gdp_capita`), porcentaje de desempleo (`unemployment_pct`), contaminación atmosférica (`pm25_ug_m3`) y población total en millones convertida a unidades absolutas (`population`).
* **Nota de Alcance:** El análisis se delimitó y filtró estrictamente al período más reciente y relevante: el año **2024**.
* **Reproducibilidad:** Acceso mediante [Google Colab](https://colab.research.google.com/) y ejecución local mediante clonación de repositorio.

---

## 3. Metodolojiá y Enfoque Analítico
* **Librerías y Herramientas:** `pandas`, `numpy`, `matplotlib`, `seaborn` en entornos Jupyter Notebook / Google Colab.
* **Limpieza y Preparación:** 
  * Estandarización de nombres de columnas a formato `snake_case` y limpieza de caracteres especiales, símbolos porcentuales y unidades (`μ`, `³`, `%`).
  * Conversión de campos de fecha y hora a tipo `datetime` con soporte de zona horaria UTC.
  * Conversión y limpieza de cadenas numéricas monetarias y porcentuales eliminando separadores de miles y sustituyendo comas por puntos decimales.
* **Agregación y Consolidación:** 
  * Agregación de múltiples registros diarios de tráfico por ciudad, país y año mediante promedios anuales (`groupby` + `.mean()`).
  * Unión de los datasets de tráfico y economía mediante un enlace de tipo *inner join* utilizando `city` y `year` como llaves maestras.
* **Análisis Exploratorio y Estadístico:**
  * Evaluación de distribuciones y detección de valores atípicos mediante histogramas y diagramas de caja (*boxplots* optimizados con la instrucción `showmeans=True`).

---

## 4. Descubrimientos y Hallazgos Principales (Core)
* **Desacople entre Riqueza y Congestión:** No existe una relación directa o unívoca que indique que las ciudades con mayor PIB per cápita sufran necesariamente de mayores retrasos por tráfico; el volumen de población y la densidad vehicular pesan significativamente más en la generación de embotellamientos.
* **Outliers Masivos de Tráfico:** *Ciudad de México* lidera drásticamente los niveles de retraso acumulado (`jams_delay`), reflejando la extrema complejidad de su escala metropolitana frente al resto de la muestra analizada.
* **Casos de Alta Eficiencia o Contraste:** Ciudades como Montevideo o Brasilia muestran niveles de productividad competitivos con índices de congestión moderados o bajos, mientras que ciudades críticas como Bogotá y Lima concentran pérdidas sustanciales de tiempo por cada 10 km recorridos.

---

## 5. Limitaciones Metodológicas
* **Ventana Temporal de Tráfico:** Las mediciones de TomTom corresponden al horizonte analizado de 2024, por lo que variaciones estacionales o estructurales de largo plazo podrían no estar completamente capturadas.
* **Heterogeneidad de Límites Urbanos:** Las definiciones geográficas y metropolitanas de las ciudades entre los reportes de la OECD y TomTom pueden presentar diferencias administrativas sutiles.
* **Falta de Variables de Red Vial:** El análisis no incluye la densidad kilométrica de infraestructura vial disponible ni los presupuestos históricos de inversión en transporte público por habitante.

---

## 6. Próximos Pasos Estratégicos
* **Priorización de Inversión IDB:** Canalizar recursos de infraestructura hacia ciudades críticas identificadas (como Bogotá y Lima) para mitigar el impacto negativo de los tiempos de retraso sobre la productividad laboral.
* **Modelado Multivariado:** Incorporar modelos de regresión múltiple y matrices de correlación (como Pearson y Cramer's V) para aislar el peso específico de la población frente al diseño de la red de transporte.
* **Monitoreo Longitudinal:** Ampliar la ingesta de datos a series plurianuales para evaluar la efectividad de las políticas públicas de movilidad urbana a lo largo del tiempo.

---

## 🚀 Cómo Ejecutar el Notebook

### Opción 1: Abrir directamente en Google Colab (Recomendado)
1. Haz clic en o abre [Google Colab](https://colab.research.google.com/).
2. Selecciona la pestaña **GitHub**.
3. Pega la URL de este repositorio y selecciona el archivo `.ipynb`.
4. Ejecuta las celdas secuencialmente presionando `Shift + Enter`.

### Opción 2: Ejecución Local en Jupyter Notebook / VS Code
1. **Clonar el repositorio:**
   ```bash
   git clone [https://github.com/tu-usuario/nombre-del-repositorio.git](https://github.com/tu-usuario/nombre-del-repositorio.git)
   cd nombre-del-repositorio
