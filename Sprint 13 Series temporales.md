Hola Isaac!

Soy **Patricio Requena** 👋. Es un placer ser el revisor de tu proyecto el día de hoy!

Revisaré tu proyecto detenidamente con el objetivo de ayudarte a mejorar y perfeccionar tus habilidades. Durante mi revisión, identificaré áreas donde puedas hacer mejoras en tu código, señalando específicamente qué y cómo podrías ajustar para optimizar el rendimiento y la claridad de tu proyecto. Además, es importante para mí destacar los aspectos que has manejado excepcionalmente bien. Reconocer tus fortalezas te ayudará a entender qué técnicas y métodos están funcionando a tu favor y cómo puedes aplicarlos en futuras tareas. 

_**Recuerda que al final de este notebook encontrarás un comentario general de mi parte**_, empecemos!

Encontrarás mis comentarios dentro de cajas verdes, amarillas o rojas, ⚠️ **por favor, no muevas, modifiques o borres mis comentarios** ⚠️:


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class=“tocSkip”></a>
Si todo está perfecto.
</div>

<div class="alert alert-block alert-warning">
<b>Comentario del revisor</b> <a class=“tocSkip”></a>
Si tu código está bien pero se puede mejorar o hay algún detalle que le hace falta.
</div>

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class=“tocSkip”></a>
Si de pronto hace falta algo o existe algún problema con tu código o conclusiones.
</div>

Puedes responderme de esta forma:
<div class="alert alert-block alert-info">
<b>Respuesta del estudiante</b> <a class=“tocSkip”></a>
</div>

# Descripción del proyecto

La compañía Sweet Lift Taxi ha recopilado datos históricos sobre pedidos de taxis en los aeropuertos. Para atraer a más conductores durante las horas pico, necesitamos predecir la cantidad de pedidos de taxis para la próxima hora. Construye un modelo para dicha predicción.

La métrica RECM en el conjunto de prueba no debe ser superior a 48.

## Instrucciones del proyecto.

1. Descarga los datos y haz el remuestreo por una hora.
2. Analiza los datos
3. Entrena diferentes modelos con diferentes hiperparámetros. La muestra de prueba debe ser el 10% del conjunto de datos inicial.4. Prueba los datos usando la muestra de prueba y proporciona una conclusión.

## Descripción de los datos

Los datos se almacenan en el archivo `taxi.csv`. 	
El número de pedidos está en la columna `num_orders`.

## Preparación


```python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split, GridSearchCV
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_squared_error
import matplotlib.pyplot as plt
```


```python
data = pd.read_csv('/datasets/taxi.csv')
```


```python
data_sample = data.head()
display(data_sample)
display(data.columns)

```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>datetime</th>
      <th>num_orders</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-03-01 00:00:00</td>
      <td>9</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-03-01 00:10:00</td>
      <td>14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-03-01 00:20:00</td>
      <td>28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-03-01 00:30:00</td>
      <td>20</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018-03-01 00:40:00</td>
      <td>32</td>
    </tr>
  </tbody>
</table>
</div>



    Index(['datetime', 'num_orders'], dtype='object')



```python
data['datetime'] = pd.to_datetime(data['datetime'])
data.set_index('datetime', inplace=True)
data = data.resample('H').sum() 
```

<div class="alert alert-block alert-warning">
<b>Comentario del revisor (1ra Iteracion)</b> <a class=“tocSkip”></a>

Correcto, carga de datos e importación de librerías bien hecha! Recuerda que en lugar de print puedes usar `display()` para mostrar los DataFrames como una tabla en el notebook 
</div>


```python
data.info()

print(data.describe())

print(data.isnull().sum())

```

    <class 'pandas.core.frame.DataFrame'>
    DatetimeIndex: 4416 entries, 2018-03-01 00:00:00 to 2018-08-31 23:00:00
    Freq: H
    Data columns (total 1 columns):
     #   Column      Non-Null Count  Dtype
    ---  ------      --------------  -----
     0   num_orders  4416 non-null   int64
    dtypes: int64(1)
    memory usage: 69.0 KB
            num_orders
    count  4416.000000
    mean     84.422781
    std      45.023853
    min       0.000000
    25%      54.000000
    50%      78.000000
    75%     107.000000
    max     462.000000
    num_orders    0
    dtype: int64



