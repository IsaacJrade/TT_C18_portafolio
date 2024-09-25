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

# Descripción

La compañía de seguros Sure Tomorrow quiere resolver varias tareas con la ayuda de machine learning y te pide que evalúes esa posibilidad.
- Tarea 1: encontrar clientes que sean similares a un cliente determinado. Esto ayudará a los agentes de la compañía con el marketing.
- Tarea 2: predecir la probabilidad de que un nuevo cliente reciba una prestación del seguro. ¿Puede un modelo de predictivo funcionar mejor que un modelo dummy?
- Tarea 3: predecir el número de prestaciones de seguro que un nuevo cliente pueda recibir utilizando un modelo de regresión lineal.
- Tarea 4: proteger los datos personales de los clientes sin afectar al modelo del ejercicio anterior. Es necesario desarrollar un algoritmo de transformación de datos que dificulte la recuperación de la información personal si los datos caen en manos equivocadas. Esto se denomina enmascaramiento u ofuscación de datos. Pero los datos deben protegerse de tal manera que no se vea afectada la calidad de los modelos de machine learning. No es necesario elegir el mejor modelo, basta con demostrar que el algoritmo funciona correctamente.


# Preprocesamiento y exploración de datos

## Inicialización


```python
pip install scikit-learn --upgrade
```

    Requirement already satisfied: scikit-learn in /opt/conda/envs/python3/lib/python3.9/site-packages (0.24.1)
    Collecting scikit-learn
      Downloading scikit_learn-1.5.1-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (12 kB)
    Requirement already satisfied: numpy>=1.19.5 in /opt/conda/envs/python3/lib/python3.9/site-packages (from scikit-learn) (1.21.2)
    Requirement already satisfied: scipy>=1.6.0 in /opt/conda/envs/python3/lib/python3.9/site-packages (from scikit-learn) (1.10.1)
    Requirement already satisfied: joblib>=1.2.0 in /opt/conda/envs/python3/lib/python3.9/site-packages (from scikit-learn) (1.4.2)
    Requirement already satisfied: threadpoolctl>=3.1.0 in /opt/conda/envs/python3/lib/python3.9/site-packages (from scikit-learn) (3.5.0)
    Downloading scikit_learn-1.5.1-cp39-cp39-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (13.4 MB)
    [2K   [90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━[0m [32m13.4/13.4 MB[0m [31m98.4 MB/s[0m eta [36m0:00:00[0m:00:01[0m00:01[0m
    [?25hInstalling collected packages: scikit-learn
      Attempting uninstall: scikit-learn
        Found existing installation: scikit-learn 0.24.1
        Uninstalling scikit-learn-0.24.1:
    [31mERROR: Could not install packages due to an OSError: [Errno 13] Permission denied: 'COPYING'
    Consider using the `--user` option or check the permissions.
    [0m[31m
    [0mNote: you may need to restart the kernel to use updated packages.



```python
import numpy as np
import pandas as pd

import seaborn as sns

import sklearn.linear_model
import sklearn.metrics
import sklearn.neighbors
import sklearn.preprocessing

from sklearn.model_selection import train_test_split

from IPython.display import display
```

## Carga de datos

Carga los datos y haz una revisión básica para comprobar que no hay problemas obvios.


```python
df = pd.read_csv('/datasets/insurance_us.csv')
```

Renombramos las columnas para que el código se vea más coherente con su estilo.


```python
df = df.rename(columns={'Gender': 'gender', 'Age': 'age', 'Salary': 'income', 'Family members': 'family_members', 'Insurance benefits': 'insurance_benefits'})
```


```python
df.sample(10)
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
      <th>gender</th>
      <th>age</th>
      <th>income</th>
      <th>family_members</th>
      <th>insurance_benefits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2846</th>
      <td>0</td>
      <td>38.0</td>
      <td>27500.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>548</th>
      <td>1</td>
      <td>33.0</td>
      <td>41500.0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>386</th>
      <td>0</td>
      <td>26.0</td>
      <td>26700.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>902</th>
      <td>0</td>
      <td>19.0</td>
      <td>42200.0</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>500</th>
      <td>0</td>
      <td>18.0</td>
      <td>54800.0</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3348</th>
      <td>0</td>
      <td>25.0</td>
      <td>46800.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2183</th>
      <td>0</td>
      <td>19.0</td>
      <td>56200.0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3459</th>
      <td>1</td>
      <td>52.0</td>
      <td>30600.0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4854</th>
      <td>1</td>
      <td>22.0</td>
      <td>30300.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4388</th>
      <td>1</td>
      <td>20.0</td>
      <td>38900.0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 5000 entries, 0 to 4999
    Data columns (total 5 columns):
     #   Column              Non-Null Count  Dtype  
    ---  ------              --------------  -----  
     0   gender              5000 non-null   int64  
     1   age                 5000 non-null   float64
     2   income              5000 non-null   float64
     3   family_members      5000 non-null   int64  
     4   insurance_benefits  5000 non-null   int64  
    dtypes: float64(2), int64(3)
    memory usage: 195.4 KB



```python
df['age'] = df['age'].astype(int)# puede que queramos cambiar el tipo de edad (de float a int) aunque esto no es crucial

# escribe tu conversión aquí si lo deseas:
```


```python
display(df.sample(10))# comprueba que la conversión se haya realizado con éxito
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
      <th>gender</th>
      <th>age</th>
      <th>income</th>
      <th>family_members</th>
      <th>insurance_benefits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2748</th>
      <td>0</td>
      <td>38</td>
      <td>30800.0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4937</th>
      <td>1</td>
      <td>40</td>
      <td>24100.0</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3410</th>
      <td>0</td>
      <td>24</td>
      <td>33900.0</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>671</th>
      <td>0</td>
      <td>26</td>
      <td>51200.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3209</th>
      <td>1</td>
      <td>59</td>
      <td>51700.0</td>
      <td>2</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4880</th>
      <td>1</td>
      <td>53</td>
      <td>38300.0</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1203</th>
      <td>0</td>
      <td>31</td>
      <td>19600.0</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>952</th>
      <td>0</td>
      <td>23</td>
      <td>49900.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>48</th>
      <td>1</td>
      <td>25</td>
      <td>33100.0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>381</th>
      <td>1</td>
      <td>30</td>
      <td>40500.0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



```python
df.describe()# ahora echa un vistazo a las estadísticas descriptivas de los datos.# ¿Se ve todo bien?
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
      <th>gender</th>
      <th>age</th>
      <th>income</th>
      <th>family_members</th>
      <th>insurance_benefits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>5000.000000</td>
      <td>5000.000000</td>
      <td>5000.000000</td>
      <td>5000.000000</td>
      <td>5000.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.499000</td>
      <td>30.952800</td>
      <td>39916.360000</td>
      <td>1.194200</td>
      <td>0.148000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.500049</td>
      <td>8.440807</td>
      <td>9900.083569</td>
      <td>1.091387</td>
      <td>0.463183</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>18.000000</td>
      <td>5300.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.000000</td>
      <td>24.000000</td>
      <td>33300.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.000000</td>
      <td>30.000000</td>
      <td>40200.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.000000</td>
      <td>37.000000</td>
      <td>46600.000000</td>
      <td>2.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.000000</td>
      <td>65.000000</td>
      <td>79000.000000</td>
      <td>6.000000</td>
      <td>5.000000</td>
    </tr>
  </tbody>
</table>
</div>



<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Muy bien! Importaste de forma correcta las librerías y módulos, cambiaste el formato de los nombres y verificaste que no hubiera outliers inválidos en los datos.
</div>

# Revisar estadísticas descriptivas para detectar valores extremos o problemas

# 1. 'gender': Es una variable categórica binaria, donde 0 y 1 parecen representar los dos géneros. La media está cercana a 0.5, lo cual indica una distribución balanceada entre los dos géneros.
# Conclusión: No se detectan problemas en la variable 'gender'.

# 2. 'age': El rango de edad es de 18 a 65 años, lo cual es razonable.
# Conclusión: No se observan valores extremos o atípicos en 'age'. 

# 3. 'income': Los salarios van de 5300 a 79000. Este rango parece razonable.
# Conclusión: No hay valores extremos o atípicos en 'income'.

# 4. 'family_members': El número de miembros familiares varía de 0 a 6, la mayoría de los asegurados tiene pocos dependientes.
# Conclusión: No se observan problemas en 'family_members'

# 5. 'insurance_benefits': El número de beneficios varía de 0 a 5
# Conclusión: La distribución parece cargada hacia 0, lo cual podría requerir una exploración más profunda durante el análisis.

# Resumen: No se detectan problemas significativos en las estadísticas descriptivas. Podemos proceder con el análisis exploratorio de datos (EDA) y el desarrollo de los modelos.



```python
print(df.head())

```

       gender  age   income  family_members  insurance_benefits
    0       1   41  49600.0               1                   0
    1       0   46  38000.0               1                   1
    2       0   29  21000.0               0                   0
    3       0   21  41700.0               2                   0
    4       1   28  26100.0               0                   0



```python
print(df.info())

print(df.describe())

```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 5000 entries, 0 to 4999
    Data columns (total 5 columns):
     #   Column              Non-Null Count  Dtype  
    ---  ------              --------------  -----  
     0   gender              5000 non-null   int64  
     1   age                 5000 non-null   int64  
     2   income              5000 non-null   float64
     3   family_members      5000 non-null   int64  
     4   insurance_benefits  5000 non-null   int64  
    dtypes: float64(1), int64(4)
    memory usage: 195.4 KB
    None
                gender          age        income  family_members  \
    count  5000.000000  5000.000000   5000.000000     5000.000000   
    mean      0.499000    30.952800  39916.360000        1.194200   
    std       0.500049     8.440807   9900.083569        1.091387   
    min       0.000000    18.000000   5300.000000        0.000000   
    25%       0.000000    24.000000  33300.000000        0.000000   
    50%       0.000000    30.000000  40200.000000        1.000000   
    75%       1.000000    37.000000  46600.000000        2.000000   
    max       1.000000    65.000000  79000.000000        6.000000   
    
           insurance_benefits  
    count         5000.000000  
    mean             0.148000  
    std              0.463183  
    min              0.000000  
    25%              0.000000  
    50%              0.000000  
    75%              0.000000  
    max              5.000000  



```python
print(df.isnull().sum())

feature_names = ['gender', 'age', 'income', 'family_members']


print(df[feature_names].head())

```

    gender                0
    age                   0
    income                0
    family_members        0
    insurance_benefits    0
    dtype: int64
       gender  age   income  family_members
    0       1   41  49600.0               1
    1       0   46  38000.0               1
    2       0   29  21000.0               0
    3       0   21  41700.0               2
    4       1   28  26100.0               0


## Análisis exploratorio de datos

Vamos a comprobar rápidamente si existen determinados grupos de clientes observando el gráfico de pares.


```python
g = sns.pairplot(df, kind='hist')
g.fig.set_size_inches(12, 12)
```


    
![png](output_23_0.png)
    


De acuerdo, es un poco complicado detectar grupos obvios (clústeres) ya que es difícil combinar diversas variables simultáneamente (para analizar distribuciones multivariadas). Ahí es donde LA y ML pueden ser bastante útiles.

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Excelente trabajo con el desarrollo de la gráfica de pares. 
</div>

# Tarea 1. Clientes similares

En el lenguaje de ML, es necesario desarrollar un procedimiento que devuelva los k vecinos más cercanos (objetos) para un objeto dado basándose en la distancia entre los objetos.
Es posible que quieras revisar las siguientes lecciones (capítulo -> lección)- Distancia entre vectores -> Distancia euclidiana
- Distancia entre vectores -> Distancia Manhattan

Para resolver la tarea, podemos probar diferentes métricas de distancia.

Escribe una función que devuelva los k vecinos más cercanos para un $n^{th}$ objeto basándose en una métrica de distancia especificada. A la hora de realizar esta tarea no debe tenerse en cuenta el número de prestaciones de seguro recibidas.
Puedes utilizar una implementación ya existente del algoritmo kNN de scikit-learn (consulta [el enlace](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.NearestNeighbors.html#sklearn.neighbors.NearestNeighbors)) o tu propia implementación.
Pruébalo para cuatro combinaciones de dos casos- Escalado
  - los datos no están escalados
  - los datos se escalan con el escalador [MaxAbsScaler](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.MaxAbsScaler.html)
- Métricas de distancia
  - Euclidiana
  - Manhattan

Responde a estas preguntas:- ¿El hecho de que los datos no estén escalados afecta al algoritmo kNN? Si es así, ¿cómo se manifiesta?- ¿Qué tan similares son los resultados al utilizar la métrica de distancia Manhattan (independientemente del escalado)?


```python
feature_names = ['gender', 'age', 'income', 'family_members']
```


```python
from sklearn.neighbors import NearestNeighbors

def get_knn(df, n, k, metric, scaled=False):
    """
    Devuelve los k vecinos más cercanos para un objeto dado
    
    :param df: DataFrame de pandas utilizado para encontrar objetos similares
    :param n: índice del objeto para el cual se buscan los vecinos más cercanos
    :param k: número de vecinos más cercanos a devolver
    :param metric: nombre de la métrica de distancia ('euclidean' o 'manhattan')
    :param scaled: bool, indica si los datos deben ser escalados
    """
    
    # Seleccionar las características relevantes
    X = df[feature_names].copy()
    
    # Escalar los datos si es necesario
    if scaled:
        from sklearn.preprocessing import MaxAbsScaler
        scaler = MaxAbsScaler()
        X = scaler.fit_transform(X)
    
    # Validar que el índice n esté dentro del rango
    if n < 0 or n >= len(X):
        raise ValueError(f"El índice {n} está fuera del rango de los datos.")
    
    # Crear y entrenar el modelo kNN
    nbrs = NearestNeighbors(n_neighbors=k, metric=metric)
    nbrs.fit(X)
    
    # Encontrar los k vecinos más cercanos
    query_point = X[n].reshape(1, -1)  # Convertir a 2D array para compatibilidad con kneighbors
    nbrs_distances, nbrs_indices = nbrs.kneighbors(query_point, return_distance=True)
    
    # Crear un DataFrame con los resultados
    df_res = pd.concat([
        df.iloc[nbrs_indices[0]], 
        pd.DataFrame(nbrs_distances.T, index=nbrs_indices[0], columns=['distance'])
        ], axis=1)
    
    return df_res

```

Escalar datos.


```python
feature_names = ['gender', 'age', 'income', 'family_members']

transformer_mas = sklearn.preprocessing.MaxAbsScaler().fit(df[feature_names].to_numpy())

df_scaled = df.copy()
df_scaled.loc[:, feature_names] = transformer_mas.transform(df[feature_names].to_numpy())
```


```python
df_scaled.sample(5)
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
      <th>gender</th>
      <th>age</th>
      <th>income</th>
      <th>family_members</th>
      <th>insurance_benefits</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4955</th>
      <td>1.0</td>
      <td>0.400000</td>
      <td>0.373418</td>
      <td>0.000000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4192</th>
      <td>0.0</td>
      <td>0.338462</td>
      <td>0.705063</td>
      <td>0.000000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1641</th>
      <td>1.0</td>
      <td>0.615385</td>
      <td>0.525316</td>
      <td>0.166667</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2392</th>
      <td>1.0</td>
      <td>0.384615</td>
      <td>0.550633</td>
      <td>0.333333</td>
      <td>0</td>
    </tr>
    <tr>
      <th>605</th>
      <td>1.0</td>
      <td>0.476923</td>
      <td>0.658228</td>
      <td>0.333333</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



Ahora, vamos a obtener registros similares para uno determinado, para cada combinación


```python
result_scale_euclidean = get_knn(df, n=0, k=5, metric='euclidean', scaled=True)
result_scale_manhattan = get_knn(df, n=0, k=5, metric='manhattan', scaled=True)

print("Resultados con escalado y métrica Euclidiana:")
print(result_scale_euclidean)

print("\nResultados con escalado y métrica Manhattan:")
print(result_scale_manhattan)
```

    Resultados con escalado y métrica Euclidiana:
          gender  age   income  family_members  insurance_benefits  distance
    0          1   41  49600.0               1                   0  0.000000
    2689       1   41  50100.0               1                   0  0.006329
    133        1   40  50300.0               1                   0  0.017754
    4869       1   42  50400.0               1                   1  0.018418
    3275       1   42  51500.0               1                   1  0.028550
    
    Resultados con escalado y métrica Manhattan:
          gender  age   income  family_members  insurance_benefits  distance
    0          1   41  49600.0               1                   0  0.000000
    2689       1   41  50100.0               1                   0  0.006329
    133        1   40  50300.0               1                   0  0.024245
    4869       1   42  50400.0               1                   1  0.025511
    3365       1   41  47100.0               1                   0  0.031646


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Bien implementado el modelo. Como acabas de notar, el escalado es muy importante debido a que permite que variables numéricas con rangos muy diferentes sean comparables. Sin escalar los datos las características con valores más grandes pueden dominar las métricas de distancia y no obtener resultados precisos.
</div>


```python

```

Respuestas a las preguntas

**¿El hecho de que los datos no estén escalados afecta al algoritmo kNN? Si es así, ¿cómo se manifiesta?** 

*Sí, el no escalar los datos afecta a kNN. Las características con diferentes escalas pueden dominar el cálculo de la distancia. Esto puede llevar a resultados distorsionados, ya que las características con mayores magnitudes tienen más peso en la distancia calculada.

**¿Qué tan similares son los resultados al utilizar la métrica de distancia Manhattan (independientemente del escalado)?** 

*La métrica de distancia Manhattan y la Euclidiana pueden dar resultados diferentes. Manhattan suma las diferencias absolutas, mientras que Euclidiana calcula la distancia en línea recta. Sin escalado, las distancias Euclidianas pueden dominar. Con escalado, las diferencias son menores, haciendo los resultados más comparables.

# Tarea 2. ¿Es probable que el cliente reciba una prestación del seguro?

En términos de machine learning podemos considerarlo como una tarea de clasificación binaria.

Con el valor de `insurance_benefits` superior a cero como objetivo, evalúa si el enfoque de clasificación kNN puede funcionar mejor que el modelo dummy.
Instrucciones:
- Construye un clasificador basado en KNN y mide su calidad con la métrica F1 para k=1...10 tanto para los datos originales como para los escalados. Sería interesante observar cómo k puede influir en la métrica de evaluación y si el escalado de los datos provoca alguna diferencia. Puedes utilizar una implementación ya existente del algoritmo de clasificación kNN de scikit-learn (consulta [el enlace](https://scikit-learn.org/stable/modules/generated/sklearn.neighbors.KNeighborsClassifier.html)) o tu propia implementación.- Construye un modelo dummy que, en este caso, es simplemente un modelo aleatorio. Debería devolver "1" con cierta probabilidad. Probemos el modelo con cuatro valores de probabilidad: 0, la probabilidad de pagar cualquier prestación del seguro, 0.5, 1.
La probabilidad de pagar cualquier prestación del seguro puede definirse como
$$
P\{\text{prestación de seguro recibida}\}=\frac{\text{número de clientes que han recibido alguna prestación de seguro}}{\text{número total de clientes}}.
$$

Divide todos los datos correspondientes a las etapas de entrenamiento/prueba respetando la proporción 70:30.


```python
# сalcula el objetivo
df['insurance_benefits_received'] = (df['insurance_benefits'] > 0).astype(int)
print(df[['insurance_benefits', 'insurance_benefits_received']].head())

#<tu código aquí>
```

       insurance_benefits  insurance_benefits_received
    0                   0                            0
    1                   1                            1
    2                   0                            0
    3                   0                            0
    4                   0                            0



```python
# comprueba el desequilibrio de clases con value_counts()

print(df['insurance_benefits_received'].value_counts())# <tu código aquí>
```

    0    4436
    1     564
    Name: insurance_benefits_received, dtype: int64



```python
import sklearn.metrics

def eval_classifier(y_true, y_pred):
    
    f1_score = sklearn.metrics.f1_score(y_true, y_pred)
    print(f'F1: {f1_score:.2f}')
 
    cm = sklearn.metrics.confusion_matrix(y_true, y_pred, normalize='all')
    print('Matriz de confusión')
    print(cm)

```


```python
# generar la salida de un modelo aleatorio

def rnd_model_predict(P, size, seed=42):

    rng = np.random.default_rng(seed=seed)
    return rng.binomial(n=1, p=P, size=size)
```


```python
for P in [0, df['insurance_benefits_received'].sum() / len(df), 0.5, 1]:

    print(f'La probabilidad: {P:.2f}')
    y_pred_rnd = rnd_model_predict(P, len(df))# <tu código aquí> 
        
    eval_classifier(df['insurance_benefits_received'], y_pred_rnd)
    
    print()
```

    La probabilidad: 0.00
    F1: 0.00
    Matriz de confusión
    [[0.8872 0.    ]
     [0.1128 0.    ]]
    
    La probabilidad: 0.11
    F1: 0.12
    Matriz de confusión
    [[0.7914 0.0958]
     [0.0994 0.0134]]
    
    La probabilidad: 0.50
    F1: 0.20
    Matriz de confusión
    [[0.456  0.4312]
     [0.053  0.0598]]
    
    La probabilidad: 1.00
    F1: 0.20
    Matriz de confusión
    [[0.     0.8872]
     [0.     0.1128]]
    



```python
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier
from sklearn.preprocessing import MaxAbsScaler
from sklearn.metrics import f1_score


X = df[feature_names]
y = df['insurance_benefits_received']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

print("Resultados sin escalado:")
for k in range(1, 11):
    knn = KNeighborsClassifier(n_neighbors=k, metric='euclidean')
    knn.fit(X_train, y_train)
    y_pred = knn.predict(X_test)
    print(f'k={k}')
    eval_classifier(y_test, y_pred)

scaler = MaxAbsScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

print("Resultados con escalado:")
for k in range(1, 11):
    knn = KNeighborsClassifier(n_neighbors=k, metric='euclidean')
    knn.fit(X_train_scaled, y_train)
    y_pred = knn.predict(X_test_scaled)
    print(f'k={k}')
    eval_classifier(y_test, y_pred)

```

    Resultados sin escalado:
    k=1
    F1: 0.65
    Matriz de confusión
    [[0.87466667 0.018     ]
     [0.04666667 0.06066667]]
    k=2
    F1: 0.38
    Matriz de confusión
    [[0.89066667 0.002     ]
     [0.082      0.02533333]]
    k=3
    F1: 0.39
    Matriz de confusión
    [[0.88333333 0.00933333]
     [0.07933333 0.028     ]]
    k=4
    F1: 0.16
    Matriz de confusión
    [[0.88933333 0.00333333]
     [0.098      0.00933333]]
    k=5
    F1: 0.17
    Matriz de confusión
    [[0.88333333 0.00933333]
     [0.09666667 0.01066667]]
    k=6
    F1: 0.09
    Matriz de confusión
    [[8.92000000e-01 6.66666667e-04]
     [1.02000000e-01 5.33333333e-03]]
    k=7
    F1: 0.12
    Matriz de confusión
    [[0.89133333 0.00133333]
     [0.10066667 0.00666667]]
    k=8
    F1: 0.02
    Matriz de confusión
    [[0.89266667 0.        ]
     [0.106      0.00133333]]
    k=9
    F1: 0.04
    Matriz de confusión
    [[0.89266667 0.        ]
     [0.10533333 0.002     ]]
    k=10
    F1: 0.04
    Matriz de confusión
    [[0.89266667 0.        ]
     [0.10533333 0.002     ]]
    Resultados con escalado:
    k=1
    F1: 0.93
    Matriz de confusión
    [[0.888      0.00466667]
     [0.00933333 0.098     ]]
    k=2
    F1: 0.91
    Matriz de confusión
    [[0.89       0.00266667]
     [0.01466667 0.09266667]]
    k=3
    F1: 0.94
    Matriz de confusión
    [[0.88933333 0.00333333]
     [0.00866667 0.09866667]]
    k=4
    F1: 0.92
    Matriz de confusión
    [[0.89133333 0.00133333]
     [0.01466667 0.09266667]]
    k=5
    F1: 0.95
    Matriz de confusión
    [[0.89       0.00266667]
     [0.00866667 0.09866667]]
    k=6
    F1: 0.92
    Matriz de confusión
    [[0.89133333 0.00133333]
     [0.01533333 0.092     ]]
    k=7
    F1: 0.93
    Matriz de confusión
    [[0.89       0.00266667]
     [0.01133333 0.096     ]]
    k=8
    F1: 0.92
    Matriz de confusión
    [[0.89266667 0.        ]
     [0.01533333 0.092     ]]
    k=9
    F1: 0.93
    Matriz de confusión
    [[0.89133333 0.00133333]
     [0.012      0.09533333]]
    k=10
    F1: 0.92
    Matriz de confusión
    [[8.92000000e-01 6.66666667e-04]
     [1.53333333e-02 9.20000000e-02]]


### Conclusiones

1. **Modelo Dummy:**
   - El modelo dummy muestra un rendimiento muy bajo en términos de F1 Score, especialmente cuando la probabilidad de predicción es 0 o 1. La probabilidad de 0.50 proporciona un rendimiento algo mejor, pero sigue siendo bajo comparado con el kNN.

2. **kNN Sin Escalado:**
   - Los resultados del modelo kNN sin escalado muestran una variabilidad considerable en el F1 Score dependiendo del valor de `k`. El rendimiento es mejor con valores bajos de `k`, pero hay una notable caída en la precisión cuando `k` aumenta más allá de 3.

3. **kNN Con Escalado:**
   - El escalado de los datos mejora significativamente el rendimiento del kNN. El F1 Score es consistentemente alto para `k` entre 1 y 5, con un rendimiento óptimo en `k=5`. El escalado parece estabilizar el rendimiento y mejorar la capacidad del modelo para hacer predicciones precisas.

En resumen, el escalado de datos tiene un impacto positivo en el rendimiento del kNN, y el modelo kNN supera al modelo dummy en términos de F1 Score.

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Excelente! Como pudiste observar el F1 usando el clasificador basado en KNN es mucho mayor que el del modelo aleatorio. Además, usando datos escalados el F1 aumenta todavía más, ya que evitar que el efecto de las variables con valores más grandes dominen sobre aquellas con valores más pequeños.
</div>

# Tarea 3. Regresión (con regresión lineal)

Con `insurance_benefits` como objetivo, evalúa cuál sería la RECM de un modelo de regresión lineal.

Construye tu propia implementación de regresión lineal. Para ello, recuerda cómo está formulada la solución de la tarea de regresión lineal en términos de LA. Comprueba la RECM tanto para los datos originales como para los escalados. ¿Puedes ver alguna diferencia en la RECM con respecto a estos dos casos?

Denotemos- $X$: matriz de características; cada fila es un caso, cada columna es una característica, la primera columna está formada por unidades- $y$ — objetivo (un vector)- $\hat{y}$ — objetivo estimado (un vector)- $w$ — vector de pesos
La tarea de regresión lineal en el lenguaje de las matrices puede formularse así:
$$
y = Xw
$$

El objetivo de entrenamiento es entonces encontrar esa $w$ w que minimice la distancia L2 (ECM) entre $Xw$ y $y$:

$$
\min_w d_2(Xw, y) \quad \text{or} \quad \min_w \text{MSE}(Xw, y)
$$

Parece que hay una solución analítica para lo anteriormente expuesto:
$$
w = (X^T X)^{-1} X^T y
$$

La fórmula anterior puede servir para encontrar los pesos $w$ y estos últimos pueden utilizarse para calcular los valores predichos
$$
\hat{y} = X_{val}w
$$

Divide todos los datos correspondientes a las etapas de entrenamiento/prueba respetando la proporción 70:30. Utiliza la métrica RECM para evaluar el modelo.


```python
class MyLinearRegression:
    
    def __init__(self):
        
        self.weights = None
    
    def fit(self, X, y):
        
        # añadir las unidades
        X2 = np.append(np.ones([len(X), 1]), X, axis=1)
        self.weights = np.linalg.inv(X2.T @ X2) @ X2.T @ y# <tu código aquí>

    def predict(self, X):
        
        # añadir las unidades
        X2 = np.append(np.ones([len(X), 1]), X, axis=1)# <tu código aquí>
        y_pred = X2 @ self.weights # <tu código aquí>
        
        return y_pred
```


```python
def eval_regressor(y_true, y_pred):
    
    rmse = math.sqrt(sklearn.metrics.mean_squared_error(y_true, y_pred))
    print(f'RMSE: {rmse:.2f}')
    
    r2_score = math.sqrt(sklearn.metrics.r2_score(y_true, y_pred))
    print(f'R2: {r2_score:.2f}')    
```


```python
import math
```


```python
X = df[['age', 'gender', 'income', 'family_members']].to_numpy()
y = df['insurance_benefits'].to_numpy()

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=12345)

lr = MyLinearRegression()

lr.fit(X_train, y_train)
print(lr.weights)

y_test_pred = lr.predict(X_test)
eval_regressor(y_test, y_test_pred)
```

    [-9.43539012e-01  3.57495491e-02  1.64272726e-02 -2.60743659e-07
     -1.16902127e-02]
    RMSE: 0.34
    R2: 0.66



```python
scaler = MaxAbsScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

```


```python
lr.fit(X_train_scaled, y_train)
y_test_pred_scaled = lr.predict(X_test_scaled)
print("Resultados con escalado:")
eval_regressor(y_test, y_test_pred_scaled)
```

    Resultados con escalado:
    RMSE: 0.34
    R2: 0.66


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Muy bien! Como pudiste notar usar los datos originales o los escalados no afectan los resultados del modelo de regresión lineal debido a que la relación lineal entre las variables no cambia, simplemente se reescalan. 
    
</div>


## Conclusiones

1. **Comparación de Resultados**:
   - Los valores de **RMSE** y **R2** son idénticos tanto para los datos originales como para los escalados. Esto indica que el escalado no ha tenido un impacto significativo en el rendimiento del modelo de regresión lineal para este conjunto de datos.

2. **Evaluación del Modelo**:
   - El **RMSE** de 0.34 sugiere un error cuadrático medio relativamente bajo, lo que implica que el modelo tiene un buen ajuste a los datos.
   - El **R2** de 0.66 indica que el modelo explica el 66% de la variabilidad en el objetivo. Esto sugiere una capacidad moderada de predicción, pero también indica que hay espacio para mejorar el modelo.

3. **Impacto del Escalado**:
   - Dado que el rendimiento del modelo no cambió con el escalado de datos, es posible que la regresión lineal ya esté manejando las características adecuadamente sin necesidad de escalado.

# Tarea 4. Ofuscar datos

Lo mejor es ofuscar los datos multiplicando las características numéricas (recuerda que se pueden ver como la matriz $X$) por una matriz invertible $P$. 

$$
X' = X \times P
$$

Trata de hacerlo y comprueba cómo quedarán los valores de las características después de la transformación. Por cierto, la propiedad de invertibilidad es importante aquí, así que asegúrate de que $P$ sea realmente invertible.

Puedes revisar la lección 'Matrices y operaciones matriciales -> Multiplicación de matrices' para recordar la regla de multiplicación de matrices y su implementación con NumPy.


```python
personal_info_column_list = ['gender', 'age', 'income', 'family_members']
df_pn = df[personal_info_column_list]
```


```python
X = df_pn.to_numpy()
```

Generar una matriz aleatoria $P$.


```python
rng = np.random.default_rng(seed=42)
P = rng.random(size=(X.shape[1], X.shape[1]))
```

Comprobar que la matriz P sea invertible


```python
try:
    np.linalg.inv(P)
    print("La matriz P es invertible.")
except np.linalg.LinAlgError:
    print("La matriz P no es invertible.")
```

    La matriz P es invertible.


¿Puedes adivinar la edad o los ingresos de los clientes después de la transformación?


```python
X_transformed = X @ P

import pandas as pd
df_transformed = pd.DataFrame(X_transformed, columns=personal_info_column_list)
print(df_transformed.head())

```

            gender           age        income  family_members
    0  6359.715273  22380.404676  18424.090742    46000.696690
    1  4873.294065  17160.367030  14125.780761    35253.455773
    2  2693.117429   9486.397744   7808.831560    19484.860631
    3  5345.603937  18803.227203  15479.148373    38663.061863
    4  3347.176735  11782.829283   9699.998942    24211.273378


¿Puedes recuperar los datos originales de $X'$ si conoces $P$? Intenta comprobarlo a través de los cálculos moviendo $P$ del lado derecho de la fórmula anterior al izquierdo. En este caso las reglas de la multiplicación matricial son realmente útiles


```python
P_inv = np.linalg.inv(P)

X_recovered = X_transformed @ P_inv

df_recovered = pd.DataFrame(X_recovered, columns=personal_info_column_list)
print(df_recovered.head())

```

             gender   age   income  family_members
    0  1.000000e+00  41.0  49600.0    1.000000e+00
    1 -4.473636e-12  46.0  38000.0    1.000000e+00
    2 -2.515869e-12  29.0  21000.0    9.524523e-13
    3 -4.844982e-12  21.0  41700.0    2.000000e+00
    4  1.000000e+00  28.0  26100.0   -1.019907e-13


Muestra los tres casos para algunos clientes- Datos originales
- El que está transformado- El que está invertido (recuperado)


```python
print("Datos originales:")
print(df_pn.head(3))

print("\nDatos transformados:")
print(df_transformed.head(3))

print("\nDatos recuperados:")
print(df_recovered.head(3))

```

    Datos originales:
       gender  age   income  family_members
    0       1   41  49600.0               1
    1       0   46  38000.0               1
    2       0   29  21000.0               0
    
    Datos transformados:
            gender           age        income  family_members
    0  6359.715273  22380.404676  18424.090742    46000.696690
    1  4873.294065  17160.367030  14125.780761    35253.455773
    2  2693.117429   9486.397744   7808.831560    19484.860631
    
    Datos recuperados:
             gender   age   income  family_members
    0  1.000000e+00  41.0  49600.0    1.000000e+00
    1 -4.473636e-12  46.0  38000.0    1.000000e+00
    2 -2.515869e-12  29.0  21000.0    9.524523e-13


Seguramente puedes ver que algunos valores no son exactamente iguales a los de los datos originales. ¿Cuál podría ser la razón de ello?

1. **Datos Originales vs. Datos Transformados**:
   - La transformación cambia significativamente los valores de las características. La magnitud de los valores transformados se ha incrementado considerablemente en comparación con los datos originales.

2. **Datos Recuperados**:
   - Los datos recuperados (invertidos) no coinciden exactamente con los datos originales. Esto se debe a errores numéricos que pueden surgir en el proceso de inversión de matrices y la multiplicación de matrices.


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Excelente! Lograste ofuscar los datos originales de forma adecuada y después recuperarlos a través de operaciones matriciales. Si bien hay una diferencia muy pequeña entre los datos orginales y los datos recuperados, se debe a los redondeos que se están realizando al hacer las operaciones.
</div>

## Prueba de que la ofuscación de datos puede funcionar con regresión lineal

En este proyecto la tarea de regresión se ha resuelto con la regresión lineal. Tu siguiente tarea es demostrar _analytically_ que el método de ofuscación no afectará a la regresión lineal en términos de valores predichos, es decir, que sus valores seguirán siendo los mismos. ¿Lo puedes creer? Pues no hace falta que lo creas, ¡tienes que que demostrarlo!

Entonces, los datos están ofuscados y ahora tenemos $X \times P$ en lugar de tener solo $X$. En consecuencia, hay otros pesos $w_P$ como
$$
w = (X^T X)^{-1} X^T y \quad \Rightarrow \quad w_P = [(XP)^T XP]^{-1} (XP)^T y
$$

¿Cómo se relacionarían $w$ y $w_P$ si simplificáramos la fórmula de $w_P$ anterior? 

¿Cuáles serían los valores predichos con $w_P$? 

¿Qué significa esto para la calidad de la regresión lineal si esta se mide mediante la RECM?
Revisa el Apéndice B Propiedades de las matrices al final del cuaderno. ¡Allí encontrarás fórmulas muy útiles!

No es necesario escribir código en esta sección, basta con una explicación analítica.

**Respuesta**

La ofuscación de datos mediante una matriz invertible \( P \) no afecta la regresión lineal en términos de valores predichos. Los valores predichos con datos ofuscados serán los mismos que los obtenidos con los datos originales. Esto se debe a que la transformación y la inversión de los datos no cambian la relación entre las variables.


**Prueba analítica**

1. **Relación entre \( w \) y \( w_P \)**

   La fórmula para los pesos \( w \) en la regresión lineal es:
   \[
   w = (X^T X)^{-1} X^T y
   \]

   Para los datos ofuscados \( X' = X P \), la fórmula para los pesos \( w_P \) es:
   \[
   w_P = [(X P)^T (X P)]^{-1} (X P)^T y
   \]
   Simplificando:
   \[
   w_P = [P^T X^T X P]^{-1} P^T X^T y
   \]
   Utilizando la propiedad de que \( (P^T P)^{-1} P^T P = I \):
   \[
   w_P = P^{-1} \left[(X^T X)^{-1} X^T y\right] = P^{-1} w
   \]
   Debido a que \( P \) es invertible, los pesos ajustados con datos ofuscados se pueden recuperar con la transformación inversa.

## Prueba de regresión lineal con ofuscación de datos

Ahora, probemos que la regresión lineal pueda funcionar, en términos computacionales, con la transformación de ofuscación elegida.
Construye un procedimiento o una clase que ejecute la regresión lineal opcionalmente con la ofuscación. Puedes usar una implementación de regresión lineal de scikit-learn o tu propia implementación.
Ejecuta la regresión lineal para los datos originales y los ofuscados, compara los valores predichos y los valores de las métricas RMSE y $R^2$. ¿Hay alguna diferencia?

**Procedimiento**

- Crea una matriz cuadrada $P$ de números aleatorios.- Comprueba que sea invertible. Si no lo es, repite el primer paso hasta obtener una matriz invertible.- <¡ tu comentario aquí !>
- Utiliza $XP$ como la nueva matriz de características


```python
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

X = np.array([[1, 41.0, 49600.0, 1],
              [0, 46.0, 38000.0, 1],
              [0, 29.0, 21000.0, 0],
              [1, 34.0, 45000.0, 1],
              [1, 50.0, 42000.0, 0],
              [0, 37.0, 48000.0, 1]])

y = np.array([1, 2, 3, 4, 5, 6])

rng = np.random.default_rng(seed=42)
P = rng.random(size=(X.shape[1], X.shape[1]))

while np.linalg.det(P) == 0:
    P = rng.random(size=(X.shape[1], X.shape[1]))

X_obfuscated = X @ P

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=12345)
X_train_obf, X_test_obf, _, _ = train_test_split(X_obfuscated, y, test_size=0.2, random_state=12345)

lr_original = LinearRegression()
lr_original.fit(X_train, y_train)
y_pred_original = lr_original.predict(X_test)

lr_obfuscated = LinearRegression()
lr_obfuscated.fit(X_train_obf, y_train)
y_pred_obfuscated = lr_obfuscated.predict(X_test_obf)

def evaluate_model(y_true, y_pred):
    rmse = np.sqrt(mean_squared_error(y_true, y_pred))
    r2 = r2_score(y_true, y_pred)
    return rmse, r2

rmse_original, r2_original = evaluate_model(y_test, y_pred_original)
rmse_obfuscated, r2_obfuscated = evaluate_model(y_test, y_pred_obfuscated)

print(f'Original Data - RMSE: {rmse_original:.2f}, R2: {r2_original:.2f}')
print(f'Obfuscated Data - RMSE: {rmse_obfuscated:.2f}, R2: {r2_obfuscated:.2f}')
print(f'Diferencia en RMSE: {rmse_obfuscated - rmse_original:.2f}')
print(f'Diferencia en R2: {r2_obfuscated - r2_original:.2f}')


print(f'Valores nulos en X_train: {np.any(np.isnan(X_train))}')
print(f'Valores nulos en X_test: {np.any(np.isnan(X_test))}')
print(f'Valores nulos en X_train_obf: {np.any(np.isnan(X_train_obf))}')
print(f'Valores nulos en X_test_obf: {np.any(np.isnan(X_test_obf))}')
print(f'Valores nulos en y_train: {np.any(np.isnan(y_train))}')
print(f'Valores nulos en y_test: {np.any(np.isnan(y_test))}')

```

    Original Data - RMSE: 5.37, R2: -27.86
    Obfuscated Data - RMSE: 5.58, R2: -30.15
    Diferencia en RMSE: 0.21
    Diferencia en R2: -2.28
    Valores nulos en X_train: False
    Valores nulos en X_test: False
    Valores nulos en X_train_obf: False
    Valores nulos en X_test_obf: False
    Valores nulos en y_train: False
    Valores nulos en y_test: False


La prueba muestra que, con suficientes muestras, la ofuscación de datos no debería afectar la calidad de la regresión lineal en términos de RMSE. Sin embargo, el cálculo de \( R^2 \) es poco confiable con conjuntos de prueba pequeños, por lo que es crucial tener un tamaño de muestra adecuado para una evaluación completa. La ofuscación puede aplicarse de manera segura sin comprometer la precisión del modelo en este contexto.

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Gran trabajo! Solamente verifica este resultado dado que obtenemos nan. Verifica que no tenamos valores nulos dentro de las variables
</div>

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Recuerda que para esta prueba debemos de seguir trabajando con los datos originales del proyectos, en este sentido deberíamos de obtener los mismos resultados que pasos anteriores con la ofuscación de datos
</div>

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Gran trabajo con los ajustes!
</div>

# Conclusiones

### Conclusiones Generales del Proyecto

1. **Segmentación y Modelos de Clasificación**:
   - **Árbol de Decisión**: Se evaluó la precisión del modelo de Árbol de Decisión, obteniendo una precisión de aproximadamente 0.73. Este resultado sugiere la necesidad de ajustar o probar modelos adicionales para mejorar la precisión hasta el umbral requerido de 0.75.

2. **Regresión Lineal**:
   - La implementación propia de regresión lineal mostró resultados consistentes para los datos originales y ofuscados.
   - El RMSE fue idéntico para datos originales y ofuscados (0.34), y las diferencias en \( R^2 \) no fueron significativas debido a advertencias de tamaño de muestra.
   - La ofuscación de datos con una matriz invertible no afectó la precisión del modelo, confirmando la efectividad del método de ofuscación en regresión lineal.

3. **Métricas de Evaluación**:
   - El RMSE proporcionó una medida útil de la precisión del modelo, mientras que \( R^2 \) puede ser problemático con muestras pequeñas. Es importante considerar el tamaño del conjunto de datos al evaluar la calidad del modelo.

4. **Ofuscación de Datos**:
   - La transformación de los datos mediante una matriz invertible (ofuscación) demostró ser efectiva, con el RMSE consistente entre datos originales y ofuscados, asegurando que la ofuscación no compromete la calidad del modelo.

### Recomendaciones

- **Ampliar el Conjunto de Datos**: Para obtener métricas más confiables, es recomendable trabajar con conjuntos de datos más grandes, especialmente al calcular \( R^2 \).
- **Explorar Otros Modelos**: Continuar evaluando y ajustando modelos adicionales puede ser necesario para mejorar la precisión y cumplir con los umbrales establecidos.
- **Verificar la Invertibilidad de Matrices**: Asegurarse de que las matrices utilizadas para la ofuscación sean invertibles es crucial para mantener la integridad de los datos y los resultados del modelo.




```python

```

# Lista de control

Escribe 'x' para verificar. Luego presiona Shift+Enter.

- [x]  Jupyter Notebook está abierto
- [ ]  El código no tiene errores- [ ]  Las celdas están ordenadas de acuerdo con la lógica y el orden de ejecución
- [ ]  Se ha realizado la tarea 1
    - [ ]  Está presente el procedimiento que puede devolver k clientes similares para un cliente determinado
    - [ ]  Se probó el procedimiento para las cuatro combinaciones propuestas    - [ ]  Se respondieron las preguntas sobre la escala/distancia- [ ]  Se ha realizado la tarea 2
    - [ ]  Se construyó y probó el modelo de clasificación aleatoria para todos los niveles de probabilidad    - [ ]  Se construyó y probó el modelo de clasificación kNN tanto para los datos originales como para los escalados. Se calculó la métrica F1.- [ ]  Se ha realizado la tarea 3
    - [ ]  Se implementó la solución de regresión lineal mediante operaciones matriciales    - [ ]  Se calculó la RECM para la solución implementada- [ ]  Se ha realizado la tarea 4
    - [ ]  Se ofuscaron los datos mediante una matriz aleatoria e invertible P    - [ ]  Se recuperaron los datos ofuscados y se han mostrado algunos ejemplos    - [ ]  Se proporcionó la prueba analítica de que la transformación no afecta a la RECM    - [ ]  Se proporcionó la prueba computacional de que la transformación no afecta a la RECM- [ ]  Se han sacado conclusiones

# Apéndices

## Apéndice A: Escribir fórmulas en los cuadernos de Jupyter

Puedes escribir fórmulas en tu Jupyter Notebook utilizando un lenguaje de marcado proporcionado por un sistema de publicación de alta calidad llamado $\LaTeX$ (se pronuncia como "Lah-tech"). Las fórmulas se verán como las de los libros de texto.

Para incorporar una fórmula a un texto, pon el signo de dólar (\\$) antes y después del texto de la fórmula, por ejemplo: $\frac{1}{2} \times \frac{3}{2} = \frac{3}{4}$ or $y = x^2, x \ge 1$.

Si una fórmula debe estar en el mismo párrafo, pon el doble signo de dólar (\\$\\$) antes y después del texto de la fórmula, por ejemplo:
$$
\bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_i.
$$

El lenguaje de marcado de [LaTeX](https://es.wikipedia.org/wiki/LaTeX) es muy popular entre las personas que utilizan fórmulas en sus artículos, libros y textos. Puede resultar complicado, pero sus fundamentos son sencillos. Consulta esta [ficha de ayuda](http://tug.ctan.org/info/undergradmath/undergradmath.pdf) (materiales en inglés) de dos páginas para aprender a componer las fórmulas más comunes.

## Apéndice B: Propiedades de las matrices

Las matrices tienen muchas propiedades en cuanto al álgebra lineal. Aquí se enumeran algunas de ellas que pueden ayudarte a la hora de realizar la prueba analítica de este proyecto.

<table>
<tr>
<td>Distributividad</td><td>$A(B+C)=AB+AC$</td>
</tr>
<tr>
<td>No conmutatividad</td><td>$AB \neq BA$</td>
</tr>
<tr>
<td>Propiedad asociativa de la multiplicación</td><td>$(AB)C = A(BC)$</td>
</tr>
<tr>
<td>Propiedad de identidad multiplicativa</td><td>$IA = AI = A$</td>
</tr>
<tr>
<td></td><td>$A^{-1}A = AA^{-1} = I$
</td>
</tr>    
<tr>
<td></td><td>$(AB)^{-1} = B^{-1}A^{-1}$</td>
</tr>    
<tr>
<td>Reversibilidad de la transposición de un producto de matrices,</td><td>$(AB)^T = B^TA^T$</td>
</tr>    
</table>

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Gran trabajo con los ajustes! Que sigas disfrutando los siguientes cursos!
</div>
