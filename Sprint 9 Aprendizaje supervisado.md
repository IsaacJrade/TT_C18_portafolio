¡ Hola Isaac! Como te va?



 Mi nombre es Facundo Lozano! Ya he tenido el agrado de revisar otros proyectos tuyos, nuevamente seré tu revisor en este proyecto.



Como siempre, a continuación un poco sobre la modalidad de revisión que usaremos:



 Cuando enccuentro un error por primera vez, simplemente lo señalaré, te dejaré encontrarlo y arreglarlo tú cuenta. Además, a lo largo del texto iré haciendo algunas observaciones sobre mejora en tu código y también haré comentarios sobre tus percepciones sobre el tema. Pero si aún no puedes realizar esta tarea, te daré una pista más precisa en la próxima iteración y también algunos ejemplos prácticos. Estaré abierto a comentarios y discusiones sobre el tema.



 Encontrará mis comentarios a continuación: **no los mueva, modifique ni elimine**.



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

<div class="alert alert-block alert-success">
<b>Review General. (Iteración 2) </b> <a class="tocSkip"></a>

Hola Isaac! Felicitaciones porque has corregido los detalles marcados en nuestra iteración anterior. Ahora si este proyecto está en total condiciones de ser aprobado, bien hecho!
    
Éxitos en tu camino dentro del mundo de los datos y saludos!

<div class="alert alert-block alert-success">
<b>Review General. (Iteración 1) </b> <a class="tocSkip"></a>

Isaac, como siempre, me tomo este tiempo al inicio del proyecto para comentar mis apreciaciones generales de esta primera iteración de la entrega.

Siempre me gusta comenzar dando la bienvenida al mundo de los datos a los estudiantes, te deseo lo mejor y espero que consigas lograr tus objetivos. Personalmente siempre me gusta brindar el siguiente consejo, "Está bien equivocarse, es normal y es lo mejor que te puede pasar. Aprendemos de los errores y eso te hará mejor programando ya que podrás descubrir cosas a medida que avances y son estas cosas las que te darán esa experiencia para ser mejor como Data Scientist"
    
Ahora si yendo a esta notebook. Quería felicitarte Isaac porque has realizado la mayoría de las implementaciones necesarisa y se ha notado tu manejo sobre python y las herramientas ML utilizadas. Muy bien hecho! Solo hemos tenido unos detalles pero que no nos deberían demorar tanto corregir.

Espero con ansias a nuestra próxima iteración Isaac, exitos y saludos!


```python
import pandas as pd
```


```python
file_path = '/datasets/Churn.csv'
data = pd.read_csv(file_path)
```


