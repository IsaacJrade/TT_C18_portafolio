<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Excelente trabajo, Isaac! El desarrollo de la primera prueba de hipótesis es correcta, solamente recuerda que en la segunda prueba estamos buscando probar si el ingreso promedio de los usuarios del área NY-NJ es diferente al de los usuarios de otras regiones.

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Hola, Isaac! Muy buen trabajo, la forma en la que lo ajustate es correcta. Pero aún no logramos solucionar el problema. Para identificar el error te recomiendo realizar un análisis breve de estadistica descriptiva sobre esa variable que usas para la prueba par

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Hola, Isaac! Muy buen trabajo ya casi tienes el ejercicio, ya solucionaste la segunda prueba de hipótesis ya solamente verifica que las variables que usas para la primera no tienes valores nulos que esten haciendo que llegues a ese resultado.. 

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Hola, Isaac! Te recomiendo que te acerques con tu tutor dado que puede ser que tengamos algun error en el tema de valores nulos dentro de las variables que usamos en la prueba de hipótesis. Entonces el podría asesorte en este tema.

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Para correr la pruebas de hipótesis y que no salga el error que te aparece debes de colocar la librearia que tiene esa prueba. En este caso es stats, por lo que lo deberías de colocar como:
    
    stat.ttest_ind(surf_revenue, ultimate_revenue, equal_var=False)

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Hola, Isaac! Muy buen trabajo ya casi tienes el ejercicio, ya solucionaste la segunda prueba de hipótesis ya solamente verifica que las variables que usas para la primera no tienes valores nulos que esten haciendo que llegues a ese resultado.. 

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Hola, Isaac! Muy buen trabajo ya casi tienes el ejercicio, solamente verifica que en las pruebas de hipótesis cuents con las variables 'plan_name' y 'monthly_revenue' dentro de la base de datos que utilizas. 

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

# ¿Cuál es la mejor tarifa?

Trabajas como analista para el operador de telecomunicaciones Megaline. La empresa ofrece a sus clientes dos tarifas de prepago, Surf y Ultimate. El departamento comercial quiere saber cuál de las tarifas genera más ingresos para poder ajustar el presupuesto de publicidad.

Vas a realizar un análisis preliminar de las tarifas basado en una selección de clientes relativamente pequeña. Tendrás los datos de 500 clientes de Megaline: quiénes son los clientes, de dónde son, qué tarifa usan, así como la cantidad de llamadas que hicieron y los mensajes de texto que enviaron en 2018. Tu trabajo es analizar el comportamiento de los clientes y determinar qué tarifa de prepago genera más ingresos.

[Te proporcionamos algunos comentarios para orientarte mientras completas este proyecto. Pero debes asegurarte de eliminar todos los comentarios entre corchetes antes de entregar tu proyecto.]

[Antes de sumergirte en el análisis de datos, explica por tu propia cuenta el propósito del proyecto y las acciones que planeas realizar.]

[Ten en cuenta que estudiar, modificar y analizar datos es un proceso iterativo. Es normal volver a los pasos anteriores y corregirlos/ampliarlos para permitir nuevos pasos.]

## Inicialización


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats
import math
# Cargar todas las librerías


```

<div class="alert alert-block alert-warning">
<b>Comentario revisor</b> <a class="tocSkip"></a>


Recomiendo cargar la libreria math. De esta manera, puedes realizar redondeos con otros métodos. 
</div>

## Cargar datos


```python
calls = pd.read_csv('/datasets/megaline_calls.csv')
internet = pd.read_csv('/datasets/megaline_internet.csv')
messages = pd.read_csv('/datasets/megaline_messages.csv')
plans = pd.read_csv('/datasets/megaline_plans.csv')
users = pd.read_csv('/datasets/megaline_users.csv')# Carga los archivos de datos en diferentes DataFrames


```

## Preparar los datos

[Los datos para este proyecto se dividen en varias tablas. Explora cada una para tener una comprensión inicial de los datos. Si es necesario, haz las correcciones requeridas en cada tabla.]

## Tarifas


```python
plans.info()# Imprime la información general/resumida sobre el DataFrame de las tarifas


```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2 entries, 0 to 1
    Data columns (total 8 columns):
     #   Column                 Non-Null Count  Dtype  
    ---  ------                 --------------  -----  
     0   messages_included      2 non-null      int64  
     1   mb_per_month_included  2 non-null      int64  
     2   minutes_included       2 non-null      int64  
     3   usd_monthly_pay        2 non-null      int64  
     4   usd_per_gb             2 non-null      int64  
     5   usd_per_message        2 non-null      float64
     6   usd_per_minute         2 non-null      float64
     7   plan_name              2 non-null      object 
    dtypes: float64(2), int64(5), object(1)
    memory usage: 256.0+ bytes



```python
plans.head()# Imprime una muestra de los datos para las tarifas


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
      <th>messages_included</th>
      <th>mb_per_month_included</th>
      <th>minutes_included</th>
      <th>usd_monthly_pay</th>
      <th>usd_per_gb</th>
      <th>usd_per_message</th>
      <th>usd_per_minute</th>
      <th>plan_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>50</td>
      <td>15360</td>
      <td>500</td>
      <td>20</td>
      <td>10</td>
      <td>0.03</td>
      <td>0.03</td>
      <td>surf</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1000</td>
      <td>30720</td>
      <td>3000</td>
      <td>70</td>
      <td>7</td>
      <td>0.01</td>
      <td>0.01</td>
      <td>ultimate</td>
    </tr>
  </tbody>
</table>
</div>



El DataFrame tiene dos filas, una para cada plan de tarifa ("surf" y "ultimate").
No hay valores nulos en ninguna de las columnas.

Las columnas messages_included, mb_per_month_included, minutes_included, usd_monthly_pay, y usd_per_gb son de tipo(int64) usd_per_message y usd_per_minute son de tipo (float64). 
plan_name es de tipo (object).

convertir usd_monthly_pay a tipo flotante.
La columna plan_name es de tipo objeto, pero podríamos considerar cambiarla a un tipo categórico para un manejo más eficiente.

## Corregir datos

[Corrige los problemas obvios con los datos basándote en las observaciones iniciales.]


```python
plans['usd_monthly_pay'] = plans['usd_monthly_pay'].astype(float)
plans['plan_name'] = plans['plan_name'].astype('category')
```

## Enriquecer los datos

Podemos sacar la duración promedio de llamadas y  la cantidad promedio de mensajes por usuario. Tambien el volumen promedio de datos consumidos por usuario


```python
calls_mean = calls.groupby('user_id')['duration'].mean()

messages_mean = messages.groupby('user_id').size().mean()

internet_mean = internet.groupby('user_id')['mb_used'].mean()

print(calls_mean)

print(messages_mean)

print(internet_mean)

internet_mean_gb = internet_mean / 1024
print("\nVolumen promedio de datos consumidos por usuario (en GB):")
print(internet_mean_gb)
```

    user_id
    1000    7.301875
    1001    6.285287
    1002    6.877257
    1003    6.986577
    1004    7.078243
              ...   
    1495    6.586601
    1496    7.057487
    1497    5.120926
    1498    6.718337
    1499    7.109363
    Name: duration, Length: 481, dtype: float64
    189.181592039801
    user_id
    1000    380.294000
    1001    328.318122
    1002    324.946210
    1003    520.079615
    1004    339.897413
               ...    
    1495    341.003310
    1496    285.638400
    1497    358.275806
    1498    346.309178
    1499    324.319227
    Name: mb_used, Length: 489, dtype: float64
    
    Volumen promedio de datos consumidos por usuario (en GB):
    user_id
    1000    0.371381
    1001    0.320623
    1002    0.317330
    1003    0.507890
    1004    0.331931
              ...   
    1495    0.333011
    1496    0.278944
    1497    0.349879
    1498    0.338193
    1499    0.316718
    Name: mb_used, Length: 489, dtype: float64


<div class="alert alert-block alert-warning">
<b>Comentario Revisor</b> <a class="tocSkip"></a>

Muy buen trabajo, solamente te sugiero que en este apartado menciones un poco sobre la transformación que se debe realizar de megabytes a gigabytes. 
</div>

## Usuarios/as


```python
users.info()# Imprime la información general/resumida sobre el DataFrame de usuarios


```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 500 entries, 0 to 499
    Data columns (total 8 columns):
     #   Column      Non-Null Count  Dtype 
    ---  ------      --------------  ----- 
     0   user_id     500 non-null    int64 
     1   first_name  500 non-null    object
     2   last_name   500 non-null    object
     3   age         500 non-null    int64 
     4   city        500 non-null    object
     5   reg_date    500 non-null    object
     6   plan        500 non-null    object
     7   churn_date  34 non-null     object
    dtypes: int64(2), object(6)
    memory usage: 31.4+ KB



