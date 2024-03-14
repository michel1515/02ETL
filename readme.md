# Práctica 2 ETL

## Objetivo

Realizar un ETL con un dataset que contiene información sobre las emisiones de CO2 por país.

## Carga de datos

Primero, cargaremos el archivo CSV. Es importante variar el parámetro `sep` para encontrar el carácter más adecuado para realizar la carga.

```python
import pandas as pd

df = pd.read_csv('Emisiones_CO2.csv', encoding = 'latin-1', sep=',')
```

## Visualización del DataFrame

Después de cargar los datos, es útil visualizar el DataFrame para entender mejor la estructura de los datos.

```python
df.head()
```

## Limpieza de datos

En este caso, mantener los registros nulos no aporta información, por lo que los eliminaremos. Sin embargo, es importante recordar que no se deben eliminar los nulos como regla a menos que estos no afecten la data.

```python
df = df.dropna()
```

La columna 'CO2 (kt)' contiene valores numéricos enteros, pero debemos retirar las comas y puntos (que representan miles y millones) para posteriormente convertirlo a dato de tipo entero.

```python
df['CO2 (kt)'] = df['CO2 (kt)'].str.replace(',', '').str.replace('.', '').astype(int)
```

La columna 'CO2 per cápita (toneladas métricas)' contiene datos tipo float, pero debemos reemplazar la coma por punto para convertir posteriormente a float.

```python
df['CO2 per cápita (toneladas métricas)'] = df['CO2 per cápita (toneladas métricas)'].str.replace(',', '.').astype(float)
```

## Análisis de datos

Finalmente, realizaremos un análisis de los datos con `df.describe()` y buscaremos valores atípicos.
Ingresa comentarios de tus observaciones y ejecuta multiples celdas de codigo en donde explores la data

```python
df.describe()
```

## Guarda el DataFrame en  formato CSV

Alamacena la data limpia en un nuevo CSV con el nombre Emisiones_CO2_V2.csv

```python
df.to_csv('Emisiones_CO2_V2.csv')
```