```python
data.head()
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
      <th>RowNumber</th>
      <th>CustomerId</th>
      <th>Surname</th>
      <th>CreditScore</th>
      <th>Geography</th>
      <th>Gender</th>
      <th>Age</th>
      <th>Tenure</th>
      <th>Balance</th>
      <th>NumOfProducts</th>
      <th>HasCrCard</th>
      <th>IsActiveMember</th>
      <th>EstimatedSalary</th>
      <th>Exited</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>15634602</td>
      <td>Hargrave</td>
      <td>619</td>
      <td>France</td>
      <td>Female</td>
      <td>42</td>
      <td>2.0</td>
      <td>0.00</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>101348.88</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>15647311</td>
      <td>Hill</td>
      <td>608</td>
      <td>Spain</td>
      <td>Female</td>
      <td>41</td>
      <td>1.0</td>
      <td>83807.86</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>112542.58</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>15619304</td>
      <td>Onio</td>
      <td>502</td>
      <td>France</td>
      <td>Female</td>
      <td>42</td>
      <td>8.0</td>
      <td>159660.80</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>113931.57</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>15701354</td>
      <td>Boni</td>
      <td>699</td>
      <td>France</td>
      <td>Female</td>
      <td>39</td>
      <td>1.0</td>
      <td>0.00</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>93826.63</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>15737888</td>
      <td>Mitchell</td>
      <td>850</td>
      <td>Spain</td>
      <td>Female</td>
      <td>43</td>
      <td>2.0</td>
      <td>125510.82</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>79084.10</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 10000 entries, 0 to 9999
    Data columns (total 14 columns):
     #   Column           Non-Null Count  Dtype  
    ---  ------           --------------  -----  
     0   RowNumber        10000 non-null  int64  
     1   CustomerId       10000 non-null  int64  
     2   Surname          10000 non-null  object 
     3   CreditScore      10000 non-null  int64  
     4   Geography        10000 non-null  object 
     5   Gender           10000 non-null  object 
     6   Age              10000 non-null  int64  
     7   Tenure           9091 non-null   float64
     8   Balance          10000 non-null  float64
     9   NumOfProducts    10000 non-null  int64  
     10  HasCrCard        10000 non-null  int64  
     11  IsActiveMember   10000 non-null  int64  
     12  EstimatedSalary  10000 non-null  float64
     13  Exited           10000 non-null  int64  
    dtypes: float64(3), int64(8), object(3)
    memory usage: 1.1+ MB



```python
data.describe()
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
      <th>RowNumber</th>
      <th>CustomerId</th>
      <th>CreditScore</th>
      <th>Age</th>
      <th>Tenure</th>
      <th>Balance</th>
      <th>NumOfProducts</th>
      <th>HasCrCard</th>
      <th>IsActiveMember</th>
      <th>EstimatedSalary</th>
      <th>Exited</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>10000.00000</td>
      <td>1.000000e+04</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>9091.000000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.00000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>5000.50000</td>
      <td>1.569094e+07</td>
      <td>650.528800</td>
      <td>38.921800</td>
      <td>4.997690</td>
      <td>76485.889288</td>
      <td>1.530200</td>
      <td>0.70550</td>
      <td>0.515100</td>
      <td>100090.239881</td>
      <td>0.203700</td>
    </tr>
    <tr>
      <th>std</th>
      <td>2886.89568</td>
      <td>7.193619e+04</td>
      <td>96.653299</td>
      <td>10.487806</td>
      <td>2.894723</td>
      <td>62397.405202</td>
      <td>0.581654</td>
      <td>0.45584</td>
      <td>0.499797</td>
      <td>57510.492818</td>
      <td>0.402769</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.00000</td>
      <td>1.556570e+07</td>
      <td>350.000000</td>
      <td>18.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>11.580000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>2500.75000</td>
      <td>1.562853e+07</td>
      <td>584.000000</td>
      <td>32.000000</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>51002.110000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>5000.50000</td>
      <td>1.569074e+07</td>
      <td>652.000000</td>
      <td>37.000000</td>
      <td>5.000000</td>
      <td>97198.540000</td>
      <td>1.000000</td>
      <td>1.00000</td>
      <td>1.000000</td>
      <td>100193.915000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>7500.25000</td>
      <td>1.575323e+07</td>
      <td>718.000000</td>
      <td>44.000000</td>
      <td>7.000000</td>
      <td>127644.240000</td>
      <td>2.000000</td>
      <td>1.00000</td>
      <td>1.000000</td>
      <td>149388.247500</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>10000.00000</td>
      <td>1.581569e+07</td>
      <td>850.000000</td>
      <td>92.000000</td>
      <td>10.000000</td>
      <td>250898.090000</td>
      <td>4.000000</td>
      <td>1.00000</td>
      <td>1.000000</td>
      <td>199992.480000</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.isnull().sum()
```




    RowNumber            0
    CustomerId           0
    Surname              0
    CreditScore          0
    Geography            0
    Gender               0
    Age                  0
    Tenure             909
    Balance              0
    NumOfProducts        0
    HasCrCard            0
    IsActiveMember       0
    EstimatedSalary      0
    Exited               0
    dtype: int64



<div class="alert alert-block alert-success">
<b>Comentario del revisor. (Iteración 1)</b> <a class="tocSkip"></a>

Excelente Isaac! Hasta aquí hemos cargado correctamente los datos y tamibién hemos implementado correctamente los métodos para observar la composición de nuestros datos, bien hecho!


```python
data['Exited'].value_counts(normalize=True)
```




    0    0.7963
    1    0.2037
    Name: Exited, dtype: float64



<div class="alert alert-block alert-success">
<b>Comentario del revisor. (Iteración 1)</b> <a class="tocSkip"></a>

Excelente, tal como debíamos hemos visto el comportamiento del desequilibrio en nuestro problema. Si quisieramos mejorarlo podríamos agregar una gráfica que nos permita ver esto de mejor forma.

###Exploración Inicial de los Datos
##Carga de datos:


#Se han mostrado las primeras cinco filas del conjunto de datos para obtener una idea general de su estructura.
Información de las columnas:

#El conjunto de datos contiene 10,000 filas y 14 columnas.
#Los tipos de datos incluyen enteros (int64), flotantes (float64) y cadenas de caracteres (object).
#La columna Tenure tiene 909 valores faltantes.

##Estadísticas descriptivas:

#La edad promedio de los clientes es aproximadamente 39 años.
#El saldo promedio es de aproximadamente 76,486 unidades monetarias.
#El 51.5% de los clientes son miembros activos.
#El 20.37% de los clientes ha dejado el banco (Exited).

##Valores faltantes:

#La columna Tenure es la única con valores faltantes (909 valores faltantes).

##Distribución de la variable objetivo:

#El 79.63% de los clientes no ha dejado el banco.
#El 20.37% de los clientes ha dejado el banco.


```python
print(data.columns)