```python
users.head(20)# Imprime una muestra de datos para usuarios


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
      <th>user_id</th>
      <th>first_name</th>
      <th>last_name</th>
      <th>age</th>
      <th>city</th>
      <th>reg_date</th>
      <th>plan</th>
      <th>churn_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000</td>
      <td>Anamaria</td>
      <td>Bauer</td>
      <td>45</td>
      <td>Atlanta-Sandy Springs-Roswell, GA MSA</td>
      <td>2018-12-24</td>
      <td>ultimate</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1001</td>
      <td>Mickey</td>
      <td>Wilkerson</td>
      <td>28</td>
      <td>Seattle-Tacoma-Bellevue, WA MSA</td>
      <td>2018-08-13</td>
      <td>surf</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1002</td>
      <td>Carlee</td>
      <td>Hoffman</td>
      <td>36</td>
      <td>Las Vegas-Henderson-Paradise, NV MSA</td>
      <td>2018-10-21</td>
      <td>surf</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1003</td>
      <td>Reynaldo</td>
      <td>Jenkins</td>
      <td>52</td>
      <td>Tulsa, OK MSA</td>
      <td>2018-01-28</td>
      <td>surf</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1004</td>
      <td>Leonila</td>
      <td>Thompson</td>
      <td>40</td>
      <td>Seattle-Tacoma-Bellevue, WA MSA</td>
      <td>2018-05-23</td>
      <td>surf</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1005</td>
      <td>Livia</td>
      <td>Shields</td>
      <td>31</td>
      <td>Dallas-Fort Worth-Arlington, TX MSA</td>
      <td>2018-11-29</td>
      <td>surf</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1006</td>
      <td>Jesusa</td>
      <td>Bradford</td>
      <td>73</td>
      <td>San Francisco-Oakland-Berkeley, CA MSA</td>
      <td>2018-11-27</td>
      <td>ultimate</td>
      <td>2018-12-18</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1007</td>
      <td>Eusebio</td>
      <td>Welch</td>
      <td>42</td>
      <td>Grand Rapids-Kentwood, MI MSA</td>
      <td>2018-07-11</td>
      <td>surf</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1008</td>
      <td>Emely</td>
      <td>Hoffman</td>
      <td>53</td>
      <td>Orlando-Kissimmee-Sanford, FL MSA</td>
      <td>2018-08-03</td>
      <td>ultimate</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1009</td>
      <td>Gerry</td>
      <td>Little</td>
      <td>19</td>
      <td>San Jose-Sunnyvale-Santa Clara, CA MSA</td>
      <td>2018-04-22</td>
      <td>surf</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1010</td>
      <td>Wilber</td>
      <td>Blair</td>
      <td>52</td>
      <td>Dallas-Fort Worth-Arlington, TX MSA</td>
      <td>2018-03-09</td>
      <td>surf</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1011</td>
      <td>Halina</td>
      <td>Henry</td>
      <td>73</td>
      <td>Cleveland-Elyria, OH MSA</td>
      <td>2018-01-18</td>
      <td>ultimate</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1012</td>
      <td>Jonelle</td>
      <td>Mcbride</td>
      <td>59</td>
      <td>Chicago-Naperville-Elgin, IL-IN-WI MSA</td>
      <td>2018-06-28</td>
      <td>surf</td>
      <td>2018-11-16</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1013</td>
      <td>Nicolas</td>
      <td>Snider</td>
      <td>50</td>
      <td>Knoxville, TN MSA</td>
      <td>2018-12-01</td>
      <td>ultimate</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1014</td>
      <td>Edmundo</td>
      <td>Simon</td>
      <td>61</td>
      <td>New York-Newark-Jersey City, NY-NJ-PA MSA</td>
      <td>2018-11-25</td>
      <td>surf</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1015</td>
      <td>Beata</td>
      <td>Carpenter</td>
      <td>26</td>
      <td>Pittsburgh, PA MSA</td>
      <td>2018-12-05</td>
      <td>surf</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1016</td>
      <td>Jann</td>
      <td>Salinas</td>
      <td>30</td>
      <td>Fresno, CA MSA</td>
      <td>2018-10-25</td>
      <td>surf</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1017</td>
      <td>Boris</td>
      <td>Gates</td>
      <td>61</td>
      <td>Washington-Arlington-Alexandria, DC-VA-MD-WV MSA</td>
      <td>2018-08-26</td>
      <td>surf</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1018</td>
      <td>Dennis</td>
      <td>Grimes</td>
      <td>70</td>
      <td>Indianapolis-Carmel-Anderson, IN MSA</td>
      <td>2018-10-17</td>
      <td>surf</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1019</td>
      <td>Shizue</td>
      <td>Landry</td>
      <td>34</td>
      <td>Jacksonville, FL MSA</td>
      <td>2018-01-16</td>
      <td>surf</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



El DataFrame tiene 500 filas y 8 columnas.
La columna churn_date tiene 34 valores no nulos, algunos usuarios dejaron de usar el servicio. Las fechas nulas indican que los usuarios todavía están activos.

Las columnas reg_date y churn_date están tipo (object). debemos convertirlas a fecha


### Corregir los datos

Las columnas reg_date y churn_date deberían convertirse a tipos de datos de fecha


```python
users['reg_date'] = pd.to_datetime(users['reg_date'], format='%Y-%m-%d')
users['churn_date'] = pd.to_datetime(users['churn_date'], format='%Y-%m-%d', errors='coerce')
```

### Enriquecer los datos

podemos sacar el promedio de edad de los clientes


```python
age_mean = users['age'].mean()

age_mean

users_with_churn_date = users.dropna(subset=['churn_date'])

users_without_churn_date = users[users['churn_date'].isna()]

mean_age_with_churn_date = users_with_churn_date['age'].mean()
mean_age_without_churn_date = users_without_churn_date['age'].mean()

print("Edad promedio de usuarios con 'churn_date':", mean_age_with_churn_date)
print("Edad promedio de usuarios sin 'churn_date':", mean_age_without_churn_date)

```

    Edad promedio de usuarios con 'churn_date': 45.61764705882353
    Edad promedio de usuarios sin 'churn_date': 45.47639484978541


<div class="alert alert-block alert-warning">
<b>Comentario Revisor</b> <a class="tocSkip"></a>

Muy buena conclusión, pero a manera de complementar el análisis qué podríamos decir de los registros que no tienen valores en la variable churn_date?
</div>

## Llamadas


```python
calls.info()# Imprime la información general/resumida sobre el DataFrame de las llamadas


```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 137735 entries, 0 to 137734
    Data columns (total 4 columns):
     #   Column     Non-Null Count   Dtype  
    ---  ------     --------------   -----  
     0   id         137735 non-null  object 
     1   user_id    137735 non-null  int64  
     2   call_date  137735 non-null  object 
     3   duration   137735 non-null  float64
    dtypes: float64(1), int64(1), object(2)
    memory usage: 4.2+ MB



```python
calls.head(20)# Imprime una muestra de datos para las llamadas


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
      <th>id</th>
      <th>user_id</th>
      <th>call_date</th>
      <th>duration</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000_93</td>
      <td>1000</td>
      <td>2018-12-27</td>
      <td>8.52</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1000_145</td>
      <td>1000</td>
      <td>2018-12-27</td>
      <td>13.66</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1000_247</td>
      <td>1000</td>
      <td>2018-12-27</td>
      <td>14.48</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1000_309</td>
      <td>1000</td>
      <td>2018-12-28</td>
      <td>5.76</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1000_380</td>
      <td>1000</td>
      <td>2018-12-30</td>
      <td>4.22</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1000_388</td>
      <td>1000</td>
      <td>2018-12-31</td>
      <td>2.20</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1000_510</td>
      <td>1000</td>
      <td>2018-12-27</td>
      <td>5.75</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1000_521</td>
      <td>1000</td>
      <td>2018-12-28</td>
      <td>14.18</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1000_530</td>
      <td>1000</td>
      <td>2018-12-28</td>
      <td>5.77</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1000_544</td>
      <td>1000</td>
      <td>2018-12-26</td>
      <td>4.40</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1000_693</td>
      <td>1000</td>
      <td>2018-12-31</td>
      <td>4.31</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1000_705</td>
      <td>1000</td>
      <td>2018-12-31</td>
      <td>12.78</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1000_735</td>
      <td>1000</td>
      <td>2018-12-29</td>
      <td>1.70</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1000_778</td>
      <td>1000</td>
      <td>2018-12-28</td>
      <td>3.29</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1000_826</td>
      <td>1000</td>
      <td>2018-12-26</td>
      <td>9.96</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1000_842</td>
      <td>1000</td>
      <td>2018-12-27</td>
      <td>5.85</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1001_0</td>
      <td>1001</td>
      <td>2018-09-06</td>
      <td>10.06</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1001_1</td>
      <td>1001</td>
      <td>2018-10-12</td>
      <td>1.00</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1001_2</td>
      <td>1001</td>
      <td>2018-10-17</td>
      <td>15.83</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1001_4</td>
      <td>1001</td>
      <td>2018-12-05</td>
      <td>0.00</td>
    </tr>
  </tbody>
</table>
</div>



El DataFrame de llamadas contiene 137,735 entradas y 4 columnas.
La columna call_date debería convertirse a un tipo de datos de fecha, esta tipo (object)
No hay valores nulos en ninguna de las columnas.

