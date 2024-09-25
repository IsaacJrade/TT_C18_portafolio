¡Hola!

Mi nombre es Tonatiuh Cruz. Me complace revisar tu proyecto hoy.

Al identificar cualquier error inicialmente, simplemente los destacaré. Te animo a localizar y abordar los problemas de forma independiente como parte de tu preparación para un rol como data-scientist. En un entorno profesional, tu líder de equipo seguiría un enfoque similar. Si encuentras la tarea desafiante, proporcionaré una pista más específica en la próxima iteración.

Encontrarás mis comentarios a continuación - **por favor no los muevas, modifiques o elimines**.

Puedes encontrar mis comentarios en cajas verdes, amarillas o rojas como esta:

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Éxito. Todo está hecho correctamente.
</div>

<div class="alert alert-block alert-warning">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Observaciones. Algunas recomendaciones.
</div>

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Necesita corrección. El bloque requiere algunas correcciones. El trabajo no puede ser aceptado con comentarios en rojo.
</div>

Puedes responderme utilizando esto:

<div class="alert alert-block alert-info">
<b>Respuesta del estudiante.</b> <a class="tocSkip"></a>
</div>


```python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
import matplotlib.pyplot as plt
import seaborn as sns
```


```python
geo_data_0 = pd.read_csv('geo_data_0.csv')
geo_data_1 = pd.read_csv('geo_data_1.csv')
geo_data_2 = pd.read_csv('geo_data_2.csv')

```


```python
print(geo_data_0.head())
print(geo_data_1.head())
print(geo_data_2.head())

print(geo_data_0.info())
print(geo_data_1.info())
print(geo_data_2.info())

```

          id        f0        f1        f2     product
    0  txEyH  0.705745 -0.497823  1.221170  105.280062
    1  2acmU  1.334711 -0.340164  4.365080   73.037750
    2  409Wp  1.022732  0.151990  1.419926   85.265647
    3  iJLyR -0.032172  0.139033  2.978566  168.620776
    4  Xdl7t  1.988431  0.155413  4.751769  154.036647
          id         f0         f1        f2     product
    0  kBEdx -15.001348  -8.276000 -0.005876    3.179103
    1  62mP7  14.272088  -3.475083  0.999183   26.953261
    2  vyE1P   6.263187  -5.948386  5.001160  134.766305
    3  KcrkZ -13.081196 -11.506057  4.999415  137.945408
    4  AHL4O  12.702195  -8.147433  5.004363  134.766305
          id        f0        f1        f2     product
    0  fwXo0 -1.146987  0.963328 -0.828965   27.758673
    1  WJtFt  0.262778  0.269839 -2.530187   56.069697
    2  ovLUW  0.194587  0.289035 -5.586433   62.871910
    3  q6cA6  2.236060 -0.553760  0.930038  114.572842
    4  WPMUX -0.515993  1.716266  5.899011  149.600746
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 100000 entries, 0 to 99999
    Data columns (total 5 columns):
     #   Column   Non-Null Count   Dtype  
    ---  ------   --------------   -----  
     0   id       100000 non-null  object 
     1   f0       100000 non-null  float64
     2   f1       100000 non-null  float64
     3   f2       100000 non-null  float64
     4   product  100000 non-null  float64
    dtypes: float64(4), object(1)
    memory usage: 3.8+ MB
    None
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 100000 entries, 0 to 99999
    Data columns (total 5 columns):
     #   Column   Non-Null Count   Dtype  
    ---  ------   --------------   -----  
     0   id       100000 non-null  object 
     1   f0       100000 non-null  float64
     2   f1       100000 non-null  float64
     3   f2       100000 non-null  float64
     4   product  100000 non-null  float64
    dtypes: float64(4), object(1)
    memory usage: 3.8+ MB
    None
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 100000 entries, 0 to 99999
    Data columns (total 5 columns):
     #   Column   Non-Null Count   Dtype  
    ---  ------   --------------   -----  
     0   id       100000 non-null  object 
     1   f0       100000 non-null  float64
     2   f1       100000 non-null  float64
     3   f2       100000 non-null  float64
     4   product  100000 non-null  float64
    dtypes: float64(4), object(1)
    memory usage: 3.8+ MB
    None


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Buena exploración inicial de los datos. En este punto ya tienes una idea general de cómo están distribuidos los datos de las diferentes regiones.
</div>

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Solamente te recomiendo hacer un análisis de registros duplicados y valores nulos, así como de outliers
</div>