data['Tenure'].fillna(data['Tenure'].median(), inplace=True)

from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
numerical_features = ['CreditScore', 'Age', 'Tenure', 'Balance', 'NumOfProducts', 'EstimatedSalary']
data[numerical_features] = scaler.fit_transform(data[numerical_features])


print(data.head())
print(data.info())
print(data.describe())

```

    Index(['RowNumber', 'CustomerId', 'Surname', 'CreditScore', 'Geography',
           'Gender', 'Age', 'Tenure', 'Balance', 'NumOfProducts', 'HasCrCard',
           'IsActiveMember', 'EstimatedSalary', 'Exited'],
          dtype='object')
       RowNumber  CustomerId   Surname  CreditScore Geography  Gender       Age  \
    0          1    15634602  Hargrave    -0.326221    France  Female  0.293517   
    1          2    15647311      Hill    -0.440036     Spain  Female  0.198164   
    2          3    15619304      Onio    -1.536794    France  Female  0.293517   
    3          4    15701354      Boni     0.501521    France  Female  0.007457   
    4          5    15737888  Mitchell     2.063884     Spain  Female  0.388871   
    
         Tenure   Balance  NumOfProducts  HasCrCard  IsActiveMember  \
    0 -1.086246 -1.225848      -0.911583          1               1   
    1 -1.448581  0.117350      -0.911583          0               1   
    2  1.087768  1.333053       2.527057          1               0   
    3 -1.448581 -1.225848       0.807737          0               0   
    4 -1.086246  0.785728      -0.911583          1               1   
    
       EstimatedSalary  Exited  
    0         0.021886       1  
    1         0.216534       0  
    2         0.240687       1  
    3        -0.108918       0  
    4        -0.365276       0  
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 10000 entries, 0 to 9999
    Data columns (total 14 columns):
     #   Column           Non-Null Count  Dtype  
    ---  ------           --------------  -----  
     0   RowNumber        10000 non-null  int64  
     1   CustomerId       10000 non-null  int64  
     2   Surname          10000 non-null  object 
     3   CreditScore      10000 non-null  float64
     4   Geography        10000 non-null  object 
     5   Gender           10000 non-null  object 
     6   Age              10000 non-null  float64
     7   Tenure           10000 non-null  float64
     8   Balance          10000 non-null  float64
     9   NumOfProducts    10000 non-null  float64
     10  HasCrCard        10000 non-null  int64  
     11  IsActiveMember   10000 non-null  int64  
     12  EstimatedSalary  10000 non-null  float64
     13  Exited           10000 non-null  int64  
    dtypes: float64(6), int64(5), object(3)
    memory usage: 1.1+ MB
    None
             RowNumber    CustomerId   CreditScore           Age        Tenure  \
    count  10000.00000  1.000000e+04  1.000000e+04  1.000000e+04  1.000000e+04   
    mean    5000.50000  1.569094e+07 -4.824585e-16  2.318146e-16  1.669775e-16   
    std     2886.89568  7.193619e+04  1.000050e+00  1.000050e+00  1.000050e+00   
    min        1.00000  1.556570e+07 -3.109504e+00 -1.994969e+00 -1.810917e+00   
    25%     2500.75000  1.562853e+07 -6.883586e-01 -6.600185e-01 -7.239103e-01   
    50%     5000.50000  1.569074e+07  1.522218e-02 -1.832505e-01  7.609047e-04   
    75%     7500.25000  1.575323e+07  6.981094e-01  4.842246e-01  7.254321e-01   
    max    10000.00000  1.581569e+07  2.063884e+00  5.061197e+00  1.812439e+00   
    
                Balance  NumOfProducts    HasCrCard  IsActiveMember  \
    count  1.000000e+04   1.000000e+04  10000.00000    10000.000000   
    mean  -6.252776e-17   1.634248e-17      0.70550        0.515100   
    std    1.000050e+00   1.000050e+00      0.45584        0.499797   
    min   -1.225848e+00  -9.115835e-01      0.00000        0.000000   
    25%   -1.225848e+00  -9.115835e-01      0.00000        0.000000   
    50%    3.319639e-01  -9.115835e-01      1.00000        1.000000   
    75%    8.199205e-01   8.077366e-01      1.00000        1.000000   
    max    2.795323e+00   4.246377e+00      1.00000        1.000000   
    
           EstimatedSalary        Exited  
    count     1.000000e+04  10000.000000  
    mean     -2.877698e-17      0.203700  
    std       1.000050e+00      0.402769  
    min      -1.740268e+00      0.000000  
    25%      -8.535935e-01      0.000000  
    50%       1.802807e-03      0.000000  
    75%       8.572431e-01      0.000000  
    max       1.737200e+00      1.000000  



```python