La duración de la llamada está representada en minutos en la columna duration.

Algunas llamadas tienen una duración de 0.00, lo que podría indicar llamadas perdidas.



### Corregir los datos

La columna call_date debería convertirse a un tipo de datos de fecha.


```python
calls['call_date'] = pd.to_datetime(calls['call_date'], format='%Y-%m-%d')
```

### Enriquecer los datos

promedio de duracion de llamadas por usuario


```python
average_call_duration = calls.groupby('user_id')['duration'].mean()

average_call_duration

calls['duration_rounded'] = calls['duration'].apply(lambda x: math.ceil(x))

average_call_duration = calls.groupby('user_id')['duration_rounded'].mean()


average_call_duration

calls_with_zero_duration = calls[calls['duration'] == 0]
print("Número de llamadas con duración igual a 0:", len(calls_with_zero_duration))
```

    Número de llamadas con duración igual a 0: 26834


<div class="alert alert-block alert-warning">
<b>Comentario revisor</b> <a class="tocSkip"></a>


Recuerda que es necesario redondear la duración de las llamadas  hacia arriba lo valores, dado que para este ejercicio debemos hacer el redondeo superior dado que se cobra el costo extra en cuanto se pasa de los límites.
</div>

<div class="alert alert-block alert-warning">
<b>Comentario Revisor</b> <a class="tocSkip"></a>

Qué podríamos decir hasta el momento de las llamadas que tienen una duración de 0?
</div>

## Mensajes


```python
messages.info()# Imprime la información general/resumida sobre el DataFrame de los mensajes


```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 76051 entries, 0 to 76050
    Data columns (total 3 columns):
     #   Column        Non-Null Count  Dtype 
    ---  ------        --------------  ----- 
     0   id            76051 non-null  object
     1   user_id       76051 non-null  int64 
     2   message_date  76051 non-null  object
    dtypes: int64(1), object(2)
    memory usage: 1.7+ MB



```python
messages.head(20)# Imprime una muestra de datos para los mensajes


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
      <th>id</th>
      <th>user_id</th>
      <th>message_date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000_125</td>
      <td>1000</td>
      <td>2018-12-27</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1000_160</td>
      <td>1000</td>
      <td>2018-12-31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1000_223</td>
      <td>1000</td>
      <td>2018-12-31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1000_251</td>
      <td>1000</td>
      <td>2018-12-27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1000_255</td>
      <td>1000</td>
      <td>2018-12-26</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1000_346</td>
      <td>1000</td>
      <td>2018-12-29</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1000_386</td>
      <td>1000</td>
      <td>2018-12-30</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1000_413</td>
      <td>1000</td>
      <td>2018-12-31</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1000_502</td>
      <td>1000</td>
      <td>2018-12-27</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1000_525</td>
      <td>1000</td>
      <td>2018-12-28</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1000_567</td>
      <td>1000</td>
      <td>2018-12-25</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1001_1</td>
      <td>1001</td>
      <td>2018-11-14</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1001_2</td>
      <td>1001</td>
      <td>2018-08-17</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1001_5</td>
      <td>1001</td>
      <td>2018-12-05</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1001_7</td>
      <td>1001</td>
      <td>2018-11-28</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1001_9</td>
      <td>1001</td>
      <td>2018-10-23</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1001_10</td>
      <td>1001</td>
      <td>2018-09-01</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1001_11</td>
      <td>1001</td>
      <td>2018-11-18</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1001_17</td>
      <td>1001</td>
      <td>2018-12-11</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1001_18</td>
      <td>1001</td>
      <td>2018-10-01</td>
    </tr>
  </tbody>
</table>
</div>



El DataFrame tiene un total de 76,051 entradas. 
No hay valores nulos en ninguna de las columnas

la columna message_date se almacena actualmente como tipo de dato object, se debe de corregir a tipo fecha

### Corregir los datos

corregir el tipo de dato de la columna message_date a fecha


```python
messages['message_date'] = pd.to_datetime(messages['message_date'], format='%Y-%m-%d')
```

### Enriquecer los datos

agregar una columna que represente el mes en el que se envió cada mensaje


```python
messages['message_month'] = messages['message_date'].dt.month
```

## Internet


```python
internet.info()# Imprime la información general/resumida sobre el DataFrame de internet


```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 104825 entries, 0 to 104824
    Data columns (total 4 columns):
     #   Column        Non-Null Count   Dtype  
    ---  ------        --------------   -----  
     0   id            104825 non-null  object 
     1   user_id       104825 non-null  int64  
     2   session_date  104825 non-null  object 
     3   mb_used       104825 non-null  float64
    dtypes: float64(1), int64(1), object(2)
    memory usage: 3.2+ MB



```python
internet.head(20)# Imprime una muestra de datos para el tráfico de internet


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
      <th>id</th>
      <th>user_id</th>
      <th>session_date</th>
      <th>mb_used</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000_13</td>
      <td>1000</td>
      <td>2018-12-29</td>
      <td>89.86</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1000_204</td>
      <td>1000</td>
      <td>2018-12-31</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1000_379</td>
      <td>1000</td>
      <td>2018-12-28</td>
      <td>660.40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1000_413</td>
      <td>1000</td>
      <td>2018-12-26</td>
      <td>270.99</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1000_442</td>
      <td>1000</td>
      <td>2018-12-27</td>
      <td>880.22</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1001_0</td>
      <td>1001</td>
      <td>2018-08-24</td>
      <td>284.68</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1001_3</td>
      <td>1001</td>
      <td>2018-12-09</td>
      <td>656.04</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1001_4</td>
      <td>1001</td>
      <td>2018-11-04</td>
      <td>16.97</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1001_10</td>
      <td>1001</td>
      <td>2018-11-27</td>
      <td>135.18</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1001_15</td>
      <td>1001</td>
      <td>2018-12-13</td>
      <td>761.92</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1001_16</td>
      <td>1001</td>
      <td>2018-10-28</td>
      <td>501.53</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1001_17</td>
      <td>1001</td>
      <td>2018-09-05</td>
      <td>727.29</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1001_24</td>
      <td>1001</td>
      <td>2018-09-05</td>
      <td>622.03</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1001_25</td>
      <td>1001</td>
      <td>2018-10-14</td>
      <td>310.43</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1001_26</td>
      <td>1001</td>
      <td>2018-09-17</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1001_27</td>
      <td>1001</td>
      <td>2018-12-13</td>
      <td>149.17</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1001_28</td>
      <td>1001</td>
      <td>2018-10-17</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1001_29</td>
      <td>1001</td>
      <td>2018-10-09</td>
      <td>1067.99</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1001_30</td>
      <td>1001</td>
      <td>2018-12-27</td>
      <td>157.20</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1001_33</td>
      <td>1001</td>
      <td>2018-09-27</td>
      <td>236.40</td>
    </tr>
  </tbody>
</table>
</div>



Hay 104,825 entradas y 4 columnas. 
Las columnas "id" y "session_date" son de tipo objeto 
"user_id" es de tipo entero (int64) 
"mb_used" es de tipo flotante (float64).



### Corregir los datos

Convertir la columna "session_date" al formato de fecha.


```python
internet['session_date'] = pd.to_datetime(internet['session_date'], format='%Y-%m-%d')
```

### Enriquecer los datos

promedio de mb usados


```python
mb_mean = internet['mb_used'].mean()
mb_mean_gb = np.ceil(mb_mean / 1024)

mb_mean
mb_mean_gb
```




    1.0



<div class="alert alert-block alert-warning">
<b>Comentario revisor</b> <a class="tocSkip"></a>


Te recomiendo solamente comentar que cuando agrupemos los datos vamos a tener que redondear hacia arriba lo valores de la transformación de mbegabyter a gigabyte, para este ejercicio debemos hacer el redondeo superior dado que se cobra el costo extra en cuanto se pasa de los límites.Por lo que es necesario hacer la transformación de mb a gb y después hacer el redondeo.  
</div>

<div class="alert alert-block alert-warning">
<b>Comentario Revisor</b> <a class="tocSkip"></a>

Cuando hacemos análisis de datos, un paso que es muy importate realizar es verificar que no se tengan duplicados en nuestras bases de datos y en caso de tener duplicados entender si hace sentido su duplicación o solamente son errores de registro. En este sentido sería importante que para todas las bases de datos desarrolles un análisis de registros duplicados.
    
</div>

## Estudiar las condiciones de las tarifas

Plan "Surf":

Mensajes incluidos: 50
Datos (en MB) incluidos por mes: 15,360
Minutos incluidos: 500
Precio mensual en USD: $20.0
Costo adicional por GB de datos excedido: $10.0
Costo adicional por mensaje: $0.03
Costo adicional por minuto: $0.03
Plan "Ultimate":

Mensajes incluidos: 1,000
Datos (en MB) incluidos por mes: 30,720
Minutos incluidos: 3,000
Precio mensual en USD: $70.0
Costo adicional por GB de datos excedido: $7.0
Costo adicional por mensaje: $0.01
Costo adicional por minuto: $0.01