```python
print(f"Duplicados en geo_data_0: {geo_data_0.duplicated().sum()}")
print(f"Duplicados en geo_data_1: {geo_data_1.duplicated().sum()}")
print(f"Duplicados en geo_data_2: {geo_data_2.duplicated().sum()}")

```

    Duplicados en geo_data_0: 0
    Duplicados en geo_data_1: 0
    Duplicados en geo_data_2: 0



```python
print(f"Valores nulos en geo_data_0:\n{geo_data_0.isnull().sum()}")
print(f"Valores nulos en geo_data_1:\n{geo_data_1.isnull().sum()}")
print(f"Valores nulos en geo_data_2:\n{geo_data_2.isnull().sum()}")

```

    Valores nulos en geo_data_0:
    id         0
    f0         0
    f1         0
    f2         0
    product    0
    dtype: int64
    Valores nulos en geo_data_1:
    id         0
    f0         0
    f1         0
    f2         0
    product    0
    dtype: int64
    Valores nulos en geo_data_2:
    id         0
    f0         0
    f1         0
    f2         0
    product    0
    dtype: int64



```python
def detectar_outliers(df, columna):
    Q1 = df[columna].quantile(0.25)
    Q3 = df[columna].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR
    outliers = df[(df[columna] < lower_bound) | (df[columna] > upper_bound)]
    return outliers

for columna in ['f0', 'f1', 'f2', 'product']:
    outliers_geo_data_0 = detectar_outliers(geo_data_0, columna)
    outliers_geo_data_1 = detectar_outliers(geo_data_1, columna)
    outliers_geo_data_2 = detectar_outliers(geo_data_2, columna)
    
    print(f"Outliers en geo_data_0 para la columna {columna}: {len(outliers_geo_data_0)} registros")
    print(f"Outliers en geo_data_1 para la columna {columna}: {len(outliers_geo_data_1)} registros")
    print(f"Outliers en geo_data_2 para la columna {columna}: {len(outliers_geo_data_2)} registros")
    print()

```

    Outliers en geo_data_0 para la columna f0: 0 registros
    Outliers en geo_data_1 para la columna f0: 1 registros
    Outliers en geo_data_2 para la columna f0: 733 registros
    
    Outliers en geo_data_0 para la columna f1: 0 registros
    Outliers en geo_data_1 para la columna f1: 636 registros
    Outliers en geo_data_2 para la columna f1: 684 registros
    
    Outliers en geo_data_0 para la columna f2: 506 registros
    Outliers en geo_data_1 para la columna f2: 0 registros
    Outliers en geo_data_2 para la columna f2: 584 registros
    
    Outliers en geo_data_0 para la columna product: 0 registros
    Outliers en geo_data_1 para la columna product: 0 registros
    Outliers en geo_data_2 para la columna product: 0 registros
    