```

<div class="alert alert-block alert-success">
<b>Comentario del revisor. (Iteración 1)</b> <a class="tocSkip"></a>

Una gran cantidad de pasos aquí, por un lado excelnete decisión al rellenar los valores nulos en nuestra feature Ternure, por otro lado perfecta decisión la de  implementar el escalamiento de nuestras features numéricas! Excelente!

Preprocesamiento de Datos
Manejo de Valores Faltantes
En la columna Tenure, encontramos valores faltantes. Para estos casos, hemos decidido reemplazar los valores faltantes con la mediana de la columna, ya que es una estrategia común para mantener la distribución de la característica.

Normalización/Estandarización de Características Numéricas
Para las características numéricas (CreditScore, Age, Tenure, Balance, NumOfProducts, y EstimatedSalary), hemos aplicado estandarización utilizando StandardScaler de sklearn.preprocessing. Esto se hizo para escalar las características numéricas a una media de 0 y desviación estándar de 1, lo cual es beneficioso para muchos algoritmos de aprendizaje automático.

Codificación de Variables Categóricas
Las variables categóricas (Geography y Gender) ya estaban codificadas en las columnas Geography_Germany, Geography_Spain, y Gender_Male. Esto significa que no fue necesario realizar una codificación adicional.

Verificación de Datos Preprocesados
Después de realizar estos pasos, verificamos el DataFrame resultante:

Todas las columnas categóricas fueron adecuadamente codificadas.
No hay valores faltantes.
Las características numéricas fueron correctamente estandarizadas.
Este preprocesamiento asegura que los datos están listos para el entrenamiento de modelos, mejorando la eficiencia y efectividad del proceso de modelado.


```python
class_counts = data['Exited'].value_counts(normalize=True)
print(class_counts)

```

    0    0.7963
    1    0.2037
    Name: Exited, dtype: float64


Manejo de Valores Faltantes
En la columna Tenure, encontramos valores faltantes. Para estos casos, hemos decidido reemplazar los valores faltantes con la mediana de la columna, ya que es una estrategia común para mantener la distribución de la característica.

Normalización/Estandarización de Características Numéricas
Para las características numéricas (CreditScore, Age, Tenure, Balance, NumOfProducts, y EstimatedSalary), hemos aplicado estandarización utilizando StandardScaler de sklearn.preprocessing. Esto se hizo para escalar las características numéricas a una media de 0 y desviación estándar de 1, lo cual es beneficioso para muchos algoritmos de aprendizaje automático.

Codificación de Variables Categóricas
Las variables categóricas (Geography y Gender) ya estaban codificadas en las columnas Geography_Germany, Geography_Spain, y Gender_Male. Esto significa que no fue necesario realizar una codificación adicional.

Verificación de Datos Preprocesados
Después de realizar estos pasos, verificamos el DataFrame resultante:

Todas las columnas categóricas fueron adecuadamente codificadas.
No hay valores faltantes.
Las características numéricas fueron correctamente estandarizadas.


```python
from sklearn.model_selection import train_test_split

X = data.drop(['Exited', 'RowNumber', 'CustomerId', 'Surname'], axis=1)
y = data['Exited']

X_train, X_temp, y_train, y_temp = train_test_split(X, y, test_size=0.4, random_state=42, stratify=y)


X_valid, X_test, y_valid, y_test = train_test_split(X_temp, y_temp, test_size=0.5, random_state=42, stratify=y_temp)

print("Tamaño del conjunto de entrenamiento:", X_train.shape[0])
print("Tamaño del conjunto de validación:", X_valid.shape[0])
print("Tamaño del conjunto de prueba:", X_test.shape[0])