```python
plans# Imprime las condiciones de la tarifa y asegúrate de que te quedan claras


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
      <th>messages_included</th>
      <th>mb_per_month_included</th>
      <th>minutes_included</th>
      <th>usd_monthly_pay</th>
      <th>usd_per_gb</th>
      <th>usd_per_message</th>
      <th>usd_per_minute</th>
      <th>plan_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>50</td>
      <td>15360</td>
      <td>500</td>
      <td>20.0</td>
      <td>10</td>
      <td>0.03</td>
      <td>0.03</td>
      <td>surf</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1000</td>
      <td>30720</td>
      <td>3000</td>
      <td>70.0</td>
      <td>7</td>
      <td>0.01</td>
      <td>0.01</td>
      <td>ultimate</td>
    </tr>
  </tbody>
</table>
</div>



## Agregar datos por usuario

[Ahora que los datos están limpios, agrega los datos por usuario y por periodo para que solo haya un registro por usuario y por periodo. Esto facilitará mucho el análisis posterior.]


```python
calls['call_date'] = pd.to_datetime(calls['call_date'])
calls['month'] = calls['call_date'].dt.to_period('M')
calls_per_user_month = calls.groupby(['user_id', 'month']).size().reset_index(name='calls_count')
calls_per_user_month.head(20)# Calcula el número de llamadas hechas por cada usuario al mes. Guarda el resultado.

pivot_calls = calls.pivot_table(index=['user_id', 'month'],
                                values=['duration'],
                                aggfunc=['sum', 'count']).reset_index()

pivot_calls
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>user_id</th>
      <th>month</th>
      <th>sum</th>
      <th>count</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th></th>
      <th>duration</th>
      <th>duration</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000</td>
      <td>2018-12</td>
      <td>116.83</td>
      <td>16</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1001</td>
      <td>2018-08</td>
      <td>171.14</td>
      <td>27</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1001</td>
      <td>2018-09</td>
      <td>297.69</td>
      <td>49</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1001</td>
      <td>2018-10</td>
      <td>374.11</td>
      <td>65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1001</td>
      <td>2018-11</td>
      <td>404.59</td>
      <td>64</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2253</th>
      <td>1498</td>
      <td>2018-12</td>
      <td>324.77</td>
      <td>39</td>
    </tr>
    <tr>
      <th>2254</th>
      <td>1499</td>
      <td>2018-09</td>
      <td>330.37</td>
      <td>41</td>
    </tr>
    <tr>
      <th>2255</th>
      <td>1499</td>
      <td>2018-10</td>
      <td>363.28</td>
      <td>53</td>
    </tr>
    <tr>
      <th>2256</th>
      <td>1499</td>
      <td>2018-11</td>
      <td>288.56</td>
      <td>45</td>
    </tr>
    <tr>
      <th>2257</th>
      <td>1499</td>
      <td>2018-12</td>
      <td>468.10</td>
      <td>65</td>
    </tr>
  </tbody>
</table>
<p>2258 rows × 4 columns</p>
</div>



<div class="alert alert-block alert-warning">

<b>Comentario revisor</b> <a class="tocSkip"></a>

Si bien es correcta la forma de agrupar para sacar la duración de las llamadas por cada ususario, para proximas ocasiones puedes hacer uso de la siguiente forma:
    
    pivot_calls = calls.pivot_table(index=['user_id', 'month'],
                                values=['duration'],
                                aggfunc=['sum','count']).reset_index()

</div>




```python
minutes_per_user_month = calls.groupby(['user_id', 'month'])['duration'].sum().reset_index(name='minutes_used')
minutes_per_user_month.head(20)# Calcula la cantidad de minutos usados por cada usuario al mes. Guarda el resultado.


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
      <th>user_id</th>
      <th>month</th>
      <th>minutes_used</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000</td>
      <td>2018-12</td>
      <td>116.83</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1001</td>
      <td>2018-08</td>
      <td>171.14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1001</td>
      <td>2018-09</td>
      <td>297.69</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1001</td>
      <td>2018-10</td>
      <td>374.11</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1001</td>
      <td>2018-11</td>
      <td>404.59</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1001</td>
      <td>2018-12</td>
      <td>392.93</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1002</td>
      <td>2018-10</td>
      <td>54.13</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1002</td>
      <td>2018-11</td>
      <td>359.76</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1002</td>
      <td>2018-12</td>
      <td>363.24</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1003</td>
      <td>2018-12</td>
      <td>1041.00</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1004</td>
      <td>2018-05</td>
      <td>181.58</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1004</td>
      <td>2018-06</td>
      <td>261.32</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1004</td>
      <td>2018-07</td>
      <td>358.45</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1004</td>
      <td>2018-08</td>
      <td>334.86</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1004</td>
      <td>2018-09</td>
      <td>284.60</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1004</td>
      <td>2018-10</td>
      <td>341.63</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1004</td>
      <td>2018-11</td>
      <td>452.98</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1004</td>
      <td>2018-12</td>
      <td>403.53</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1005</td>
      <td>2018-12</td>
      <td>470.22</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1006</td>
      <td>2018-11</td>
      <td>9.32</td>
    </tr>
  </tbody>
</table>
</div>




```python
messages['message_date'] = pd.to_datetime(messages['message_date'])
messages['month'] = messages['message_date'].dt.to_period('M')
messages_per_user_month = messages.groupby(['user_id', 'month']).size().reset_index(name='messages_count')
messages_per_user_month.head(20)# Calcula el número de mensajes enviados por cada usuario al mes. Guarda el resultado.


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
      <th>user_id</th>
      <th>month</th>
      <th>messages_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000</td>
      <td>2018-12</td>
      <td>11</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1001</td>
      <td>2018-08</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1001</td>
      <td>2018-09</td>
      <td>44</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1001</td>
      <td>2018-10</td>
      <td>53</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1001</td>
      <td>2018-11</td>
      <td>36</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1001</td>
      <td>2018-12</td>
      <td>44</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1002</td>
      <td>2018-10</td>
      <td>15</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1002</td>
      <td>2018-11</td>
      <td>32</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1002</td>
      <td>2018-12</td>
      <td>41</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1003</td>
      <td>2018-12</td>
      <td>50</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1004</td>
      <td>2018-05</td>
      <td>7</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1004</td>
      <td>2018-06</td>
      <td>18</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1004</td>
      <td>2018-07</td>
      <td>26</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1004</td>
      <td>2018-08</td>
      <td>25</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1004</td>
      <td>2018-09</td>
      <td>21</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1004</td>
      <td>2018-10</td>
      <td>24</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1004</td>
      <td>2018-11</td>
      <td>25</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1004</td>
      <td>2018-12</td>
      <td>31</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1005</td>
      <td>2018-12</td>
      <td>11</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1006</td>
      <td>2018-11</td>
      <td>15</td>
    </tr>
  </tbody>
</table>
</div>




```python
internet['session_date'] = pd.to_datetime(internet['session_date'])
internet['month'] = internet['session_date'].dt.to_period('M')
traffic_per_user_month = internet.groupby(['user_id', 'month'])['mb_used'].sum().reset_index(name='mb_used')
traffic_per_user_month.head(20)# Calcula el volumen del tráfico de Internet usado por cada usuario al mes. Guarda el resultado.


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
      <th>user_id</th>
      <th>month</th>
      <th>mb_used</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000</td>
      <td>2018-12</td>
      <td>1901.47</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1001</td>
      <td>2018-08</td>
      <td>6919.15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1001</td>
      <td>2018-09</td>
      <td>13314.82</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1001</td>
      <td>2018-10</td>
      <td>22330.49</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1001</td>
      <td>2018-11</td>
      <td>18504.30</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1001</td>
      <td>2018-12</td>
      <td>19369.18</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1002</td>
      <td>2018-10</td>
      <td>6552.01</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1002</td>
      <td>2018-11</td>
      <td>19345.08</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1002</td>
      <td>2018-12</td>
      <td>14396.24</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1003</td>
      <td>2018-12</td>
      <td>27044.14</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1004</td>
      <td>2018-05</td>
      <td>6547.21</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1004</td>
      <td>2018-06</td>
      <td>20672.82</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1004</td>
      <td>2018-07</td>
      <td>24516.62</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1004</td>
      <td>2018-08</td>
      <td>27981.74</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1004</td>
      <td>2018-09</td>
      <td>18852.72</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1004</td>
      <td>2018-10</td>
      <td>14541.63</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1004</td>
      <td>2018-11</td>
      <td>21850.78</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1004</td>
      <td>2018-12</td>
      <td>21389.29</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1005</td>
      <td>2018-12</td>
      <td>17140.17</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1006</td>
      <td>2018-11</td>
      <td>2068.37</td>
    </tr>
  </tbody>
</table>
</div>



[Junta los datos agregados en un DataFrame para que haya un registro que represente lo que consumió un usuario único en un mes determinado.]


```python
merged_data = pd.merge(calls_per_user_month, minutes_per_user_month, on=['user_id', 'month'], how='outer')
merged_data = pd.merge(merged_data, messages_per_user_month, on=['user_id', 'month'], how='outer')
merged_data = pd.merge(merged_data, traffic_per_user_month, on=['user_id', 'month'], how='outer')

