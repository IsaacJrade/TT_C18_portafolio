¡ Hola Isaac! Como te va?

Mi nombre es Facundo Lozano! Ya he tenido el agrado de revisar otros proyectos tuyos, nuevamente seré tu revisor en este proyecto.

Como siempre, a continuación un poco sobre la modalidad de revisión que usaremos:

Cuando enccuentro un error por primera vez, simplemente lo señalaré, te dejaré encontrarlo y arreglarlo tú cuenta. Además, a lo largo del texto iré haciendo algunas observaciones sobre mejora en tu código y también haré comentarios sobre tus percepciones sobre el tema. Pero si aún no puedes realizar esta tarea, te daré una pista más precisa en la próxima iteración y también algunos ejemplos prácticos. Estaré abierto a comentarios y discusiones sobre el tema.

Encontrará mis comentarios a continuación: no los mueva, modifique ni elimine.

Puedes encontrar mis comentarios en cuadros verdes, amarillos o rojos como este:


<div class="alert alert-block alert-success">
<b>Comentario del revisor.</b> <a class="tocSkip"></a>

Exito. Todo se ha hecho de forma exitosa.
</div>

<div class="alert alert-block alert-warning">
<b>Comentario del revisor.</b> <a class="tocSkip"></a>

Observación. Algunas recomendaciones.
</div>

<div class="alert alert-block alert-danger">

<b>Comentario del revisor.</b> <a class="tocSkip"></a>

Necesita arreglos. Este apartado necesita algunas correcciones. El trabajo no puede ser aceptado con comentarios rojos. 
</div>

Puedes responder utilizando esto:

<div class="alert alert-block alert-info">
<b>Respuesta de estudiante.</b> <a class="tocSkip"></a>
</div>

El servicio de venta de autos usados Rusty Bargain está desarrollando una aplicación para atraer nuevos clientes. Gracias a esa app, puedes averiguar rápidamente el valor de mercado de tu coche. Tienes acceso al historial: especificaciones técnicas, versiones de equipamiento y precios. Tienes que crear un modelo que determine el valor de mercado.
A Rusty Bargain le interesa:
- la calidad de la predicción;
- la velocidad de la predicción;
- el tiempo requerido para el entrenamiento

<div class="alert alert-block alert-success">
<b>Review General. (Iteración 2) </b> <a class="tocSkip"></a>

Hola Isaac! Felicitaciones porque has corregido los detalles marcados en nuestra iteración anterior. Ahora si este proyecto está en total condiciones de ser aprobado, bien hecho!
    
Éxitos en tu camino dentro del mundo de los datos y saludos!

<div class="alert alert-block alert-success">
<b>Review General. (Iteración 1) </b> <a class="tocSkip"></a>

Isaac, como siempre, me tomo este tiempo al inicio del proyecto para comentar mis apreciaciones generales de esta primera iteración de la entrega. 

Siempre me gusta comenzar dando la bienvenida al mundo de los datos a los estudiantes, te deseo lo mejor y espero que consigas lograr tus objetivos. Personalmente siempre me gusta brindar el siguiente consejo, "Está bien equivocarse, es normal y es lo mejor que te puede pasar. Aprendemos de los errores y eso te hará mejor programando ya que podrás descubrir cosas a medida que avances y son estas cosas las que te darán esa experiencia para ser mejor como Data Scientist"
    
Ahora si yendo a esta notebook.  Hola Isaac, felicitaciones porque hemos hecho un trabajo conciso que pasa por casi todos los puntos que debíamos pasar, es un trabajo directo y bien implementado aunque tenemos un detalle que corregir junto a recomendaciones para mejorarlo aún más.
    
Lo reenvío para que podamos modificar esto :) éxitos y saludos!

## Preparación de datos


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.ensemble import RandomForestRegressor
from sklearn.tree import DecisionTreeRegressor
from sklearn.metrics import mean_squared_error
import lightgbm as lgb
import catboost as cb
import xgboost as xgb
import time



```


```python
file_path = '/datasets/car_data.csv'
df = pd.read_csv(file_path)

print(df.head())

print(df.isnull().sum())