```python
file_paths = ['geo_data_0.csv', 'geo_data_1.csv', 'geo_data_2.csv']

results = {}

for file_path in file_paths:
    
    data = pd.read_csv(file_path)
    
    
    print(f"Datos cargados de {file_path}:")
    print(data.head())
    
    
    features = data.drop(columns=['id', 'product'])
    target = data['product']
    
    
    features_train, features_valid, target_train, target_valid = train_test_split(
        features, target, test_size=0.25, random_state=42
    )
    
    
    model = LinearRegression()
    model.fit(features_train, target_train)
    
    
    predictions_valid = model.predict(features_valid)
    
    
    rmse = mean_squared_error(target_valid, predictions_valid, squared=False)
    mean_predicted_reserves = np.mean(predictions_valid)
    
    
    results[file_path] = {
        'RMSE': rmse,
        'Mean Predicted Reserves': mean_predicted_reserves
    }
    
    
    print(f"Resultados para {file_path}:")
    print(f"RMSE: {rmse}")
    print(f"Volumen medio de reservas predicho: {mean_predicted_reserves}\n")


print("Resultados para todas las regiones:")
for file_path, metrics in results.items():
    print(f"{file_path}: RMSE = {metrics['RMSE']}, Volumen medio de reservas predicho = {metrics['Mean Predicted Reserves']}")

```

    Datos cargados de geo_data_0.csv:
          id        f0        f1        f2     product
    0  txEyH  0.705745 -0.497823  1.221170  105.280062
    1  2acmU  1.334711 -0.340164  4.365080   73.037750
    2  409Wp  1.022732  0.151990  1.419926   85.265647
    3  iJLyR -0.032172  0.139033  2.978566  168.620776
    4  Xdl7t  1.988431  0.155413  4.751769  154.036647
    Resultados para geo_data_0.csv:
    RMSE: 37.756600350261685
    Volumen medio de reservas predicho: 92.3987999065777
    
    Datos cargados de geo_data_1.csv:
          id         f0         f1        f2     product
    0  kBEdx -15.001348  -8.276000 -0.005876    3.179103
    1  62mP7  14.272088  -3.475083  0.999183   26.953261
    2  vyE1P   6.263187  -5.948386  5.001160  134.766305
    3  KcrkZ -13.081196 -11.506057  4.999415  137.945408
    4  AHL4O  12.702195  -8.147433  5.004363  134.766305
    Resultados para geo_data_1.csv:
    RMSE: 0.890280100102884
    Volumen medio de reservas predicho: 68.71287803913762
    
    Datos cargados de geo_data_2.csv:
          id        f0        f1        f2     product
    0  fwXo0 -1.146987  0.963328 -0.828965   27.758673
    1  WJtFt  0.262778  0.269839 -2.530187   56.069697
    2  ovLUW  0.194587  0.289035 -5.586433   62.871910
    3  q6cA6  2.236060 -0.553760  0.930038  114.572842
    4  WPMUX -0.515993  1.716266  5.899011  149.600746
    Resultados para geo_data_2.csv:
    RMSE: 40.14587231134218
    Volumen medio de reservas predicho: 94.77102387765939
    
    Resultados para todas las regiones:
    geo_data_0.csv: RMSE = 37.756600350261685, Volumen medio de reservas predicho = 92.3987999065777
    geo_data_1.csv: RMSE = 0.890280100102884, Volumen medio de reservas predicho = 68.71287803913762
    geo_data_2.csv: RMSE = 40.14587231134218, Volumen medio de reservas predicho = 94.77102387765939


# Observaciones sobre el rendimiento del modelo en cada región

## geo_data_0.csv
- **RMSE**: 37.76
- **Volumen medio de reservas predicho**: 92.40

  Observación: El modelo tiene un error cuadrático medio relativamente alto, pero el volumen medio de reservas predicho es bastante alto.

## geo_data_1.csv
- **RMSE**: 0.89
- **Volumen medio de reservas predicho**: 68.71

  Observación: El modelo muestra un muy bajo RMSE, indicando una alta precisión. Sin embargo, el volumen medio de reservas predicho es el más bajo de las tres regiones.

## geo_data_2.csv
- **RMSE**: 40.15
- **Volumen medio de reservas predicho**: 94.77

  Observación: El modelo tiene un alto RMSE, lo que sugiere una menor precisión en las predicciones. El volumen medio de reservas predicho es alto, pero el error es significativo.

# Conclusión
La región `geo_data_1.csv` muestra el mejor desempeño en términos de precisión del modelo (bajo RMSE), aunque el volumen medio de reservas es el más bajo. La región `geo_data_2.csv` tiene un volumen de reservas alto pero con un alto RMSE, indicando menor precisión. `geo_data_0.csv` ofrece un equilibrio moderado entre el volumen de reservas y el error del modelo.


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Implementaste el modelo de regresión logística de forma excelente para los 3 conjuntos de datos! En este punto ya puedes obervar cuál es el modelo con el mayor $R^2$ y menor RMSE. A pesar de que la elección de la región 1 pareciera ser muy clara por estas dos métricas, su volumen es significativamente menor al de las otras regiones. Debido a esto es necesario realizar unos cuántos análisis más.
</div>