print(merged_data.head(20))# Fusiona los datos de llamadas, minutos, mensajes e Internet con base en user_id y month


```

        user_id    month  calls_count  minutes_used  messages_count   mb_used
    0      1000  2018-12         16.0        116.83            11.0   1901.47
    1      1001  2018-08         27.0        171.14            30.0   6919.15
    2      1001  2018-09         49.0        297.69            44.0  13314.82
    3      1001  2018-10         65.0        374.11            53.0  22330.49
    4      1001  2018-11         64.0        404.59            36.0  18504.30
    5      1001  2018-12         56.0        392.93            44.0  19369.18
    6      1002  2018-10         11.0         54.13            15.0   6552.01
    7      1002  2018-11         55.0        359.76            32.0  19345.08
    8      1002  2018-12         47.0        363.24            41.0  14396.24
    9      1003  2018-12        149.0       1041.00            50.0  27044.14
    10     1004  2018-05         21.0        181.58             7.0   6547.21
    11     1004  2018-06         44.0        261.32            18.0  20672.82
    12     1004  2018-07         49.0        358.45            26.0  24516.62
    13     1004  2018-08         49.0        334.86            25.0  27981.74
    14     1004  2018-09         42.0        284.60            21.0  18852.72
    15     1004  2018-10         61.0        341.63            24.0  14541.63
    16     1004  2018-11         54.0        452.98            25.0  21850.78
    17     1004  2018-12         50.0        403.53            31.0  21389.29
    18     1005  2018-12         59.0        470.22            11.0  17140.17
    19     1006  2018-11          2.0          9.32            15.0   2068.37



```python
merged_data_with_plan_info = pd.merge(merged_data, users[['user_id', 'plan']], on='user_id', how='left')
merged_data_with_tariff = pd.merge(merged_data_with_plan_info, plans, left_on='plan', right_on='plan_name', how='left')
merged_data_with_tariff.head()
# Añade la información de la tarifa


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
      <th>user_id</th>
      <th>month</th>
      <th>calls_count</th>
      <th>minutes_used</th>
      <th>messages_count</th>
      <th>mb_used</th>
      <th>plan</th>
      <th>messages_included</th>
      <th>mb_per_month_included</th>
      <th>minutes_included</th>
      <th>usd_monthly_pay</th>
      <th>usd_per_gb</th>
      <th>usd_per_message</th>
      <th>usd_per_minute</th>
      <th>plan_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000</td>
      <td>2018-12</td>
      <td>16.0</td>
      <td>116.83</td>
      <td>11.0</td>
      <td>1901.47</td>
      <td>ultimate</td>
      <td>1000</td>
      <td>30720</td>
      <td>3000</td>
      <td>70.0</td>
      <td>7</td>
      <td>0.01</td>
      <td>0.01</td>
      <td>ultimate</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1001</td>
      <td>2018-08</td>
      <td>27.0</td>
      <td>171.14</td>
      <td>30.0</td>
      <td>6919.15</td>
      <td>surf</td>
      <td>50</td>
      <td>15360</td>
      <td>500</td>
      <td>20.0</td>
      <td>10</td>
      <td>0.03</td>
      <td>0.03</td>
      <td>surf</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1001</td>
      <td>2018-09</td>
      <td>49.0</td>
      <td>297.69</td>
      <td>44.0</td>
      <td>13314.82</td>
      <td>surf</td>
      <td>50</td>
      <td>15360</td>
      <td>500</td>
      <td>20.0</td>
      <td>10</td>
      <td>0.03</td>
      <td>0.03</td>
      <td>surf</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1001</td>
      <td>2018-10</td>
      <td>65.0</td>
      <td>374.11</td>
      <td>53.0</td>
      <td>22330.49</td>
      <td>surf</td>
      <td>50</td>
      <td>15360</td>
      <td>500</td>
      <td>20.0</td>
      <td>10</td>
      <td>0.03</td>
      <td>0.03</td>
      <td>surf</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1001</td>
      <td>2018-11</td>
      <td>64.0</td>
      <td>404.59</td>
      <td>36.0</td>
      <td>18504.30</td>
      <td>surf</td>
      <td>50</td>
      <td>15360</td>
      <td>500</td>
      <td>20.0</td>
      <td>10</td>
      <td>0.03</td>
      <td>0.03</td>
      <td>surf</td>
    </tr>
  </tbody>
</table>
</div>



<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Muy buen trabajo!! el merge es correcto para unir todas las bases trabajadas.
    
</div>

[Calcula los ingresos mensuales por usuario (resta el límite del paquete gratuito del número total de llamadas, mensajes de texto y datos; multiplica el resultado por el valor del plan de llamadas; añade la tarifa mensual en función del plan de llamadas). Nota: Dadas las condiciones del plan, ¡esto podría no ser tan trivial como un par de líneas! Así que no pasa nada si dedicas algo de tiempo a ello.]


```python
merged_data_with_tariff['extra_calls'] = merged_data_with_tariff['calls_count'] - merged_data_with_tariff['minutes_included']
merged_data_with_tariff['extra_messages'] = merged_data_with_tariff['messages_count'] - merged_data_with_tariff['messages_included']
merged_data_with_tariff['extra_mb'] = merged_data_with_tariff['mb_used'] - merged_data_with_tariff['mb_per_month_included']


merged_data_with_tariff['extra_calls'] = merged_data_with_tariff['extra_calls'].apply(lambda x: max(x, 0))
merged_data_with_tariff['extra_messages'] = merged_data_with_tariff['extra_messages'].apply(lambda x: max(x, 0))
merged_data_with_tariff['extra_mb'] = merged_data_with_tariff['extra_mb'].apply(lambda x: max(x, 0))

merged_data_with_tariff['call_revenue'] = merged_data_with_tariff['extra_calls'] * merged_data_with_tariff['usd_per_minute']
merged_data_with_tariff['message_revenue'] = merged_data_with_tariff['extra_messages'] * merged_data_with_tariff['usd_per_message']
merged_data_with_tariff['data_revenue'] = (merged_data_with_tariff['extra_mb'] / 1024) * merged_data_with_tariff['usd_per_gb']  # Convertir de MB a GB

merged_data_with_tariff['monthly_revenue'] = (merged_data_with_tariff['call_revenue'] +
                                              merged_data_with_tariff['message_revenue'] +
                                              merged_data_with_tariff['data_revenue'] +
                                              merged_data_with_tariff['usd_monthly_pay'])

monthly_revenue_per_user = merged_data_with_tariff[['user_id', 'month', 'monthly_revenue']]
# Calcula el ingreso mensual para cada usuario

monthly_revenue_per_user
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
      <th>user_id</th>
      <th>month</th>
      <th>monthly_revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000</td>
      <td>2018-12</td>
      <td>70.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1001</td>
      <td>2018-08</td>
      <td>20.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1001</td>
      <td>2018-09</td>
      <td>20.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1001</td>
      <td>2018-10</td>
      <td>88.161191</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1001</td>
      <td>2018-11</td>
      <td>50.706055</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2288</th>
      <td>1349</td>
      <td>2018-12</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2289</th>
      <td>1361</td>
      <td>2018-05</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2290</th>
      <td>1482</td>
      <td>2018-10</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2291</th>
      <td>1108</td>
      <td>2018-12</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2292</th>
      <td>1311</td>
      <td>2018-06</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>2293 rows × 3 columns</p>
</div>




```python
merged_data_with_tariff.head()
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
      <th>user_id</th>
      <th>month</th>
      <th>calls_count</th>
      <th>minutes_used</th>
      <th>messages_count</th>
      <th>mb_used</th>
      <th>plan</th>
      <th>messages_included</th>
      <th>mb_per_month_included</th>
      <th>minutes_included</th>
      <th>...</th>
      <th>usd_per_message</th>
      <th>usd_per_minute</th>
      <th>plan_name</th>
      <th>extra_calls</th>
      <th>extra_messages</th>
      <th>extra_mb</th>
      <th>call_revenue</th>
      <th>message_revenue</th>
      <th>data_revenue</th>
      <th>monthly_revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000</td>
      <td>2018-12</td>
      <td>16.0</td>
      <td>116.83</td>
      <td>11.0</td>
      <td>1901.47</td>
      <td>ultimate</td>
      <td>1000</td>
      <td>30720</td>
      <td>3000</td>
      <td>...</td>
      <td>0.01</td>
      <td>0.01</td>
      <td>ultimate</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>70.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1001</td>
      <td>2018-08</td>
      <td>27.0</td>
      <td>171.14</td>
      <td>30.0</td>
      <td>6919.15</td>
      <td>surf</td>
      <td>50</td>
      <td>15360</td>
      <td>500</td>
      <td>...</td>
      <td>0.03</td>
      <td>0.03</td>
      <td>surf</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>20.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1001</td>
      <td>2018-09</td>
      <td>49.0</td>
      <td>297.69</td>
      <td>44.0</td>
      <td>13314.82</td>
      <td>surf</td>
      <td>50</td>
      <td>15360</td>
      <td>500</td>
      <td>...</td>
      <td>0.03</td>
      <td>0.03</td>
      <td>surf</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>20.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1001</td>
      <td>2018-10</td>
      <td>65.0</td>
      <td>374.11</td>
      <td>53.0</td>
      <td>22330.49</td>
      <td>surf</td>
      <td>50</td>
      <td>15360</td>
      <td>500</td>
      <td>...</td>
      <td>0.03</td>
      <td>0.03</td>
      <td>surf</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>6970.49</td>
      <td>0.0</td>
      <td>0.09</td>
      <td>68.071191</td>
      <td>88.161191</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1001</td>
      <td>2018-11</td>
      <td>64.0</td>
      <td>404.59</td>
      <td>36.0</td>
      <td>18504.30</td>
      <td>surf</td>
      <td>50</td>
      <td>15360</td>
      <td>500</td>
      <td>...</td>
      <td>0.03</td>
      <td>0.03</td>
      <td>surf</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3144.30</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>30.706055</td>
      <td>50.706055</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>