```python
display(data.head())
display(data.tail())

```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>num_orders</th>
    </tr>
    <tr>
      <th>datetime</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-03-01 00:00:00</th>
      <td>124</td>
    </tr>
    <tr>
      <th>2018-03-01 01:00:00</th>
      <td>85</td>
    </tr>
    <tr>
      <th>2018-03-01 02:00:00</th>
      <td>71</td>
    </tr>
    <tr>
      <th>2018-03-01 03:00:00</th>
      <td>66</td>
    </tr>
    <tr>
      <th>2018-03-01 04:00:00</th>
      <td>43</td>
    </tr>
  </tbody>
</table>
</div>



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>num_orders</th>
    </tr>
    <tr>
      <th>datetime</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-31 19:00:00</th>
      <td>136</td>
    </tr>
    <tr>
      <th>2018-08-31 20:00:00</th>
      <td>154</td>
    </tr>
    <tr>
      <th>2018-08-31 21:00:00</th>
      <td>159</td>
    </tr>
    <tr>
      <th>2018-08-31 22:00:00</th>
      <td>223</td>
    </tr>
    <tr>
      <th>2018-08-31 23:00:00</th>
      <td>205</td>
    </tr>
  </tbody>
</table>
</div>



```python
X = data.index.astype(np.int64).values.reshape(-1, 1)  # Convertir datetime a números
y = data['num_orders'].values

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.1, shuffle=False)
```

<div class="alert alert-block alert-danger">
<b>Comentario del revisor (1ra Iteracion)</b> <a class=“tocSkip”></a>

Al ejecutar esta línea `data.set_index('datetime', inplace=True)` estás cambiando la columna datetime a ser el índice, por lo que también estás cambiando todo el dataset en la variable `data` y debido a esto te da un error en la siguiente celda de aquí abajo. Además, como estás cambiando toda la variable `data` no se pueden ejecutar el resto de celdas que dependen de la misma para poder realizar el entrenamiento.
    
    
Para evitar estas situaciones siempre procura reiniciar el kernel de tu notebook y ejecutar todas las celdas desde la primera a la última, así puedes identificar donde tienes errores y puedes compartir tu trabajo a otras personas en tu equipo sin pasar por estos errores.
</div>

## Análisis


```python
param_grid = {
    'n_estimators': [50, 100, 200],
    'max_depth': [10, 15, 20],
    'min_samples_split': [2, 5],
    'min_samples_leaf': [2, 4]
}

rf = RandomForestRegressor(random_state=42)
grid_search_rf = GridSearchCV(estimator=rf, param_grid=param_grid, cv=5, scoring='neg_root_mean_squared_error')
grid_search_rf.fit(X_train, y_train)

```




    GridSearchCV(cv=5, estimator=RandomForestRegressor(random_state=42),
                 param_grid={'max_depth': [10, 15, 20], 'min_samples_leaf': [2, 4],
                             'min_samples_split': [2, 5],
                             'n_estimators': [50, 100, 200]},
                 scoring='neg_root_mean_squared_error')




```python
best_rf_model = grid_search_rf.best_estimator_
y_pred = best_rf_model.predict(X_test)
rmse = mean_squared_error(y_test, y_pred, squared=False)
print(f"Mejores hiperparámetros: {grid_search_rf.best_params_}")
print(f"RECM en el conjunto de prueba: {rmse}")

```

    Mejores hiperparámetros: {'max_depth': 10, 'min_samples_leaf': 4, 'min_samples_split': 2, 'n_estimators': 50}
    RECM en el conjunto de prueba: 64.40930700051098


## Formación

<div class="alert alert-block alert-danger">
<b>Comentario del revisor (1ra Iteracion)</b> <a class=“tocSkip”></a>

La descripción del proyecto te sugiere probar con distintos modelos, y aquí solo estás usando RandomForestRegressor. Te sugiero agregar 1 modelo más para que puedas comparar el desempeño entre los mismos. 
    
Recuerda además que debes obtener un RECM por debajo de 48, en esta iteración no he podido ejecutar tu proyecto pero te dejo el comentario para que lo tengas en cuenta en caso de que no se haya logrado
</div>

## Prueba