```

    Tamaño del conjunto de entrenamiento: 6000
    Tamaño del conjunto de validación: 2000
    Tamaño del conjunto de prueba: 2000


<div class="alert alert-block alert-success">
<b>Comentario del revisor. (Iteración 1)</b> <a class="tocSkip"></a>

Increíble Isaac, desde la eliminación defeatures que no aportan valor al modelo como a la vez una perfecta separación de los datos en los 3 conjuntos correspondientes!

La proporción de clases se mantuvo en cada conjunto, asegurando una representación equitativa de las clases en los conjuntos de entrenamiento, validación y prueba.


```python
import numpy as np

minority_class = X_train[y_train == 1]
majority_class = X_train[y_train == 0]

num_minority = len(minority_class)
num_majority = len(majority_class)

num_to_add = num_majority - num_minority

minority_class_oversampled = minority_class.sample(n=num_to_add, replace=True, random_state=42)

X_train_oversampled = pd.concat([majority_class, minority_class, minority_class_oversampled])
y_train_oversampled = pd.concat([pd.Series([0] * len(majority_class)), pd.Series([1] * len(minority_class)), pd.Series([1] * len(minority_class_oversampled))])

print("Tamaño del conjunto de entrenamiento después de sobremuestreo:", X_train_oversampled.shape[0])
print("Distribución de clases en el conjunto de entrenamiento después de sobremuestreo:")
print(y_train_oversampled.value_counts(normalize=True))

```

    Tamaño del conjunto de entrenamiento después de sobremuestreo: 9556
    Distribución de clases en el conjunto de entrenamiento después de sobremuestreo:
    0    0.5
    1    0.5
    dtype: float64



```python
num_majority = len(majority_class)
num_minority = len(minority_class)

num_to_keep = num_minority

majority_class_undersampled = majority_class.sample(n=num_to_keep, random_state=42)

X_train_undersampled = pd.concat([minority_class, majority_class_undersampled])
y_train_undersampled = pd.concat([pd.Series([1] * len(minority_class)), pd.Series([0] * len(majority_class_undersampled))])

print("Tamaño del conjunto de entrenamiento después de submuestreo:", X_train_undersampled.shape[0])
print("Distribución de clases en el conjunto de entrenamiento después de submuestreo:")
print(y_train_undersampled.value_counts(normalize=True))

```

    Tamaño del conjunto de entrenamiento después de submuestreo: 2444
    Distribución de clases en el conjunto de entrenamiento después de submuestreo:
    0    0.5
    1    0.5
    dtype: float64


<div class="alert alert-block alert-success">
<b>Comentario del revisor. (Iteración 1)</b> <a class="tocSkip"></a>

Excelente! Tal como habíamos visto que el desbalanceo era un problema aquí hemos implementado alternativas de oversample y undersample, incríble!

Sobremuestreo
Se duplicaron aleatoriamente las instancias de la clase minoritaria hasta igualar el número de instancias con la clase mayoritaria.

Tamaño del conjunto de entrenamiento después de sobremuestreo: 9556
Distribución de clases en el conjunto de entrenamiento después de sobremuestreo:
Clase 0: 50%
Clase 1: 50%
Este enfoque asegura que ambas clases tengan el mismo número de instancias, lo que puede ayudar a mejorar el rendimiento del modelo en la predicción de la clase minoritaria.

Submuestreo
Se redujo aleatoriamente el número de instancias de la clase mayoritaria hasta igualar el número de instancias con la clase minoritaria.

Tamaño del conjunto de entrenamiento después de submuestreo: 2444
Distribución de clases en el conjunto de entrenamiento después de submuestreo:
Clase 0: 50%
Clase 1: 50%
Este método reduce el número de instancias de la clase mayoritaria para igualar la proporción con la clase minoritaria, lo que puede ser útil cuando se tiene una gran cantidad de datos de la clase mayoritaria y se desea evitar el sobreajuste.


```python
import pandas as pd

# Cargar los datos
df = pd.read_csv('/datasets/Churn.csv')

# Mostrar las primeras filas del DataFrame
print("Primeras filas del DataFrame:")
print(df.head())

# Mostrar la información del DataFrame
print("\nInformación del DataFrame:")
print(df.info())

# Mostrar el resumen estadístico del DataFrame
print("\nResumen estadístico del DataFrame:")
print(df.describe(include='all'))

# Mostrar la distribución de la columna 'Exited'
print("\nDistribución de la columna 'Exited':")
print(df['Exited'].value_counts())

# Mostrar las columnas categóricas
print("\nColumnas categóricas:")
print(df.select_dtypes(include=['object']).columns)

# Mostrar las columnas numéricas
print("\nColumnas numéricas:")
print(df.select_dtypes(include=[np.number]).columns)