<div class="alert alert-block alert-danger">
<b>Comentario revisor</b> <a class="tocSkip"></a>


Muy buen trabajo, solamente cuando calculos el extra de llamadas, mensajes e internet, es necesari agregar que si la resta da como resultado un numero negativo, entonces el extra es 0. 
</div>

<div class="alert alert-block alert-danger">
<b>Comentario revisor</b> <a class="tocSkip"></a>


Por otro lado, recuerda que para este punto, es necesario que ya tengamos los valores redondeados de la duración de las llamadas y la transformación de megabytes a gigabytes. 
</div>


```python

```

## Estudia el comportamiento de usuario


```python

```

[Calcula algunas estadísticas descriptivas para los datos agregados y fusionados que nos sean útiles y que muestren un panorama general captado por los datos. Dibuja gráficos útiles para facilitar la comprensión. Dado que la tarea principal es comparar las tarifas y decidir cuál es más rentable, las estadísticas y gráficas deben calcularse por tarifa.]

[En los comentarios hallarás pistas relevantes para las llamadas, pero no las hay para los mensajes e Internet. Sin embargo, el principio del estudio estadístico que se aplica para ellos es el mismo que para las llamadas.]

### Llamadas


```python
avg_call_duration_by_plan = merged_data_with_tariff.groupby(['plan_name', 'month'])['minutes_used'].mean().reset_index()


plt.figure(figsize=(12, 6))
sns.barplot(x='month', y='minutes_used', hue='plan_name', data=avg_call_duration_by_plan)
plt.title('Duración Promedio de Llamadas por Plan y Mes')
plt.xlabel('Mes')
plt.ylabel('Duración Promedio de Llamadas (minutos)')
plt.xticks(rotation=45)
plt.legend(title='Plan')
plt.show()

avg_call_duration_by_plan# Compara la duración promedio de llamadas por cada plan y por cada mes. Traza un gráfico de barras para visualizarla.


```


    
![png](output_96_0.png)
    





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
      <th>plan_name</th>
      <th>month</th>
      <th>minutes_used</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>surf</td>
      <td>2018-01</td>
      <td>192.840000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>surf</td>
      <td>2018-02</td>
      <td>280.851111</td>
    </tr>
    <tr>
      <th>2</th>
      <td>surf</td>
      <td>2018-03</td>
      <td>310.970000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>surf</td>
      <td>2018-04</td>
      <td>332.380000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>surf</td>
      <td>2018-05</td>
      <td>387.108000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>surf</td>
      <td>2018-06</td>
      <td>411.450625</td>
    </tr>
    <tr>
      <th>6</th>
      <td>surf</td>
      <td>2018-07</td>
      <td>428.060917</td>
    </tr>
    <tr>
      <th>7</th>
      <td>surf</td>
      <td>2018-08</td>
      <td>394.474717</td>
    </tr>
    <tr>
      <th>8</th>
      <td>surf</td>
      <td>2018-09</td>
      <td>397.133298</td>
    </tr>
    <tr>
      <th>9</th>
      <td>surf</td>
      <td>2018-10</td>
      <td>414.435733</td>
    </tr>
    <tr>
      <th>10</th>
      <td>surf</td>
      <td>2018-11</td>
      <td>408.255415</td>
    </tr>
    <tr>
      <th>11</th>
      <td>surf</td>
      <td>2018-12</td>
      <td>457.547074</td>
    </tr>
    <tr>
      <th>12</th>
      <td>ultimate</td>
      <td>2018-01</td>
      <td>183.162500</td>
    </tr>
    <tr>
      <th>13</th>
      <td>ultimate</td>
      <td>2018-02</td>
      <td>443.171667</td>
    </tr>
    <tr>
      <th>14</th>
      <td>ultimate</td>
      <td>2018-03</td>
      <td>285.701667</td>
    </tr>
    <tr>
      <th>15</th>
      <td>ultimate</td>
      <td>2018-04</td>
      <td>316.508095</td>
    </tr>
    <tr>
      <th>16</th>
      <td>ultimate</td>
      <td>2018-05</td>
      <td>383.664828</td>
    </tr>
    <tr>
      <th>17</th>
      <td>ultimate</td>
      <td>2018-06</td>
      <td>365.358222</td>
    </tr>
    <tr>
      <th>18</th>
      <td>ultimate</td>
      <td>2018-07</td>
      <td>403.767288</td>
    </tr>
    <tr>
      <th>19</th>
      <td>ultimate</td>
      <td>2018-08</td>
      <td>397.274789</td>
    </tr>
    <tr>
      <th>20</th>
      <td>ultimate</td>
      <td>2018-09</td>
      <td>413.287326</td>
    </tr>
    <tr>
      <th>21</th>
      <td>ultimate</td>
      <td>2018-10</td>
      <td>429.217238</td>
    </tr>
    <tr>
      <th>22</th>
      <td>ultimate</td>
      <td>2018-11</td>
      <td>423.814683</td>
    </tr>
    <tr>
      <th>23</th>
      <td>ultimate</td>
      <td>2018-12</td>
      <td>438.824832</td>
    </tr>
  </tbody>
</table>
</div>




```python
surf_data = merged_data_with_tariff[merged_data_with_tariff['plan_name'] == 'surf']
ultimate_data = merged_data_with_tariff[merged_data_with_tariff['plan_name'] == 'ultimate']


plt.figure(figsize=(12, 6))
sns.histplot(surf_data['minutes_used'], kde=True, label='Surf', color='blue', alpha=0.5)
sns.histplot(ultimate_data['minutes_used'], kde=True, label='Ultimate', color='orange', alpha=0.5)

plt.title('Distribución de Duración de Llamadas por Plan y Mes')
plt.xlabel('Duración de Llamadas (minutos)')
plt.ylabel('Frecuencia')
plt.legend()
plt.show()# Compara el número de minutos mensuales que necesitan los usuarios de cada plan. Traza un histograma.


```


    
![png](output_97_0.png)
    


[Calcula la media y la variable de la duración de las llamadas para averiguar si los usuarios de los distintos planes se comportan de forma diferente al realizar sus llamadas.]


```python
mean_duration_by_plan = merged_data_with_tariff.groupby('plan_name')['minutes_used'].mean()
variance_duration_by_plan = merged_data_with_tariff.groupby('plan_name')['minutes_used'].var()

print("Media de la duración mensual de las llamadas por plan:")
print(mean_duration_by_plan)
print("\nVarianza de la duración mensual de las llamadas por plan:")
print(variance_duration_by_plan)# Calcula la media y la varianza de la duración mensual de llamadas.


```

    Media de la duración mensual de las llamadas por plan:
    plan_name
    surf        412.097890
    ultimate    410.180954
    Name: minutes_used, dtype: float64
    
    Varianza de la duración mensual de las llamadas por plan:
    plan_name
    surf        47001.254231
    ultimate    50510.631705
    Name: minutes_used, dtype: float64



```python
plt.figure(figsize=(8, 6))

sns.boxplot(x='plan_name', y='minutes_used', data=merged_data_with_tariff)


plt.title('Distribución de la Duración Mensual de Llamadas por Plan')
plt.xlabel('Plan')
plt.ylabel('Duración de las llamadas (minutos)')

plt.show()

call_duration_stats = merged_data_with_tariff.groupby('plan_name')['minutes_used'].describe()
call_duration_stats# Traza un diagrama de caja para visualizar la distribución de la duración mensual de llamadas


```


    
![png](output_100_0.png)
    





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
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>plan_name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>surf</th>
      <td>1545.0</td>
      <td>412.097890</td>
      <td>216.797727</td>
      <td>0.0</td>
      <td>262.78</td>
      <td>405.71</td>
      <td>546.23</td>
      <td>1431.22</td>
    </tr>
    <tr>
      <th>ultimate</th>
      <td>713.0</td>
      <td>410.180954</td>
      <td>224.745705</td>
      <td>0.0</td>
      <td>247.97</td>
      <td>399.98</td>
      <td>534.82</td>
      <td>1292.09</td>
    </tr>
  </tbody>
</table>
</div>



