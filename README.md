# Airbnb Global Markets - Proyecto de Limpieza y Transformación de Datos (ETL)

Este repositorio contiene la fase inicial y fundamental de nuestro análisis de datos de Airbnb en múltiples ciudades del mundo. Antes de proceder con el modelado y la creación de visualizaciones o presentaciones, hemos llevado a cabo un proceso exhaustivo de **Extracción, Transformación y Carga (ETL)** utilizando **Power Query** en Power BI para homogeneizar y asegurar la calidad de las fuentes de datos.

El objetivo principal de esta fase ha sido consolidar los datasets independientes de varias ciudades globales en un modelo único, limpio, coherente y optimizado.

---

## 🌍 Ciudades Incluidas
El análisis abarca los mercados de las siguientes ciudades globales:
* 🇪🇸 **Madrid**
* 🇮🇹 **Milán**
* 🇺🇸 **Nueva York**
* 🇦🇺 **Sídney**
* 🇯🇵 **Tokio**
* 🇬🇧 **Londres**

---

## 🛠️ Proceso de Limpieza y Transformación de Datos

Las fuentes de datos originales presentaban diversas inconsistencias típicas de sistemas transaccionales distribuidos: formatos de moneda locales, caracteres especiales corruptos o inconsistentes, valores nulos y estructuras de texto no estandarizadas. 

A continuación, se detallan las principales acciones de transformación aplicadas en **Power Query**:

### 1. Homogeneización y Conversión de Divisas (Euros €)
Dado que cada ciudad reportaba sus métricas financieras (precios, depósitos, tarifas de limpieza) en su moneda local (USD, GBP, AUD, JPY, EUR), fue imprescindible establecer una base monetaria común.
* **Identificación de Monedas:** Se mapeó el origen de cada dataset para aplicar el factor de conversión correspondiente.
* **Cálculo de Conversión:** Se integraron tasas de cambio para transformar de forma precisa los importes locales a **Euros (€)**, garantizando que las comparaciones globales de ingresos y precios sean económicamente válidas.

### 2. Eliminación de Caracteres Especiales y Símbolos
Para poder transformar las columnas de costes en tipos de datos numéricos (Decimal/Entero) y realizar agregaciones matemáticas, se limpiaron los strings de texto:
* Se eliminaron los símbolos de moneda de texto (`$`, `£`, `¥`, etc.).
* Se suprimieron comas de miles y caracteres no numéricos residuales que impedían el tipado correcto de los datos.

### 3. Normalización y Estandarización de Textos
Para evitar la duplicidad de categorías debido a problemas de capitalización o espacios en blanco:
* Se aplicó la función `Text.Proper` en Power Query para homogeneizar nombres de barrios, tipos de propiedades y tipos de habitaciones (asegurando que la primera letra sea mayúscula y el resto minúsculas).
* Se eliminaron espacios en blanco adicionales al inicio y al final de los textos (`Text.Trim`).

### 4. Gestión de Valores Nulos y Datos Faltantes
* Se identificaron columnas críticas con registros vacíos.
* En campos de texto no determinantes se sustituyeron los valores nulos por etiquetas estandarizadas como 0.
* En métricas cuantitativas clave (como puntuaciones de reseñas o tarifas de limpieza), se aplicaron reglas de negocio específicas (por ejemplo, asumir `0` o filtrar filas según correspondiera) para no sesgar los cálculos de los KPIs principales.

### 5. Consolidación y Tipado de Datos
* Se forzó el tipo de datos correcto para cada columna (Moneda/Número Decimal para precios, Entero para IDs y noches mínimas, Texto para dimensiones categóricas, y Fecha para registros temporales).
* Se añadieron columnas personalizadas de origen (como la columna `Ciudad`) en cada tabla individual antes de realizar la anexión para mantener la trazabilidad de los registros en el modelo unificado final.
---

## ✒️ Autores
* **Felix Gonzalez**
* **Noelia Sanchez**
* **M. Ángel Moreno**