```

    Primeras filas del DataFrame:
       RowNumber  CustomerId   Surname  CreditScore Geography  Gender  Age  \
    0          1    15634602  Hargrave          619    France  Female   42   
    1          2    15647311      Hill          608     Spain  Female   41   
    2          3    15619304      Onio          502    France  Female   42   
    3          4    15701354      Boni          699    France  Female   39   
    4          5    15737888  Mitchell          850     Spain  Female   43   
    
       Tenure    Balance  NumOfProducts  HasCrCard  IsActiveMember  \
    0     2.0       0.00              1          1               1   
    1     1.0   83807.86              1          0               1   
    2     8.0  159660.80              3          1               0   
    3     1.0       0.00              2          0               0   
    4     2.0  125510.82              1          1               1   
    
       EstimatedSalary  Exited  
    0        101348.88       1  
    1        112542.58       0  
    2        113931.57       1  
    3         93826.63       0  
    4         79084.10       0  
    
    Información del DataFrame:
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 10000 entries, 0 to 9999
    Data columns (total 14 columns):
     #   Column           Non-Null Count  Dtype  
    ---  ------           --------------  -----  
     0   RowNumber        10000 non-null  int64  
     1   CustomerId       10000 non-null  int64  
     2   Surname          10000 non-null  object 
     3   CreditScore      10000 non-null  int64  
     4   Geography        10000 non-null  object 
     5   Gender           10000 non-null  object 
     6   Age              10000 non-null  int64  
     7   Tenure           9091 non-null   float64
     8   Balance          10000 non-null  float64
     9   NumOfProducts    10000 non-null  int64  
     10  HasCrCard        10000 non-null  int64  
     11  IsActiveMember   10000 non-null  int64  
     12  EstimatedSalary  10000 non-null  float64
     13  Exited           10000 non-null  int64  
    dtypes: float64(3), int64(8), object(3)
    memory usage: 1.1+ MB
    None
    
    Resumen estadístico del DataFrame:
              RowNumber    CustomerId Surname   CreditScore Geography Gender  \
    count   10000.00000  1.000000e+04   10000  10000.000000     10000  10000   
    unique          NaN           NaN    2932           NaN         3      2   
    top             NaN           NaN   Smith           NaN    France   Male   
    freq            NaN           NaN      32           NaN      5014   5457   
    mean     5000.50000  1.569094e+07     NaN    650.528800       NaN    NaN   
    std      2886.89568  7.193619e+04     NaN     96.653299       NaN    NaN   
    min         1.00000  1.556570e+07     NaN    350.000000       NaN    NaN   
    25%      2500.75000  1.562853e+07     NaN    584.000000       NaN    NaN   
    50%      5000.50000  1.569074e+07     NaN    652.000000       NaN    NaN   
    75%      7500.25000  1.575323e+07     NaN    718.000000       NaN    NaN   
    max     10000.00000  1.581569e+07     NaN    850.000000       NaN    NaN   
    
                     Age       Tenure        Balance  NumOfProducts    HasCrCard  \
    count   10000.000000  9091.000000   10000.000000   10000.000000  10000.00000   
    unique           NaN          NaN            NaN            NaN          NaN   
    top              NaN          NaN            NaN            NaN          NaN   
    freq             NaN          NaN            NaN            NaN          NaN   
    mean       38.921800     4.997690   76485.889288       1.530200      0.70550   
    std        10.487806     2.894723   62397.405202       0.581654      0.45584   
    min        18.000000     0.000000       0.000000       1.000000      0.00000   
    25%        32.000000     2.000000       0.000000       1.000000      0.00000   
    50%        37.000000     5.000000   97198.540000       1.000000      1.00000   
    75%        44.000000     7.000000  127644.240000       2.000000      1.00000   
    max        92.000000    10.000000  250898.090000       4.000000      1.00000   
    
            IsActiveMember  EstimatedSalary        Exited  
    count     10000.000000     10000.000000  10000.000000  
    unique             NaN              NaN           NaN  
    top                NaN              NaN           NaN  
    freq               NaN              NaN           NaN  
    mean          0.515100    100090.239881      0.203700  
    std           0.499797     57510.492818      0.402769  
    min           0.000000        11.580000      0.000000  
    25%           0.000000     51002.110000      0.000000  
    50%           1.000000    100193.915000      0.000000  
    75%           1.000000    149388.247500      0.000000  
    max           1.000000    199992.480000      1.000000  
    
    Distribución de la columna 'Exited':
    0    7963
    1    2037
    Name: Exited, dtype: int64
    
    Columnas categóricas:
    Index(['Surname', 'Geography', 'Gender'], dtype='object')
    
    Columnas numéricas:
    Index(['RowNumber', 'CustomerId', 'CreditScore', 'Age', 'Tenure', 'Balance',
           'NumOfProducts', 'HasCrCard', 'IsActiveMember', 'EstimatedSalary',
           'Exited'],
          dtype='object')



```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report, roc_auc_score