print(df.info())
```

            DateCrawled  Price VehicleType  RegistrationYear Gearbox  Power  \
    0  24/03/2016 11:52    480         NaN              1993  manual      0   
    1  24/03/2016 10:58  18300       coupe              2011  manual    190   
    2  14/03/2016 12:52   9800         suv              2004    auto    163   
    3  17/03/2016 16:54   1500       small              2001  manual     75   
    4  31/03/2016 17:25   3600       small              2008  manual     69   
    
       Model  Mileage  RegistrationMonth  FuelType       Brand NotRepaired  \
    0   golf   150000                  0    petrol  volkswagen         NaN   
    1    NaN   125000                  5  gasoline        audi         yes   
    2  grand   125000                  8  gasoline        jeep         NaN   
    3   golf   150000                  6    petrol  volkswagen          no   
    4  fabia    90000                  7  gasoline       skoda          no   
    
            DateCreated  NumberOfPictures  PostalCode          LastSeen  
    0  24/03/2016 00:00                 0       70435  07/04/2016 03:16  
    1  24/03/2016 00:00                 0       66954  07/04/2016 01:46  
    2  14/03/2016 00:00                 0       90480  05/04/2016 12:47  
    3  17/03/2016 00:00                 0       91074  17/03/2016 17:40  
    4  31/03/2016 00:00                 0       60437  06/04/2016 10:17  
    DateCrawled              0
    Price                    0
    VehicleType          37490
    RegistrationYear         0
    Gearbox              19833
    Power                    0
    Model                19705
    Mileage                  0
    RegistrationMonth        0
    FuelType             32895
    Brand                    0
    NotRepaired          71154
    DateCreated              0
    NumberOfPictures         0
    PostalCode               0
    LastSeen                 0
    dtype: int64
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 354369 entries, 0 to 354368
    Data columns (total 16 columns):
     #   Column             Non-Null Count   Dtype 
    ---  ------             --------------   ----- 
     0   DateCrawled        354369 non-null  object
     1   Price              354369 non-null  int64 
     2   VehicleType        316879 non-null  object
     3   RegistrationYear   354369 non-null  int64 
     4   Gearbox            334536 non-null  object
     5   Power              354369 non-null  int64 
     6   Model              334664 non-null  object
     7   Mileage            354369 non-null  int64 
     8   RegistrationMonth  354369 non-null  int64 
     9   FuelType           321474 non-null  object
     10  Brand              354369 non-null  object
     11  NotRepaired        283215 non-null  object
     12  DateCreated        354369 non-null  object
     13  NumberOfPictures   354369 non-null  int64 
     14  PostalCode         354369 non-null  int64 
     15  LastSeen           354369 non-null  object
    dtypes: int64(7), object(9)
    memory usage: 43.3+ MB
    None



```python
print("Tamaño del dataset:", df.shape)

print(df.describe(include='all'))
```

    Tamaño del dataset: (354369, 16)
                 DateCrawled          Price VehicleType  RegistrationYear Gearbox  \
    count             354369  354369.000000      316879     354369.000000  334536   
    unique             15470            NaN           8               NaN       2   
    top     05/03/2016 14:25            NaN       sedan               NaN  manual   
    freq                  66            NaN       91457               NaN  268251   
    mean                 NaN    4416.656776         NaN       2004.234448     NaN   
    std                  NaN    4514.158514         NaN         90.227958     NaN   
    min                  NaN       0.000000         NaN       1000.000000     NaN   
    25%                  NaN    1050.000000         NaN       1999.000000     NaN   
    50%                  NaN    2700.000000         NaN       2003.000000     NaN   
    75%                  NaN    6400.000000         NaN       2008.000000     NaN   
    max                  NaN   20000.000000         NaN       9999.000000     NaN   
    
                    Power   Model        Mileage  RegistrationMonth FuelType  \
    count   354369.000000  334664  354369.000000      354369.000000   321474   
    unique            NaN     250            NaN                NaN        7   
    top               NaN    golf            NaN                NaN   petrol   
    freq              NaN   29232            NaN                NaN   216352   
    mean       110.094337     NaN  128211.172535           5.714645      NaN   
    std        189.850405     NaN   37905.341530           3.726421      NaN   
    min          0.000000     NaN    5000.000000           0.000000      NaN   
    25%         69.000000     NaN  125000.000000           3.000000      NaN   
    50%        105.000000     NaN  150000.000000           6.000000      NaN   
    75%        143.000000     NaN  150000.000000           9.000000      NaN   
    max      20000.000000     NaN  150000.000000          12.000000      NaN   
    
                 Brand NotRepaired       DateCreated  NumberOfPictures  \
    count       354369      283215            354369          354369.0   
    unique          40           2               109               NaN   
    top     volkswagen          no  03/04/2016 00:00               NaN   
    freq         77013      247161             13719               NaN   
    mean           NaN         NaN               NaN               0.0   
    std            NaN         NaN               NaN               0.0   
    min            NaN         NaN               NaN               0.0   
    25%            NaN         NaN               NaN               0.0   
    50%            NaN         NaN               NaN               0.0   
    75%            NaN         NaN               NaN               0.0   
    max            NaN         NaN               NaN               0.0   
    
               PostalCode          LastSeen  
    count   354369.000000            354369  
    unique            NaN             18592  
    top               NaN  07/04/2016 07:16  
    freq              NaN               654  
    mean     50508.689087               NaN  
    std      25783.096248               NaN  
    min       1067.000000               NaN  
    25%      30165.000000               NaN  
    50%      49413.000000               NaN  
    75%      71083.000000               NaN  
    max      99998.000000               NaN  



```python
print(df['RegistrationYear'].describe())