Plan Surf:

La duración media de las llamadas mensuales es de aproximadamente 412 minutos, con una desviación estándar de alrededor de 217 minutos.
El rango de duración de las llamadas va desde 0 minutos hasta 1431 minutos, con la mayoría de las llamadas (el 75%) con una duración inferior a 546 minutos.
Plan Ultimate:

La duración media de las llamadas mensuales es de aproximadamente 410 minutos, con una desviación estándar de alrededor de 225 minutos.
El rango de duración de las llamadas va desde 0 minutos hasta 1292 minutos, con la mayoría de las llamadas (el 75%) con una duración inferior a 535 minutos.

### Mensajes


```python
messages_per_plan_month = merged_data_with_tariff.groupby(['month', 'plan_name'])['messages_count'].sum().reset_index()


plt.figure(figsize=(12, 6))
sns.barplot(x='month', y='messages_count', hue='plan_name', data=messages_per_plan_month)
plt.title('Número de Mensajes por Plan y Mes')
plt.xlabel('Mes')
plt.ylabel('Número de Mensajes')
plt.xticks(rotation=45)
plt.show()# Comprara el número de mensajes que tienden a enviar cada mes los usuarios de cada plan

messages_per_plan_month
```


    
![png](output_103_0.png)
    





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
      <th>month</th>
      <th>plan_name</th>
      <th>messages_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-01</td>
      <td>surf</td>
      <td>21.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-01</td>
      <td>ultimate</td>
      <td>62.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-02</td>
      <td>surf</td>
      <td>108.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-02</td>
      <td>ultimate</td>
      <td>151.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018-03</td>
      <td>surf</td>
      <td>351.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2018-03</td>
      <td>ultimate</td>
      <td>243.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2018-04</td>
      <td>surf</td>
      <td>870.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2018-04</td>
      <td>ultimate</td>
      <td>463.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018-05</td>
      <td>surf</td>
      <td>1849.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2018-05</td>
      <td>ultimate</td>
      <td>931.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2018-06</td>
      <td>surf</td>
      <td>2454.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2018-06</td>
      <td>ultimate</td>
      <td>1379.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2018-07</td>
      <td>surf</td>
      <td>3271.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2018-07</td>
      <td>ultimate</td>
      <td>1937.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2018-08</td>
      <td>surf</td>
      <td>4662.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2018-08</td>
      <td>ultimate</td>
      <td>2732.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2018-09</td>
      <td>surf</td>
      <td>5968.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2018-09</td>
      <td>ultimate</td>
      <td>3259.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2018-10</td>
      <td>surf</td>
      <td>8020.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2018-10</td>
      <td>ultimate</td>
      <td>4181.0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2018-11</td>
      <td>surf</td>
      <td>9165.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2018-11</td>
      <td>ultimate</td>
      <td>4903.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2018-12</td>
      <td>surf</td>
      <td>12275.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2018-12</td>
      <td>ultimate</td>
      <td>6796.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
internet_per_plan_month = merged_data_with_tariff.groupby(['month', 'plan_name'])['mb_used'].sum().reset_index()

plt.figure(figsize=(12, 6))
sns.barplot(x='month', y='mb_used', hue='plan_name', data=internet_per_plan_month)
plt.title('Tráfico de Internet por Plan y Mes')
plt.xlabel('Mes')
plt.ylabel('Tráfico de Internet (MB)')
plt.xticks(rotation=45)
plt.show()# Compara la cantidad de tráfico de Internet consumido por usuarios por plan

internet_per_plan_month
```


    
![png](output_104_0.png)
    





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
      <th>month</th>
      <th>plan_name</th>
      <th>mb_used</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-01</td>
      <td>surf</td>
      <td>9749.72</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-01</td>
      <td>ultimate</td>
      <td>27672.37</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-02</td>
      <td>surf</td>
      <td>109609.59</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-02</td>
      <td>ultimate</td>
      <td>119901.66</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018-03</td>
      <td>surf</td>
      <td>306945.12</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2018-03</td>
      <td>ultimate</td>
      <td>219858.22</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2018-04</td>
      <td>surf</td>
      <td>599210.15</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2018-04</td>
      <td>ultimate</td>
      <td>338554.75</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2018-05</td>
      <td>surf</td>
      <td>1073099.33</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2018-05</td>
      <td>ultimate</td>
      <td>482109.99</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2018-06</td>
      <td>surf</td>
      <td>1484248.33</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2018-06</td>
      <td>ultimate</td>
      <td>720882.29</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2018-07</td>
      <td>surf</td>
      <td>2030815.67</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2018-07</td>
      <td>ultimate</td>
      <td>964339.92</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2018-08</td>
      <td>surf</td>
      <td>2720843.68</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2018-08</td>
      <td>ultimate</td>
      <td>1264845.13</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2018-09</td>
      <td>surf</td>
      <td>3218737.67</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2018-09</td>
      <td>ultimate</td>
      <td>1459408.78</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2018-10</td>
      <td>surf</td>
      <td>4102786.41</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2018-10</td>
      <td>ultimate</td>
      <td>1866930.66</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2018-11</td>
      <td>surf</td>
      <td>4624009.00</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2018-11</td>
      <td>ultimate</td>
      <td>2163278.04</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2018-12</td>
      <td>surf</td>
      <td>5766125.26</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2018-12</td>
      <td>ultimate</td>
      <td>2766801.97</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

 los usuarios del plan Ultimate tienden a enviar más mensajes y consumir más tráfico de Internet en comparación con los usuarios del plan Surf.

### Internet


```python
plt.figure(figsize=(12, 6))
sns.barplot(x='month', y='mb_used', hue='plan_name', data=merged_data_with_tariff)
plt.title('Tráfico de Internet por Mes y Plan')
plt.xlabel('Mes')
plt.ylabel('Tráfico de Internet (MB)')
plt.xticks(rotation=45)
plt.show()
```


    
![png](output_108_0.png)
    



```python
plt.figure(figsize=(12, 6))
for plan in ['surf', 'ultimate']:
    plan_data = merged_data_with_tariff[merged_data_with_tariff['plan_name'] == plan]
    sns.histplot(plan_data['mb_used'], kde=True, label=plan.capitalize(), bins=30, alpha=0.5)

plt.title('Distribución del Tráfico de Internet por Plan')
plt.xlabel('Tráfico de Internet (MB)')
plt.ylabel('Densidad')
plt.legend()
plt.show()
```


    
![png](output_109_0.png)
    



```python
internet_stats = merged_data_with_tariff.groupby('plan_name')['mb_used'].describe()
internet_stats

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
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
    <tr>
      <th>plan_name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>surf</th>
      <td>1558.0</td>
      <td>16717.702137</td>
      <td>7884.682983</td>
      <td>92.31</td>
      <td>12187.955</td>
      <td>16923.83</td>
      <td>21039.860</td>
      <td>70931.59</td>
    </tr>
    <tr>
      <th>ultimate</th>
      <td>719.0</td>
      <td>17238.642253</td>
      <td>7831.018323</td>
      <td>233.17</td>
      <td>12671.130</td>
      <td>16863.45</td>
      <td>21025.155</td>
      <td>46595.33</td>
    </tr>
  </tbody>
</table>
</div>



Ambos planes muestran una media similar de tráfico de Internet, con el Plan Ultimate ligeramente por encima del Plan Surf.

El Plan Surf tiene un mínimo de tráfico de Internet más bajo, pero también un máximo más alto en comparación con el Plan Ultimate.
La distribución del tráfico de Internet parece ser más variada en el Plan Surf

<div class="alert alert-block alert-success">
<b>Comentario revisor</b> <a class="tocSkip"></a>

 Muy buena prática la de usar distintos tipos de gráficas identificar algunos hallazgos y llegar a conclusiones
</div>

## Ingreso

[Del mismo modo que has estudiado el comportamiento de los usuarios, describe estadísticamente los ingresos de los planes.]


```python
users_per_plan = users['plan'].value_counts().reset_index()
users_per_plan.columns = ['plan_name', 'number_of_users']
merged_data = pd.merge(plans, users_per_plan, on='plan_name')

merged_data['total_monthly_revenue'] = merged_data['usd_monthly_pay'] * merged_data['number_of_users']

merged_data[['plan_name', 'total_monthly_revenue']]

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
      <th>plan_name</th>
      <th>total_monthly_revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>surf</td>
      <td>6780.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ultimate</td>
      <td>11270.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize=(10, 6))
plt.bar(merged_data['plan_name'], merged_data['number_of_users'], color=['blue', 'orange'])
plt.title('Cantidad de Usuarios por Plan')
plt.xlabel('Plan')
plt.ylabel('Número de Usuarios')
plt.show()
```


    
![png](output_116_0.png)
    



```python
plt.figure(figsize=(10, 6))
plt.bar(merged_data['plan_name'], merged_data['total_monthly_revenue'], color=['blue', 'orange'])
plt.title('Ingresos Mensuales Totales por Plan')
plt.xlabel('Plan')
plt.ylabel('Ingresos Mensuales Totales ($)')
plt.show()
```


    
![png](output_117_0.png)
    