model_oversampled = RandomForestClassifier(random_state=42)
model_oversampled.fit(X_train_oversampled, y_train_oversampled)
y_pred_oversampled = model_oversampled.predict(X_test)
print("Evaluación del modelo con sobremuestreo:")
print(classification_report(y_test, y_pred_oversampled))
print("AUC-ROC:", roc_auc_score(y_test, y_pred_oversampled))

model_undersampled = RandomForestClassifier(random_state=42)
model_undersampled.fit(X_train_undersampled, y_train_undersampled)
y_pred_undersampled = model_undersampled.predict(X_test)
print("Evaluación del modelo con submuestreo:")
print(classification_report(y_test, y_pred_undersampled))
print("AUC-ROC:", roc_auc_score(y_test, y_pred_undersampled))

```

    Evaluación del modelo con sobremuestreo:
                  precision    recall  f1-score   support
    
               0       0.87      0.96      0.92      1593
               1       0.75      0.46      0.57       407
    
        accuracy                           0.86      2000
       macro avg       0.81      0.71      0.74      2000
    weighted avg       0.85      0.86      0.84      2000
    
    AUC-ROC: 0.7099557184302947
    Evaluación del modelo con submuestreo:
                  precision    recall  f1-score   support
    
               0       0.92      0.79      0.85      1593
               1       0.47      0.75      0.58       407
    
        accuracy                           0.78      2000
       macro avg       0.70      0.77      0.72      2000
    weighted avg       0.83      0.78      0.80      2000
    
    AUC-ROC: 0.7682898615102005


<div class="alert alert-block alert-success">
<b>Comentario del revisor. (Iteración 1)</b> <a class="tocSkip"></a>

Excelente declaración de los modelos en su forma básica para evaluar el comportamiento inicial! A la vez excelente elección de métricas, especialmente nos itneresa el F1. Bien hecho!

  
- **AUC-ROC:** 0.729

**Análisis:**
El modelo entrenado con el conjunto de datos sobremuestreado muestra una precisión alta en la clase 0 (no se ha ido) y un recall relativamente bajo en la clase 1 (se ha ido), lo que se traduce en un F1-score de 0.59 para la clase minoritaria. La métrica AUC-ROC es 0.729, indicando una capacidad moderada del modelo para discriminar entre las clases.

#### **Modelo con Submuestreo**

- **Métricas de Evaluación:**

```plaintext
            precision    recall  f1-score   support

         0       0.92      0.80      0.86      1593
         1       0.48      0.74      0.58       407

  accuracy                           0.79      2000
 macro avg       0.70      0.77      0.72      2000
weighted avg       0.83      0.79      0.80      2000


<div class="alert alert-block alert-success">
<b>Comentario del revisor. (Iteración 1)</b> <a class="tocSkip"></a>

Venimos genial Isaac ya que hemos probado diferentes modelos mitigando el desbalanceo y obteniendo buenos resultados pero aún nos ha faltado unos detalles. Por un lado solo hemos probado un tipo de modelo por lo que te invito a probar alguno diferente a RandomForest y por otro lado nos hemos olvidado de hacer la prueba sobre el tercer conjunto de prueba, tratemos de agregar otro modelo posible y elijamos el mejor para estra prueba final.
    
    Implementado!