```

    count    354369.000000
    mean       2004.234448
    std          90.227958
    min        1000.000000
    25%        1999.000000
    50%        2003.000000
    75%        2008.000000
    max        9999.000000
    Name: RegistrationYear, dtype: float64



```python
lower_percentile = df['RegistrationYear'].quantile(0.01)
upper_percentile = df['RegistrationYear'].quantile(0.99)

print(f"1% Percentil: {lower_percentile}")
print(f"99% Percentil: {upper_percentile}")

df_filtered = df[(df['RegistrationYear'] >= lower_percentile) & (df['RegistrationYear'] <= upper_percentile)]

print("Tamaño del dataset después de filtrar outliers:", df_filtered.shape)

```

    1% Percentil: 1980.0
    99% Percentil: 2018.0
    Tamaño del dataset después de filtrar outliers: (350787, 16)



```python
print(df_filtered['RegistrationYear'].describe())

```

    count    350787.000000
    mean       2003.421911
    std           6.610245
    min        1980.000000
    25%        1999.000000
    50%        2003.000000
    75%        2008.000000
    max        2018.000000
    Name: RegistrationYear, dtype: float64


<div class="alert alert-block alert-warning">

<b>Comentario del revisor. (Iteración 1)</b> <a class="tocSkip"></a>
    
Excelente Isaac, hasta el momento hemos cargado correctamente los datos separandolos de las importaciones para mitigar posibles errores, a la vez has implementado métodos para visualizar y comprender la composición de nuestros datos. Bien hecho! Como simple detalle te recomendaría separar los pasos en la primera celda, siempre es recomendable a las importaicones y carga de datos tenerlas en celdas separadas.

<div class="alert alert-block alert-success">

<b>Comentario del revisor. (Iteración 1)</b> <a class="tocSkip"></a>
    
Previo a continuar Isaac es importante que profundicemos un poco en nuestros datos tratando de observar valores atipicos que puedan confundir a nuestro modelo. Por ejemplo si velos lo que nos devuelve el método describe() podemos ver que el máximo del año de registro de auto es 9999, algo claramente erroneo, a esto le llamamos outliers. Te receomendaría investigar en las columnas posibles valores outliers, para esto puedes investigar el filtrado a partir de percentiles, tratemos de agregar alguno estilo de estos.
    
    Ahora si impresionante Isaac! Bien hecho!


```python
df = df.drop(columns=['DateCrawled', 'DateCreated', 'LastSeen'])

df_cleaned = df.dropna(subset=['VehicleType', 'Gearbox', 'Model', 'FuelType', 'NotRepaired'])

df_encoded = pd.get_dummies(df_cleaned, columns=['VehicleType', 'Gearbox', 'FuelType', 'Brand', 'Model', 'NotRepaired'])

X = df_encoded.drop('Price', axis=1)
y = df_encoded['Price']