```python

budget = 100_000_000  # 100 millones de dólares
num_wells = 200
price_per_barrel = 4.5  # Ingresos por barril en USD
volume_per_unit = 4500  # Unidades por cada mil barriles

required_revenue_per_well = budget / num_wells  # en dólares
required_volume_per_well = required_revenue_per_well / (price_per_barrel * volume_per_unit)  # en miles de barriles

results = {
    'geo_data_0.csv': 92.40,
    'geo_data_1.csv': 68.71,
    'geo_data_2.csv': 94.77
}

print(f"Volumen mínimo requerido por pozo: {required_volume_per_well:.2f} miles de barriles")

for file_path, mean_volume in results.items():
    if mean_volume >= required_volume_per_well:
        print(f"{file_path}: Cumple con el criterio de viabilidad económica.")
    else:
        print(f"{file_path}: No cumple con el criterio de viabilidad económica.")

```

    Volumen mínimo requerido por pozo: 24.69 miles de barriles
    geo_data_0.csv: Cumple con el criterio de viabilidad económica.
    geo_data_1.csv: Cumple con el criterio de viabilidad económica.
    geo_data_2.csv: Cumple con el criterio de viabilidad económica.


# Observaciones sobre la viabilidad económica de las regiones

## Volumen mínimo requerido por pozo
- **Volumen mínimo necesario**: 24.69 miles de barriles

## Resultados por región

### geo_data_0.csv
- **Volumen medio de reservas predicho**: 92.40 miles de barriles
- **Estado**: Cumple con el criterio de viabilidad económica.

### geo_data_1.csv
- **Volumen medio de reservas predicho**: 68.71 miles de barriles
- **Estado**: Cumple con el criterio de viabilidad económica.

### geo_data_2.csv
- **Volumen medio de reservas predicho**: 94.77 miles de barriles
- **Estado**: Cumple con el criterio de viabilidad económica.

# Conclusión
Todas las regiones cumplen con el criterio de viabilidad económica, ya que el volumen medio de reservas predicho en cada una supera el mínimo requerido de 24.69 miles de barriles por pozo. 




```python
BUDGET = 100_000_000  # 100 millones de dólares
BARREL_INCOME = 4.5  # Ingreso por barril de materia prima en dólares
PRODUCT_UNIT_INCOME = 4500  # Ingreso por unidad de producto en dólares

def calculate_profit(predictions, actual_reserves):
    top_200_indexes = predictions.nlargest(200).index
    top_200_reserves = actual_reserves.loc[top_200_indexes]
    total_reserves = top_200_reserves.sum()
    profit = total_reserves * PRODUCT_UNIT_INCOME
    return profit

file_paths = ['/datasets/geo_data_0.csv', '/datasets/geo_data_1.csv', '/datasets/geo_data_2.csv']
dfs = [pd.read_csv(file_path) for file_path in file_paths]

for i, df in enumerate(dfs):
    features = df[['f0', 'f1', 'f2']]
    target = df['product']
    
    
    model = LinearRegression()
    model.fit(features, target)
    
    
    predictions = model.predict(features)
    df['predictions'] = predictions
    
    
    df_predictions = pd.Series(predictions, index=df.index)
    df_actual_reserves = df['product']
    profit = calculate_profit(df_predictions, df_actual_reserves)
    
    
    print(f"Resultados para geo_data_{i}.csv:")
    print(f"Ganancia potencial: ${profit:,.2f}")
    print()

```

    Resultados para geo_data_0.csv:
    Ganancia potencial: $134,923,324.80
    
    Resultados para geo_data_1.csv:
    Ganancia potencial: $124,150,866.97
    
    Resultados para geo_data_2.csv:
    Ganancia potencial: $126,038,138.61
    


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Muy bien calculado el beneficio bruto de las 3 regiones! Estos cálculos te ayudarán en la elección de la mejor región teniendo en cuenta también los beneficios brutos según las predicciones, pero a pesar de que el beneficio bruto sea mayor en tu conjunto data2, es necesario comprobar los riesgos que implica.
</div>



# Conclusiones sobre la ganancia potencial para cada región


## Análisis

1. **Región geo_data_0.csv** tiene la ganancia potencial más alta, superando a las otras dos regiones. Esto indica que, a partir de las predicciones de reservas, esta región tiene el mayor beneficio potencial al seleccionar los 200 pozos con las reservas más altas.

2. **Región geo_data_1.csv** y **geo_data_2.csv** también cumplen con los criterios de viabilidad económica, pero sus ganancias potenciales son menores comparadas con la región geo_data_0.csv.

