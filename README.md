# telecom-analysis
sprint7-final-project

# 📊 Análisis de Comportamiento de Clientes y Consumo — ConnectaTel LATAM

## 🎯 Objetivo del Proyecto
El objetivo de este proyecto es evaluar y analizar el comportamiento de consumo de los clientes de **ConnectaTel**, una empresa de telecomunicaciones en Latinoamérica, considerando los datos registrados **hasta el año 2024**.

A través de un enfoque programático en Python, el análisis abarca la exploración, limpieza, perfilamiento estadístico y segmentación de la base de usuarios. Esto permite:
- **Identificar patrones de consumo** de llamadas y mensajes de texto.
- **Detectar inconsistencias y valores atípicos** en los registros de servicio.
- **Sugerir estrategias de retención de clientes** y optimización de la oferta comercial (planes Básico vs. Premium).

---

## 📁 Datasets Utilizados
El análisis integra tres conjuntos de datos ubicados en la carpeta `datasets/`:

1. **`plans.csv`**: Especificaciones y tarifas de la oferta comercial actual.
   - `plan_name`: Nombre del plan (Básico, Premium).
   - `messages_included`, `gb_per_month`, `minutes_included`: Cuotas incluidas en la tarifa base.
   - `usd_monthly_pay`: Pago mensual en USD.
   - `usd_per_gb`, `usd_per_message`, `usd_per_minute`: Costo de consumos adicionales.

2. **`users_latam.csv`**: Información demográfica y contractual de los clientes.
   - `user_id`: Identificador único del cliente.
   - `first_name`, `last_name`, `age`: Datos personales (incluye valores atípicos a tratar).
   - `city`: Ciudad de residencia en LATAM (ej. Bogotá, CDMX, Medellín, GDL, Cali, MTY).
   - `reg_date`: Fecha de registro/alta.
   - `plan`: Plan contratado.
   - `churn_date`: Fecha de cancelación del servicio (si aplica).

3. **`usage.csv`**: Registro detallado del uso real de servicios de telefonía y mensajería.
   - `id`: Identificador del evento de uso.
   - `user_id`: Identificador del cliente.
   - `type`: Tipo de servicio (`call` para llamadas, `text` para mensajes de texto).
   - `date`: Fecha de la transacción (año 2024).
   - `duration`: Duración de la llamada en minutos (solo aplica a `call`).
   - `length`: Longitud/caracteres del mensaje (solo aplica a `text`).

---

## ⚙️ Etapas del Análisis
El proyecto sigue una estructura secuencial en Jupyter Notebook:

1. **Paso 1: Carga y Exploración Inicial**
   - Lectura de fuentes de datos mediante Pandas.
   - Inspección inicial de dimensiones (`.shape`), tipos de datos y estructuras (`.info()`, `.head()`).

2. **Paso 2: Diagnóstico y Calidad de Datos**
   - **Manejo de nulos**: Identificación de valores faltantes y proporciones por columna.
   - **Detección de Sentinels**: Localización de valores fuera de rango o marcadores (ej. edad `-999`, ciudades desconocidas `?`).
   - **Validación Temporal**: Inspección de fechas inconsistentes o inconsistencias lógicas en años futuros (ej. registros asignados a 2026).

3. **Paso 3: Limpieza y Preprocesamiento de Datos**
   - Imputación de edades inválidas utilizando la mediana.
   - Reemplazo de sentinels (`"?"`) por valores nulos estructurados (`np.nan`).
   - Corrección y estandarización de columnas `datetime`, anulando registros fuera del rango límite (2024).
   - Verificación del comportamiento de nulos tipo **MAR** (*Missing At Random*) en `duration` y `length` según el tipo de servicio (`type`).

4. **Paso 4: Análisis Estadístico y Segmentación** *(Siguientes fases)*
   - Perfilamiento demográfico y geográfico de los usuarios.
   - Análisis de uso de red y métricas agregadas por plan.
   - Identificación de sesgos de consumo y evaluación de riesgo de cancelaciones (*Churn*).

---