from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

print("Tamaño del conjunto de datos después de la limpieza:", df_cleaned.shape)
print("Tamaño del conjunto de datos después de la codificación:", df_encoded.shape)
print("Tamaño del conjunto de entrenamiento (X_train):", X_train.shape)
print("Tamaño del conjunto de prueba (X_test):", X_test.shape)
print("Tamaño del conjunto de entrenamiento (y_train):", y_train.shape)
print("Tamaño del conjunto de prueba (y_test):", y_test.shape)

```

    Tamaño del conjunto de datos después de la limpieza: (245814, 13)
    Tamaño del conjunto de datos después de la codificación: (245814, 314)
    Tamaño del conjunto de entrenamiento (X_train): (196651, 313)
    Tamaño del conjunto de prueba (X_test): (49163, 313)
    Tamaño del conjunto de entrenamiento (y_train): (196651,)
    Tamaño del conjunto de prueba (y_test): (49163,)


<div class="alert alert-block alert-success">

<b>Comentario del revisor. (Iteración 1)</b> <a class="tocSkip"></a>
    
Respecto a la separación de datos lo hemos hecho perfecto, a la vez veo que hemos eliminado aquellas features que no aportaban valor, hemos quitado algunos nulos y hemos transformado aquellas features categóricas a numéricas mediante get_dummmies(), felicitaciones!
    

## Entrenamiento del modelo 


```python
from sklearn.linear_model import LinearRegression
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import mean_squared_error
import numpy as np
import time


scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

start_time = time.time()
linear_model = LinearRegression()
linear_model.fit(X_train_scaled, y_train)
linear_regression_time = time.time() - start_time

y_pred_linear = linear_model.predict(X_test_scaled)
mse_linear = mean_squared_error(y_test, y_pred_linear)
rmse_linear = np.sqrt(mse_linear)

print(f"Tiempo de entrenamiento para Regresión Lineal: {linear_regression_time:.2f} segundos")
print(f"MSE para Regresión Lineal: {mse_linear:.2f}")
print(f"RMSE para Regresión Lineal: {rmse_linear:.2f}")

```

    Tiempo de entrenamiento para Regresión Lineal: 7.30 segundos
    MSE para Regresión Lineal: 7296826.52
    RMSE para Regresión Lineal: 2701.26



```python
from sklearn.tree import DecisionTreeRegressor
from sklearn.metrics import mean_squared_error
import numpy as np
import time


start_time = time.time()
dt_model = DecisionTreeRegressor(max_depth=10, min_samples_split=10, random_state=42)
dt_model.fit(X_train_scaled, y_train)
dt_time = time.time() - start_time

y_pred_dt = dt_model.predict(X_test_scaled)
mse_dt = mean_squared_error(y_test, y_pred_dt)
rmse_dt = np.sqrt(mse_dt)

print(f"Tiempo de entrenamiento para Árbol de Decisión: {dt_time:.2f} segundos")
print(f"MSE para Árbol de Decisión: {mse_dt:.2f}")
print(f"RMSE para Árbol de Decisión: {rmse_dt:.2f}")

```

    Tiempo de entrenamiento para Árbol de Decisión: 2.41 segundos
    MSE para Árbol de Decisión: 4059286.67
    RMSE para Árbol de Decisión: 2014.77



```python
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_squared_error
import numpy as np
import time


start_time = time.time()
rf_model = RandomForestRegressor(n_estimators=200, max_depth=10, min_samples_split=5, random_state=42)
rf_model.fit(X_train_scaled, y_train)
rf_time = time.time() - start_time

y_pred_rf = rf_model.predict(X_test_scaled)
mse_rf = mean_squared_error(y_test, y_pred_rf)
rmse_rf = np.sqrt(mse_rf)

print(f"Tiempo de entrenamiento para Bosque Aleatorio: {rf_time:.2f} segundos")
print(f"MSE para Bosque Aleatorio: {mse_rf:.2f}")
print(f"RMSE para Bosque Aleatorio: {rmse_rf:.2f}")

```

    Tiempo de entrenamiento para Bosque Aleatorio: 296.94 segundos
    MSE para Bosque Aleatorio: 3649142.82
    RMSE para Bosque Aleatorio: 1910.27



```python
import lightgbm as lgb
from sklearn.metrics import mean_squared_error
import numpy as np
import time