hay mas usuarios de surf pero genera mas ingresos ultimate. monthly_revenue no tenia informacion correcta asi que tuve que sacar los ingresos en base a la cantidad de usuarios por el costo de cada plan


```python
from scipy.stats import ttest_ind

# Rellena los valores nulos en la columna 'total_monthly_revenue' con cero
#merged_data['total_monthly_revenue'].fillna(0, inplace=True)

# Filtra los ingresos mensuales totales por plan y elimina los valores nulos
surf_revenue = merged_data_with_tariff[merged_data_with_tariff['plan_name'] == 'surf']['monthly_revenue'].dropna()
ultimate_revenue = merged_data_with_tariff[merged_data_with_tariff['plan_name'] == 'ultimate']['monthly_revenue'].dropna()

# Prueba t de muestras independientes
t_stat, p_val = ttest_ind(surf_revenue, ultimate_revenue, equal_var=True)  # Usar equal_var=True

# Nivel de significancia (alfa)
alfa = 0.05  # Supongamos un valor alfa de 0.05

# Imprimir resultados
print("Estadística t:", t_stat)
print("Valor p:", p_val)

# Comprobar si el valor p es menor que alfa para decidir si rechazar H0
if p_val < alfa:
    print("Rechazamos la hipótesis nula. Hay evidencia suficiente para concluir que hay una diferencia en los ingresos mensuales totales entre los planes Ultimate y Surf.")
else:
    print("No rechazamos la hipótesis nula. No hay suficiente evidencia para concluir que hay una diferencia en los ingresos mensuales totales entre los planes Ultimate y Surf.")
```

    Estadística t: -7.861521605872225
    Valor p: 6.56601124721972e-15
    Rechazamos la hipótesis nula. Hay evidencia suficiente para concluir que hay una diferencia en los ingresos mensuales totales entre los planes Ultimate y Surf.



```python
merged_data_with_city = pd.merge(merged_data_with_tariff, users[['user_id', 'city']], on='user_id', how='left')

merged_data_with_city.head()
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
      <th>user_id</th>
      <th>month</th>
      <th>calls_count</th>
      <th>minutes_used</th>
      <th>messages_count</th>
      <th>mb_used</th>
      <th>plan</th>
      <th>messages_included</th>
      <th>mb_per_month_included</th>
      <th>minutes_included</th>
      <th>...</th>
      <th>usd_per_minute</th>
      <th>plan_name</th>
      <th>extra_calls</th>
      <th>extra_messages</th>
      <th>extra_mb</th>
      <th>call_revenue</th>
      <th>message_revenue</th>
      <th>data_revenue</th>
      <th>monthly_revenue</th>
      <th>city</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1000</td>
      <td>2018-12</td>
      <td>16.0</td>
      <td>116.83</td>
      <td>11.0</td>
      <td>1901.47</td>
      <td>ultimate</td>
      <td>1000</td>
      <td>30720</td>
      <td>3000</td>
      <td>...</td>
      <td>0.01</td>
      <td>ultimate</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>70.000000</td>
      <td>Atlanta-Sandy Springs-Roswell, GA MSA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1001</td>
      <td>2018-08</td>
      <td>27.0</td>
      <td>171.14</td>
      <td>30.0</td>
      <td>6919.15</td>
      <td>surf</td>
      <td>50</td>
      <td>15360</td>
      <td>500</td>
      <td>...</td>
      <td>0.03</td>
      <td>surf</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>20.000000</td>
      <td>Seattle-Tacoma-Bellevue, WA MSA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1001</td>
      <td>2018-09</td>
      <td>49.0</td>
      <td>297.69</td>
      <td>44.0</td>
      <td>13314.82</td>
      <td>surf</td>
      <td>50</td>
      <td>15360</td>
      <td>500</td>
      <td>...</td>
      <td>0.03</td>
      <td>surf</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>20.000000</td>
      <td>Seattle-Tacoma-Bellevue, WA MSA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1001</td>
      <td>2018-10</td>
      <td>65.0</td>
      <td>374.11</td>
      <td>53.0</td>
      <td>22330.49</td>
      <td>surf</td>
      <td>50</td>
      <td>15360</td>
      <td>500</td>
      <td>...</td>
      <td>0.03</td>
      <td>surf</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>6970.49</td>
      <td>0.0</td>
      <td>0.09</td>
      <td>68.071191</td>
      <td>88.161191</td>
      <td>Seattle-Tacoma-Bellevue, WA MSA</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1001</td>
      <td>2018-11</td>
      <td>64.0</td>
      <td>404.59</td>
      <td>36.0</td>
      <td>18504.30</td>
      <td>surf</td>
      <td>50</td>
      <td>15360</td>
      <td>500</td>
      <td>...</td>
      <td>0.03</td>
      <td>surf</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3144.30</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>30.706055</td>
      <td>50.706055</td>
      <td>Seattle-Tacoma-Bellevue, WA MSA</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 23 columns</p>
</div>



[Prueba la hipótesis de que el ingreso promedio de los usuarios del área NY-NJ es diferente al de los usuarios de otras regiones.]

[Elabora las hipótesis nula y alternativa, escoge la prueba estadística, determina el valor alfa.]


```python
from scipy.stats import ttest_ind

ny_nj_revenue = merged_data_with_city.loc[merged_data_with_city['city'].str.contains('NY-NJ'), 'monthly_revenue'].dropna()
other_revenue = merged_data_with_city.loc[~merged_data_with_city['city'].str.contains('NY-NJ'), 'monthly_revenue'].dropna()

t_stat, p_val = ttest_ind(ny_nj_revenue, other_revenue, equal_var=False)  # Usar equal_var=False si las varianzas no son iguales

alfa = 0.05

print("Estadística t:", t_stat)
print("Valor p:", p_val)

if p_val < alfa:
    print("Rechazamos la hipótesis nula. Hay evidencia suficiente para concluir que hay una diferencia en el ingreso promedio entre los usuarios del área NY-NJ y los usuarios de otras regiones.")
else:
    print("No rechazamos la hipótesis nula. No hay suficiente evidencia para concluir que hay una diferencia en el ingreso promedio entre los usuarios del área NY-NJ y los usuarios de otras regiones.")
```

    Estadística t: -3.3928948080613366
    Valor p: 0.0007376239785321068
    Rechazamos la hipótesis nula. Hay evidencia suficiente para concluir que hay una diferencia en el ingreso promedio entre los usuarios del área NY-NJ y los usuarios de otras regiones.


<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Hola, Isaac! Muy buen trabajo ya casi tienes el ejercicio, solamente verifica que en las pruebas de hipótesis cuents con las variables 'plan_name' y 'monthly_revenue' dentro de la base de datos que utilizas. 

## Conclusión general

El análisis de datos nos permitió comprender mejor el comportamiento de los usuarios en términos de llamadas, mensajes y uso de datos. Esto incluyó la identificación de tendencias, patrones estacionales y la distribución de los datos.

Limpieza de Datos: Durante la limpieza de datos, se eliminaron valores nulos, se corrigieron tipos de datos incorrectos y se manejaron valores atípicos. Esto aseguró que los datos estuvieran listos para su análisis posterior.

Enriquecimiento de Datos: Se enriquecieron los datos calculando métricas adicionales como la duración promedio de las llamadas, la cantidad promedio de mensajes por usuario y el volumen promedio de datos consumidos por usuario. Esto proporcionó una comprensión más profunda del comportamiento de los usuarios.

Análisis de Ingresos: Se calcularon los ingresos mensuales por usuario, teniendo en cuenta los límites del paquete gratuito y los cargos adicionales por exceder esos límites. Esto permitió una evaluación de la rentabilidad de cada usuario y del plan de tarifas en general.

Pruebas Estadísticas: Se llevaron a cabo pruebas estadísticas para analizar la diferencia en los ingresos promedio entre diferentes grupos de usuarios, así como para evaluar la diferencia en los ingresos promedio entre usuarios de diferentes regiones.

En resumen, el proyecto proporcionó información valiosa sobre el comportamiento de los usuarios y la rentabilidad de los diferentes planes de tarifas. Esto puede ser utilizado por la empresa para tomar decisiones informadas sobre estrategias de marketing, ajustes de precios y mejoras en los servicios ofrecidos.

<div class="alert alert-block alert-warning">
<b>Comentario revisor</b> <a class="tocSkip"></a>

En general creo que hiciste un muy buen trabajo con el proyecto, pudiste limpiar y trabajar las bases de datos de beuna manera, así como juntar la información. Además, considero que el análisis con las gráficas y con las pruebas de hipótesis es muy acertado. No obstante, recuerda que siempre podemos mejorar y te menciono algunos puntos que debes considerar:

* Realizar un análisis inicial de registros duplicados en todas las bases de datos
    
    
*  verificar que redondeamos las variables antes de hacer la agrupación por usuario
    
*  verificar que hacemos la transformación de megabytes a gigabytes
    
*  Verificar el calculo de excesos en llamadas, mensajes e internet
    
*  Profundizar en conclusiones intermedias y finales.
</div>