```python
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_squared_error


rf_model = RandomForestRegressor(random_state=42)

rf_model.fit(X_train, y_train)

y_pred_rf = rf_model.predict(X_test)

rmse_rf = mean_squared_error(y_test, y_pred_rf, squared=False)
print(f'RECM en el conjunto de prueba con RandomForestRegressor: {rmse_rf}')

```

    RECM en el conjunto de prueba con RandomForestRegressor: 63.776695799871305



```python
from sklearn.ensemble import GradientBoostingRegressor
from sklearn.metrics import mean_squared_error

gb_model = GradientBoostingRegressor(random_state=42)

gb_model.fit(X_train, y_train)

y_pred_gb = gb_model.predict(X_test)

rmse_gb = mean_squared_error(y_test, y_pred_gb, squared=False)
print(f'RECM en el conjunto de prueba con GradientBoostingRegressor: {rmse_gb}')

```

    RECM en el conjunto de prueba con GradientBoostingRegressor: 63.40721322207192



```python
from sklearn.model_selection import cross_val_score

# Validación cruzada para RandomForestRegressor
cv_scores_rf = cross_val_score(rf_model, X_train, y_train, cv=5, scoring='neg_root_mean_squared_error')
mean_cv_score_rf = -cv_scores_rf.mean()
print(f'Mean RECM con validación cruzada (RandomForestRegressor): {mean_cv_score_rf}')

# Validación cruzada para GradientBoostingRegressor
cv_scores_gb = cross_val_score(gb_model, X_train, y_train, cv=5, scoring='neg_root_mean_squared_error')
mean_cv_score_gb = -cv_scores_gb.mean()
print(f'Mean RECM con validación cruzada (GradientBoostingRegressor): {mean_cv_score_gb}')

```

    Mean RECM con validación cruzada (RandomForestRegressor): 43.50866499665449
    Mean RECM con validación cruzada (GradientBoostingRegressor): 35.34427616279761



```python
from sklearn.metrics import mean_squared_error

# Predecir en el conjunto de prueba con GradientBoostingRegressor
y_pred_gb = gb_model.predict(X_test)

# Calcular el RECM en el conjunto de prueba
rmse_gb_test = mean_squared_error(y_test, y_pred_gb, squared=False)
print(f'RECM en el conjunto de prueba con GradientBoostingRegressor: {rmse_gb_test}')

```

    RECM en el conjunto de prueba con GradientBoostingRegressor: 63.40721322207192



```python
from sklearn.model_selection import RandomizedSearchCV
from sklearn.ensemble import GradientBoostingRegressor
from scipy.stats import uniform, randint


gb_model = GradientBoostingRegressor(random_state=42)

param_dist = {
    'n_estimators': randint(50, 200),
    'learning_rate': uniform(0.01, 0.2),
    'max_depth': randint(2, 5),
    'min_samples_split': randint(2, 10),
    'min_samples_leaf': randint(1, 4)
}

random_search = RandomizedSearchCV(estimator=gb_model, param_distributions=param_dist, 
                                   n_iter=20, cv=5, scoring='neg_root_mean_squared_error', 
                                   random_state=42, n_jobs=-1)

random_search.fit(X_train, y_train)

best_params = random_search.best_params_
print(f'Mejores hiperparámetros: {best_params}')

best_model = random_search.best_estimator_
y_pred_best = best_model.predict(X_test)
rmse_best = mean_squared_error(y_test, y_pred_best, squared=False)
print(f'RECM en el conjunto de prueba con el mejor GradientBoostingRegressor: {rmse_best}')

```

    Mejores hiperparámetros: {'learning_rate': 0.01687770422304368, 'max_depth': 3, 'min_samples_leaf': 1, 'min_samples_split': 5, 'n_estimators': 99}
    RECM en el conjunto de prueba con el mejor GradientBoostingRegressor: 61.34489392315117