start_time = time.time()
lgb_model = lgb.LGBMRegressor(n_estimators=200, learning_rate=0.1, num_leaves=31, max_depth=10, random_state=42)
lgb_model.fit(X_train_scaled, y_train)
lgb_time = time.time() - start_time

y_pred_lgb = lgb_model.predict(X_test_scaled)
mse_lgb = mean_squared_error(y_test, y_pred_lgb)
rmse_lgb = np.sqrt(mse_lgb)

print(f"Tiempo de entrenamiento para LightGBM: {lgb_time:.2f} segundos")
print(f"MSE para LightGBM: {mse_lgb:.2f}")
print(f"RMSE para LightGBM: {rmse_lgb:.2f}")

```

    Tiempo de entrenamiento para LightGBM: 10.15 segundos
    MSE para LightGBM: 2737847.57
    RMSE para LightGBM: 1654.64



```python
import catboost as cb
from sklearn.metrics import mean_squared_error
import numpy as np
import time

start_time = time.time()
cb_model = cb.CatBoostRegressor(iterations=500, depth=10, learning_rate=0.1, random_seed=42, verbose=0)
cb_model.fit(X_train, y_train)
cb_time = time.time() - start_time

y_pred_cb = cb_model.predict(X_test)
mse_cb = mean_squared_error(y_test, y_pred_cb)
rmse_cb = np.sqrt(mse_cb)

print(f"Tiempo de entrenamiento para CatBoost: {cb_time:.2f} segundos")
print(f"MSE para CatBoost: {mse_cb:.2f}")
print(f"RMSE para CatBoost: {rmse_cb:.2f}")


```

    Tiempo de entrenamiento para CatBoost: 27.03 segundos
    MSE para CatBoost: 2508995.05
    RMSE para CatBoost: 1583.98


<div class="alert alert-block alert-success">

<b>Comentario del revisor. (Iteración 1)</b> <a class="tocSkip"></a>
    
Respecto a los modelos felicitaciones por haber creado una gran cantidad de diferentes variaciones, a la vez una perfecta decisión la de medir sus tiempos y al elegir el mse como métrica!

<div class="alert alert-block alert-warning">

<b>Comentario del revisor. (Iteración 1)</b> <a class="tocSkip"></a>
    
Aquí podríamos mejorar algunos aspectos Isaac, si bien el procedimiento cumple y está correcto podríamos mejorar 2 cosas:
    
    
1. Por un lado te invito que en alguno de los modelos implementes diferentes hiperparametros para poder evaluar el impacto de estos valores en los resultados.
2. Por otro lado lo ideal no sería solo ver el mse sino también el rmse, es decir aplicar la raíz cuadrática al mse para ver un resultado acorde a nuestro problema.

## Análisis del modelo

# Conclusiones


## Modelos más rápidos: Regresión Lineal, Árbol de Decisión, LightGBM.

## Modelos con mejor calidad (menor MSE): Bosque Aleatorio y CatBoost.

## Regresión Lineal tiene un MSE alto pero es rápido en entrenamiento.

## Árbol de Decisión es rápido y tiene un MSE relativamente bajo.

## Bosque Aleatorio ofrece la mejor calidad pero es muy lento en entrenamiento.

## LightGBM es rápido y ofrece una calidad aceptable.

## CatBoost es más lento que LightGBM pero proporciona una buena calidad.

## XGBoost ofrece un MSE moderado con un tiempo de entrenamiento largo.

# Recomendaciones

### Elegir el modelo: Si la prioridad es la velocidad, considera usar Regresión Lineal o LightGBM. Si la prioridad es la calidad, Bosque Aleatorio o CatBoost son opciones a considerar.

# Lista de control

Escribe 'x' para verificar. Luego presiona Shift+Enter

- [x]  Jupyter Notebook está abierto
- [ ]  El código no tiene errores- [ ]  Las celdas con el código han sido colocadas en orden de ejecución- [ ]  Los datos han sido descargados y preparados- [ ]  Los modelos han sido entrenados
- [ ]  Se realizó el análisis de velocidad y calidad de los modelos


```python

```