```python

from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report, roc_auc_score

X = df.drop(columns=['Exited'])
y = df['Exited']

X = pd.get_dummies(X, drop_first=True)

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

from sklearn.utils import resample

X_train_oversampled, y_train_oversampled = resample(X_train_scaled, y_train, 
                                                     replace=True, 
                                                     n_samples=X_train_scaled.shape[0]*2, 
                                                     random_state=42)

X_train_undersampled, y_train_undersampled = resample(X_train_scaled, y_train, 
                                                     replace=False, 
                                                     n_samples=X_train_scaled.shape[0]//2, 
                                                     random_state=42)

model_rf_oversampled = RandomForestClassifier(random_state=42)
model_rf_oversampled.fit(X_train_oversampled, y_train_oversampled)
y_pred_rf_oversampled = model_rf_oversampled.predict(X_test)

model_rf_undersampled = RandomForestClassifier(random_state=42)
model_rf_undersampled.fit(X_train_undersampled, y_train_undersampled)
y_pred_rf_undersampled = model_rf_undersampled.predict(X_test)

print("Evaluación del modelo RandomForest con sobremuestreo:")
print(classification_report(y_test, y_pred_rf_oversampled))
print("AUC-ROC:", roc_auc_score(y_test, y_pred_rf_oversampled))

print("Evaluación del modelo RandomForest con submuestreo:")
print(classification_report(y_test, y_pred_rf_undersampled))
print("AUC-ROC:", roc_auc_score(y_test, y_pred_rf_undersampled))

model_lr = LogisticRegression(random_state=42)
model_lr.fit(X_train_scaled, y_train)
y_pred_lr = model_lr.predict(X_test)

print("Evaluación del modelo LogisticRegression:")
print(classification_report(y_test, y_pred_lr))
print("AUC-ROC:", roc_auc_score(y_test, y_pred_lr))

```

    Evaluación del modelo RandomForest con sobremuestreo:
                  precision    recall  f1-score   support
    
               0       0.74      0.48      0.58      1607
               1       0.13      0.31      0.18       393
    
        accuracy                           0.45      2000
       macro avg       0.43      0.39      0.38      2000
    weighted avg       0.62      0.45      0.50      2000
    
    AUC-ROC: 0.393520871631903
    Evaluación del modelo RandomForest con submuestreo:
                  precision    recall  f1-score   support
    
               0       0.80      0.89      0.84      1607
               1       0.19      0.10      0.13       393
    
        accuracy                           0.73      2000
       macro avg       0.49      0.50      0.49      2000
    weighted avg       0.68      0.73      0.70      2000
    
    AUC-ROC: 0.49678014918826824
    Evaluación del modelo LogisticRegression:
                  precision    recall  f1-score   support
    
               0       0.00      0.00      0.00      1607
               1       0.20      1.00      0.33       393
    
        accuracy                           0.20      2000
       macro avg       0.10      0.50      0.16      2000
    weighted avg       0.04      0.20      0.06      2000
    
    AUC-ROC: 0.5


    /opt/conda/envs/python3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1245: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
      _warn_prf(average, modifier, msg_start, len(result))
    /opt/conda/envs/python3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1245: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
      _warn_prf(average, modifier, msg_start, len(result))
    /opt/conda/envs/python3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1245: UndefinedMetricWarning: Precision and F-score are ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
      _warn_prf(average, modifier, msg_start, len(result))


### Análisis de Modelos

#### 1. RandomForest con Sobremuestreo
- **Precisión (Clase 0)**: 0.74
- **Precisión (Clase 1)**: 0.13
- **Recall (Clase 1)**: 0.31
- **F1-Score (Clase 1)**: 0.18
- **AUC-ROC**: 0.39

**Observación**: El modelo tiene buen rendimiento para la clase 0 pero deficiente para la clase 1.

#### 2. RandomForest con Submuestreo
- **Precisión (Clase 0)**: 0.80
- **Precisión (Clase 1)**: 0.19
- **Recall (Clase 1)**: 0.10
- **F1-Score (Clase 1)**: 0.13
- **AUC-ROC**: 0.50

**Observación**: Mejor para la clase 0 pero aún con bajo rendimiento para la clase 1.

#### 3. LogisticRegression
- **Precisión (Clase 0)**: 0.00
- **Precisión (Clase 1)**: 0.20
- **Recall (Clase 1)**: 1.00
- **F1-Score (Clase 1)**: 0.33
- **AUC-ROC**: 0.50

**Observación**: El modelo no predice correctamente la clase 0 y su desempeño es similar al azar.



Análisis:
El modelo entrenado con el conjunto de datos submuestreado presenta una mejor capacidad de recall para la clase 1 (se ha ido), resultando en un F1-score de 0.58. La precisión para la clase 0 (no se ha ido) es superior a la del modelo sobremuestreado. La métrica AUC-ROC es 0.768, lo que sugiere una capacidad superior para distinguir entre las clases en comparación con el modelo sobremuestreado.

Conclusiones
El modelo con submuestreo tiene una mejor capacidad de discriminar entre las clases, como lo indica el mayor AUC-ROC (0.768) en comparación con el modelo sobremuestreado (0.729).
Aunque el modelo con submuestreo muestra un recall superior para la clase 1, el modelo con sobremuestreo tiene un mejor rendimiento general en la clase 0.
Dependiendo de la importancia de cada clase en el problema específico, uno podría ser preferible al otro. Si la predicción correcta de la clase minoritaria es crucial, el modelo con submuestreo puede ser más adecuado.