## Recomendación

Basado en el análisis de ganancias potenciales, **geo_data_0.csv** es la región recomendada para el desarrollo de los nuevos pozos petroleros. Esta región ofrece el mayor beneficio potencial con las reservas estimadas, lo que la hace la mejor opción para maximizar el retorno de la inversión.




```python
from sklearn.utils import resample
import numpy as np
import pandas as pd
from sklearn.linear_model import LinearRegression

N_BOOTSTRAPS = 1000  
BUDGET = 100_000_000  
PRODUCT_UNIT_INCOME = 4500  


def calculate_profit(predictions, actual_reserves):
    top_200_indexes = predictions.nlargest(200).index
    top_200_reserves = actual_reserves.loc[top_200_indexes]
    total_reserves = top_200_reserves.sum()
    profit = total_reserves * PRODUCT_UNIT_INCOME
    return profit


def bootstrap_profit(df, n_bootstraps):
    profits = []
    for _ in range(n_bootstraps):
        sample_df = resample(df)
        sample_predictions = sample_df['predictions']
        sample_reserves = sample_df['product']
        profit = calculate_profit(pd.Series(sample_predictions, index=sample_df.index), sample_reserves)
        profits.append(profit)
    return profits


file_paths = ['/datasets/geo_data_0.csv', '/datasets/geo_data_1.csv', '/datasets/geo_data_2.csv']
dfs = [pd.read_csv(file_path) for file_path in file_paths]


for i, df in enumerate(dfs):
    features = df[['f0', 'f1', 'f2']]
    target = df['product']
    
    
    model = LinearRegression()
    model.fit(features, target)
    
    
    predictions = model.predict(features)
    df['predictions'] = predictions
    
    
    profits = bootstrap_profit(df, N_BOOTSTRAPS)
    
    
    mean_profit = np.mean(profits)
    lower_bound = np.percentile(profits, 2.5)
    upper_bound = np.percentile(profits, 97.5)
    risk_of_loss = np.mean(np.array(profits) < BUDGET)
    
    
    print(f"Resultados para geo_data_{i}.csv:")
    print(f"Beneficio promedio: ${mean_profit:,.2f}")
    print(f"Intervalo de confianza del 95%: (${lower_bound:,.2f}, ${upper_bound:,.2f})")
    print(f"Riesgo de pérdidas: {risk_of_loss * 100:.2f}%")
    print()
```

    Resultados para geo_data_0.csv:
    Beneficio promedio: $269,312,188.57
    Intervalo de confianza del 95%: ($242,257,044.15, $301,893,733.59)
    Riesgo de pérdidas: 0.00%
    


Conclusiones Finales
Beneficios y Riesgos para Cada Región

geo_data_0.csv:


Beneficio promedio: $270,061,985.06

Intervalo de confianza del 95%: ($241,380,715.86, $303,962,156.80)

Riesgo de pérdidas: 0.00%

geo_data_1.csv:


Beneficio promedio: $248,423,401.78

Intervalo de confianza del 95%: ($219,747,034.53, $280,596,478.20)

Riesgo de pérdidas: 0.00%

geo_data_2.csv:


Beneficio promedio: $251,855,684.92

Intervalo de confianza del 95%: ($221,098,760.90, $285,684,304.23)

Riesgo de pérdidas: 0.00%


Recomendación

Región con el mayor beneficio promedio: geo_data_0.csv

Riesgo de pérdidas en todas las regiones: 0.00% (ninguna región presenta riesgo de pérdidas)


Decisión Final

La Región geo_data_0 es la más recomendable para el desarrollo de nuevos pozos de petróleo, ya que ofrece el mayor beneficio promedio y no presenta riesgo de pérdidas. Aunque todas las regiones cumplen con los criterios de viabilidad económica y tienen un riesgo de pérdidas nulo, geo_data_0 se destaca por su beneficio promedio superior.

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Excelente trabajo calculando el beneficio promedio, los intervalos de confianza del 95% y el riesgo de pérdidas. El uso de percentiles para los intervalos de confianza es una muy buena práctica este tipo de análisis. Tus cálculos están bien fundamentados y proporcionan información valiosa sobre el rendimiento de las simulaciones de bootstrap.
</div>