```python
from sklearn.model_selection import RandomizedSearchCV
from sklearn.ensemble import RandomForestRegressor
from scipy.stats import randint

rf_model = RandomForestRegressor(random_state=42)

param_dist = {
    'n_estimators': randint(100, 300),  # Ajustamos el rango para n_estimators
    'max_depth': randint(5, 20),        # Rango más amplio para la profundidad del árbol
    'min_samples_split': randint(2, 10),
    'min_samples_leaf': randint(1, 4),
    'max_features': ['auto', 'sqrt', 'log2']  # Probar diferentes estrategias de selección de características
}

random_search_rf = RandomizedSearchCV(estimator=rf_model, param_distributions=param_dist, 
                                      n_iter=20, cv=5, scoring='neg_root_mean_squared_error', 
                                      random_state=42, n_jobs=-1)

random_search_rf.fit(X_train, y_train)

best_params_rf = random_search_rf.best_params_
print(f'Mejores hiperparámetros (RandomForestRegressor): {best_params_rf}')

best_rf_model = random_search_rf.best_estimator_
y_pred_rf_best = best_rf_model.predict(X_test)
rmse_rf_best = mean_squared_error(y_test, y_pred_rf_best, squared=False)
print(f'RECM en el conjunto de prueba con el mejor RandomForestRegressor: {rmse_rf_best}')

```

    Mejores hiperparámetros (RandomForestRegressor): {'max_depth': 6, 'max_features': 'sqrt', 'min_samples_leaf': 2, 'min_samples_split': 3, 'n_estimators': 291}
    RECM en el conjunto de prueba con el mejor RandomForestRegressor: 61.441875617015974



```python
from sklearn.ensemble import GradientBoostingRegressor
from sklearn.model_selection import GridSearchCV


gbr_model = GradientBoostingRegressor(random_state=42)

param_grid = {
    'n_estimators': [150, 200, 250],
    'max_depth': [4, 6, 8],
    'min_samples_split': [2, 3, 5],
    'min_samples_leaf': [1, 2, 3],
    'learning_rate': [0.01, 0.05, 0.1],
    'subsample': [0.8, 1.0]
}

grid_search_gbr = GridSearchCV(estimator=gbr_model, param_grid=param_grid, 
                               scoring='neg_root_mean_squared_error', cv=5, n_jobs=-1)

grid_search_gbr.fit(X_train, y_train)

best_gbr_model = grid_search_gbr.best_estimator_
print("Mejores hiperparámetros (GradientBoostingRegressor):", grid_search_gbr.best_params_)

y_pred_gbr = best_gbr_model.predict(X_test)
rmse_gbr = mean_squared_error(y_test, y_pred_gbr, squared=False)
print(f'RECM en el conjunto de prueba con el mejor GradientBoostingRegressor: {rmse_gbr}')

```

    Mejores hiperparámetros (GradientBoostingRegressor): {'learning_rate': 0.01, 'max_depth': 4, 'min_samples_leaf': 1, 'min_samples_split': 2, 'n_estimators': 150, 'subsample': 1.0}
    RECM en el conjunto de prueba con el mejor GradientBoostingRegressor: 67.75674404344589


<div class="alert alert-block alert-warning">
<b>Comentario del revisor (2da Iteracion)</b> <a class=“tocSkip”></a>

Muy buen trabajo con la corrección y la prueba de los diferentes modelos! Obtuviste en algunos casos la métrica del RECM por debajo del umbral mencionado en este proyecto. Para tus próximos proyectos relacionados al ML te dejaré estos puntos cómo recomendaciones:
    
- Procura realizar un EDA más detallado de tus datos, debes tener un dataset limpio y sobre todo que lo entiendas para que sepas porque tus modelos puedan dar ciertos resultados
- Al final del proyecto procura redactar tus recomendaciones y conclusiones en cuanto a lo visto en la evaluación de los modelos y los datos que usaste
- Puedes optimizar la cantidad de líneas de código planteado funciones donde tengas procesos similares como el entrenar y evaluar
    
Saludos!
</div>

# Lista de revisión

- [x]  	
Jupyter Notebook está abierto.
- [ ]  El código no tiene errores
- [ ]  Las celdas con el código han sido colocadas en el orden de ejecución.
- [ ]  	
Los datos han sido descargados y preparados.
- [ ]  Se ha realizado el paso 2: los datos han sido analizados
- [ ]  Se entrenó el modelo y se seleccionaron los hiperparámetros
- [ ]  Se han evaluado los modelos. Se expuso una conclusión
- [ ] La *RECM* para el conjunto de prueba no es más de 48
