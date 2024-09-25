# Hola Isaac!

Mi nombre es David Bautista, soy code reviewer de TripleTen y voy a revisar el proyecto que acabas de desarrollar.

Cuando vea un error la primera vez, lo señalaré. Deberás encontrarlo y arreglarlo. La intención es que te prepares para un espacio real de trabajo. En un trabajo, el líder de tu equipo hará lo mismo. Si no puedes solucionar el error, te daré más información en la próxima ocasión.

Encontrarás mis comentarios más abajo - **por favor, no los muevas, no los modifiques ni los borres.**

¿Cómo lo voy a hacer? Voy a leer detenidamente cada una de las implementaciones que has llevado a cabo para cumplir con lo solicitado. Verás los comentarios de esta forma:


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Si todo está perfecto.
</div>


<div class="alert alert-block alert-warning">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Si tu código está bien pero se puede mejorar o hay algún detalle que le hace falta.
</div>


<div class="alert alert-block alert-danger">
    
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
    
Si de pronto hace falta algo o existe algún problema con tu código o conclusiones.
</div>


Puedes responderme de esta forma: 

<div class="alert alert-block alert-info">
<b>Respuesta del estudiante</b> <a class="tocSkip"></a>
</div

¡Empecemos!

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
# Comentario General

~~Hola, Isaac, te felicito por el desarrollo del proyecto hasta el momento. Ahora bien, he dejado diferentes comentarios para que los pedas tener en cuenta para la siguiente entrega.~~ </div>

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
# Comentario General #2

Hola, Isaac, te felicito por la culminación del proyecto. Muy buen trabajo. </div>

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
~~Isaac, ten en cuenta que es importante generar una sección de introducción del proyecto. En nuestra profesión como científicos de datos debemos tener la capacidad de introducir los objetivos y finalidades de un proyecto.~~ 
</div>

# Análisis de Viajes en Taxi en Chicago

## Introducción

### Contexto del Proyecto

Este proyecto se centra en el análisis de los datos de viajes en taxi en Chicago, con el objetivo de comprender las preferencias de los pasajeros y el impacto de los factores externos, como el clima, en los viajes. La empresa ficticia "Zuber", una nueva plataforma de viajes compartidos, está interesada en explorar estos datos para mejorar sus servicios y estrategias de mercado.

### Objetivos

Los objetivos principales de este proyecto son:

1. **Analizar los datos de los viajes en taxi:** Identificar patrones y tendencias en los datos de los viajes en taxi en Chicago.
2. **Impacto del clima en los viajes:** Evaluar cómo las condiciones climáticas afectan la frecuencia y duración de los viajes.
3. **Comparar la actividad de diferentes compañías de taxis:** Determinar cuáles son las compañías de taxis más activas y cómo se distribuyen los viajes entre ellas.
4. **Identificar barrios con mayor y menor actividad de taxis:** Analizar en qué barrios terminan la mayoría de los viajes y cuáles son menos frecuentados.

### Descripción de los Datos

Este proyecto utiliza varios conjuntos de datos que proporcionan información detallada sobre los viajes en taxi y las condiciones climáticas en Chicago:

1. **DataFrame 01:**
   - **company_name:** Nombre de la empresa de taxis.
   - **trips_amount:** Número de viajes de cada compañía de taxis el 15 y 16 de noviembre de 2017.

2. **DataFrame 04:**
   - **dropoff_location_name:** Barrios de Chicago donde finalizaron los viajes.
   - **average_trips:** Promedio de viajes que terminaron en cada barrio en noviembre de 2017.

3. **DataFrame 07:**
   - **start_ts:** Fecha y hora de la recogida.
   - **weather_conditions:** Condiciones climáticas en el momento en el que comenzó el viaje.
   - **duration_seconds:** Duración del viaje en segundos.

### Metodología

Para alcanzar los objetivos mencionados, se llevarán a cabo las siguientes acciones:

1. **Análisis Exploratorio de Datos (EDA):** Examinar los datos para obtener una comprensión inicial de las tendencias y patrones.
2. **Limpieza y Preparación de Datos:** Asegurarse de que los datos estén limpios y listos para el análisis.
3. **Análisis Estadístico:** Aplicar pruebas estadísticas para evaluar el impacto de las condiciones climáticas en la duración de los viajes.
4. **Visualización de Datos:** Crear gráficos y visualizaciones para presentar los hallazgos de manera clara y concisa.

### Resultados Esperados

Se espera que este proyecto proporcione información valiosa sobre las preferencias de los pasajeros de taxis en Chicago, así como el impacto de las condiciones climáticas en la frecuencia y duración de los viajes. Además, se anticipa identificar las compañías de taxis más activas y los barrios con mayor y menor actividad de taxis, lo que puede ayudar a "Zuber" a optimizar sus operaciones y estrategias de mercado.


<div class="alert alert-block alert-success">
<b>Comentario del revisor #2</b> <a class="tocSkip"></a>
    
Perfecto, buen trabajo estructurando la sección de introducción del proyecto. </div>


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy.stats import ttest_ind
```

<div class="alert alert-block alert-success">
<b>Comentario del revisor #2</b> <a class="tocSkip"></a>
    
Buen trabajo importando las librerias necesarias para el desarrollo del proyecto. </div>


```python
df_01 = pd.read_csv("/datasets/project_sql_result_01.csv")
df_04 = pd.read_csv("/datasets/project_sql_result_04.csv")

print("DataFrame 01:")
print(df_01.head())

print("\nDataFrame 04:")
print(df_04.head())

```

    DataFrame 01:
                          company_name  trips_amount
    0                        Flash Cab         19558
    1        Taxi Affiliation Services         11422
    2                Medallion Leasing         10367
    3                       Yellow Cab          9888
    4  Taxi Affiliation Service Yellow          9299
    
    DataFrame 04:
      dropoff_location_name  average_trips
    0                  Loop   10727.466667
    1           River North    9523.666667
    2         Streeterville    6664.666667
    3             West Loop    5163.666667
    4                O'Hare    2546.900000


<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
~~Isaac, te recomiendo separar las secciones de importe de las librerías y de carga de los datos. Por otro lado, ten en cuenta que el ideal es importar todas las librerías que vas a usar en el proyecto desde esta sección.~~ </div>

# Descripción de los DataFrames

## DataFrame 01

**Columnas:**

- **company_name:** Nombre de la empresa de taxis.
- **trips_amount:** Número de viajes de cada compañía de taxis el 15 y 16 de noviembre de 2017.

**Descripción:**

Este DataFrame proporciona información sobre la cantidad de viajes realizados por cada empresa de taxis durante el período especificado.

## DataFrame 04

**Columnas:**

- **dropoff_location_name:** Barrios de Chicago donde finalizaron los viajes.
- **average_trips:** Promedio de viajes que terminaron en cada barrio en noviembre de 2017.

**Descripción:**

Este DataFrame presenta el promedio de viajes que finalizaron en cada barrio de Chicago durante el mes de noviembre de 2017.


<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
~~Isaac, ten en cuenta que podrías llevar estas observaciones a una celda con formato ``Markdowm``, lo anterior permitirá que el proyecto tenga una mejor presentación.~~  </div>


```python

print("Información sobre el DataFrame 01:")
print(df_01.info())

print("\nInformación sobre el DataFrame 04:")
print(df_04.info())

```

    Información sobre el DataFrame 01:
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 64 entries, 0 to 63
    Data columns (total 2 columns):
     #   Column        Non-Null Count  Dtype 
    ---  ------        --------------  ----- 
     0   company_name  64 non-null     object
     1   trips_amount  64 non-null     int64 
    dtypes: int64(1), object(1)
    memory usage: 1.1+ KB
    None
    
    Información sobre el DataFrame 04:
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 94 entries, 0 to 93
    Data columns (total 2 columns):
     #   Column                 Non-Null Count  Dtype  
    ---  ------                 --------------  -----  
     0   dropoff_location_name  94 non-null     object 
     1   average_trips          94 non-null     float64
    dtypes: float64(1), object(1)
    memory usage: 1.6+ KB
    None


#No parece haber ningún problema con los tipos de datos en estos DataFrames.

<div class="alert alert-block alert-success">
<b>Comentario del revisor </b> <a class="tocSkip"></a>
    
Buen trabajo con la revisión inicial de la tabla.  </div>


```python
top_10_dropoff_locations = df_04.sort_values(by='average_trips', ascending=False).head(10)
print(top_10_dropoff_locations)

```

      dropoff_location_name  average_trips
    0                  Loop   10727.466667
    1           River North    9523.666667
    2         Streeterville    6664.666667
    3             West Loop    5163.666667
    4                O'Hare    2546.900000
    5             Lake View    2420.966667
    6            Grant Park    2068.533333
    7         Museum Campus    1510.000000
    8            Gold Coast    1364.233333
    9    Sheffield & DePaul    1259.766667


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Buen trabajo estructurando la tabla.   </div>


```python
import matplotlib.pyplot as plt

# Seleccionar las 10 empresas con el mayor número de viajes
top_10_companies = df_01.nlargest(20, 'trips_amount')

plt.figure(figsize=(10, 6))
plt.bar(top_10_companies['company_name'], top_10_companies['trips_amount'], color='skyblue')
plt.xlabel('Empresa de Taxis')
plt.ylabel('Número de Viajes')
plt.title('Número de Viajes por Empresa de Taxis (Top 10)')
plt.xticks(rotation=45, ha='right')  
plt.tight_layout()

plt.show()

```


    
![png](output_16_0.png)
    


<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
~~Buen trabajo, construyendo la gráfica, sin embargo, te recomiendo limitar el número de las observaciones que estás mostrando, lo anterior buscando obtener un gráfico más estético.~~   </div>

<div class="alert alert-block alert-success">
<b>Comentario del revisor #2</b> <a class="tocSkip"></a>
    
Perfecto, buen trabajo con las modificaciones. </div>


```python
df_01['trips_amount'].describe()

```




    count       64.000000
    mean      2145.484375
    std       3812.310186
    min          2.000000
    25%         20.750000
    50%        178.500000
    75%       2106.500000
    max      19558.000000
    Name: trips_amount, dtype: float64




```python
max_trips_company = df_01[df_01['trips_amount'] == df_01['trips_amount'].max()]['company_name'].iloc[0]
print("Empresa con el mayor número de viajes:", max_trips_company)

```

    Empresa con el mayor número de viajes: Flash Cab



```python
min_trips_company = df_01[df_01['trips_amount'] == df_01['trips_amount'].min()]['company_name'].iloc[0]
print("Empresa con el menor número de viajes:", min_trips_company)

```

    Empresa con el menor número de viajes: 3556 - 36214 RC Andrews Cab


# Análisis del Número de Viajes por Empresa de Taxis

En base a las estadísticas del número de viajes por empresa de taxis, podemos observar lo siguiente:

## Estadísticas Generales

- **Promedio de viajes por empresa de taxis:** Aproximadamente 2145 viajes.

## Empresa con Mayor Número de Viajes

- **Empresa:** Flash Cab
- **Número de viajes:** 19558 viajes registrados durante el período analizado.

## Empresa con Menor Número de Viajes

- **Empresa:** 3556 - 36214 RC Andrews Cab
- **Número de viajes:** 2 viajes registrados durante el período analizado.

## Conclusiones Intermedias

1. **Distribución de viajes:** Existe una gran disparidad en el número de viajes entre las diferentes empresas de taxis, con algunas empresas registrando un número muy alto de viajes y otras un número muy bajo.
2. **Flash Cab:** Dominante en el mercado con la mayor cantidad de viajes.
3. **Empresas pequeñas:** Algunas empresas, como 3556 - 36214 RC Andrews Cab, tienen muy poca actividad, lo que podría indicar la necesidad de analizar su operación o su participación en el mercado.

Estos análisis proporcionan una visión inicial sobre la distribución y la actividad de las empresas de taxis en el período analizado.


<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
~~Buen trabajo desarrollando este análisis adicional, solo te recomiendo organizar más la sección por medio del uso de  celda Markdown con conclusiones intermedias y subtítulos.~~   </div>

<div class="alert alert-block alert-success">
<b>Comentario del revisor #2</b> <a class="tocSkip"></a>
    
Buen trabajo Isaac.   </div>


```python

top_10_dropoff_locations = df_04.sort_values(by='average_trips', ascending=False).head(10)

plt.figure(figsize=(10, 6))
plt.bar(top_10_dropoff_locations['dropoff_location_name'], top_10_dropoff_locations['average_trips'], color='lightgreen')
plt.xlabel('Barrio')
plt.ylabel('Número Promedio de Viajes')
plt.title('Top 10 Barrios por Número de Finalizaciones de Viajes')
plt.xticks(rotation=45, ha='right')  # Rotar las etiquetas del eje x para una mejor legibilidad
plt.tight_layout()

plt.show()

```


    
![png](output_24_0.png)
    


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Perfecto, buen trabajo con el despliegue del gráfico.    </div>


```python
df_04['average_trips'].describe()

```




    count       94.000000
    mean       599.953728
    std       1714.591098
    min          1.800000
    25%         14.266667
    50%         52.016667
    75%        298.858333
    max      10727.466667
    Name: average_trips, dtype: float64




```python
max_avg_trips_location = df_04[df_04['average_trips'] == df_04['average_trips'].max()]['dropoff_location_name'].iloc[0]
print("Barrio con el mayor número promedio de viajes:", max_avg_trips_location)

```

    Barrio con el mayor número promedio de viajes: Loop



```python
min_avg_trips_location = df_04[df_04['average_trips'] == df_04['average_trips'].min()]['dropoff_location_name'].iloc[0]
print("Barrio con el menor número promedio de viajes:", min_avg_trips_location)

```

    Barrio con el menor número promedio de viajes: Riverdale


# Análisis del Número de Viajes por Barrio

En base a las estadísticas del número de viajes por barrio, podemos observar lo siguiente:

## Estadísticas Generales

- **Número total de barrios analizados:** 94
- **Promedio de viajes por barrio:** 599.95 viajes

## Valores Extremos

- **Valor mínimo:** 1.8 viajes
- **Valor máximo:** 10727.47 viajes

## Barrios Destacados

- **Barrio con el mayor número promedio de viajes:** Loop
- **Barrio con el menor número promedio de viajes:** Riverdale

## Conclusiones Intermedias

1. **Distribución de viajes:** Existe una variabilidad considerable en el número de viajes entre los diferentes barrios, con algunos barrios registrando un número muy alto de viajes y otros un número muy bajo.
2. **Loop:** Destacado como el barrio con el mayor número promedio de viajes, lo que puede indicar su importancia como un destino principal para los taxis.
3. **Riverdale:** Identificado como el barrio con el menor número promedio de viajes, lo que podría indicar una menor demanda de servicios de taxi en esa área.

Estos análisis proporcionan una visión inicial sobre la distribución y la actividad de los viajes de taxi en diferentes barrios durante el período analizado.


<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
~~Buen trabajo desarrollando este análisis adicional, solo te recomiendo organizar más la sección por medio del uso de  celda Markdown con conclusiones intermedias y subtítulos.~~   </div>

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
**Comentario Importante**

~~Hola, Isaac, para el desarrollo de esta última sección de prueba de hipótesis te recomiendo mejorar el orden por medio de observaciones y subtítulos, por otro lado, ten en cuenta que es importante estudiar el comportamiento de las distribuciones de los dos grupos.~~ </div>


```python
df_07 = pd.read_csv("/datasets/project_sql_result_07.csv")

print("DataFrame 07:")
print(df_07.head())

```

    DataFrame 07:
                  start_ts weather_conditions  duration_seconds
    0  2017-11-25 16:00:00               Good            2410.0
    1  2017-11-25 14:00:00               Good            1920.0
    2  2017-11-25 12:00:00               Good            1543.0
    3  2017-11-04 10:00:00               Good            2512.0
    4  2017-11-11 07:00:00               Good            1440.0



```python
rainy_days = df_07[df_07['weather_conditions'] == 'Bad']
non_rainy_days = df_07[df_07['weather_conditions'] == 'Good']

print("Días lluviosos:")
print(rainy_days.head(10))
print("\nDías no lluviosos:")
print(non_rainy_days.head(10))
```

    Días lluviosos:
                   start_ts weather_conditions  duration_seconds
    6   2017-11-04 16:00:00                Bad            2969.0
    30  2017-11-18 12:00:00                Bad            1980.0
    34  2017-11-04 17:00:00                Bad            2460.0
    51  2017-11-04 16:00:00                Bad            2760.0
    52  2017-11-18 12:00:00                Bad            2460.0
    54  2017-11-18 10:00:00                Bad            1440.0
    65  2017-11-04 18:00:00                Bad            2363.0
    70  2017-11-18 16:00:00                Bad            3000.0
    78  2017-11-04 16:00:00                Bad            3120.0
    92  2017-11-18 07:00:00                Bad            1511.0
    
    Días no lluviosos:
                   start_ts weather_conditions  duration_seconds
    0   2017-11-25 16:00:00               Good            2410.0
    1   2017-11-25 14:00:00               Good            1920.0
    2   2017-11-25 12:00:00               Good            1543.0
    3   2017-11-04 10:00:00               Good            2512.0
    4   2017-11-11 07:00:00               Good            1440.0
    5   2017-11-11 04:00:00               Good            1320.0
    7   2017-11-18 11:00:00               Good            2280.0
    8   2017-11-11 14:00:00               Good            2460.0
    9   2017-11-11 12:00:00               Good            2040.0
    10  2017-11-18 06:00:00               Good            1500.0



```python
plt.figure(figsize=(14, 7))

sns.histplot(rainy_days['duration_seconds'], kde=True, color='blue', label='Días lluviosos')


sns.histplot(non_rainy_days['duration_seconds'], kde=True, color='green', label='Días no lluviosos')

plt.xlabel('Duración del viaje (segundos)')
plt.ylabel('Frecuencia')
plt.title('Distribución de la Duración de Viajes en Días Lluviosos y No Lluviosos')
plt.legend()
plt.show()
```


    
![png](output_34_0.png)
    



```python
# Calcular la duración promedio de los viajes en días lluviosos y no lluviosos
mean_duration_rainy = rainy_days['duration_seconds'].mean()
mean_duration_non_rainy = non_rainy_days['duration_seconds'].mean()

# Realizar la prueba t de Student para determinar si hay diferencia significativa
t_statistic, p_value = ttest_ind(rainy_days['duration_seconds'], non_rainy_days['duration_seconds'], nan_policy='omit')

# Mostrar los resultados
print("\nDuración promedio de los viajes en días lluviosos:", mean_duration_rainy)
print("Duración promedio de los viajes en días no lluviosos:", mean_duration_non_rainy)
print("Valor p de la prueba de hipótesis:", p_value)

# Decisión basada en el valor p y el nivel de significación alfa
alpha = 0.05
if p_value < alpha:
    print("Se rechaza la hipótesis nula: hay evidencia suficiente para afirmar que la duración promedio de los viajes difiere en días lluviosos en comparación con días no lluviosos.")
else:
    print("No se puede rechazar la hipótesis nula: no hay suficiente evidencia para afirmar que la duración promedio de los viajes difiere en días lluviosos en comparación con días no lluviosos.")

```

    
    Duración promedio de los viajes en días lluviosos: 2427.2055555555557
    Duración promedio de los viajes en días no lluviosos: 1999.6756756756756
    Valor p de la prueba de hipótesis: 6.517970327099473e-12
    Se rechaza la hipótesis nula: hay evidencia suficiente para afirmar que la duración promedio de los viajes difiere en días lluviosos en comparación con días no lluviosos.


<div class="alert alert-block alert-success">
<b>Comentario del revisor #2</b> <a class="tocSkip"></a>
    
Perfecto, Issac, buen trabajo con las modificaciones y el desarrollo de la sección de prueba de hipótesis.   </div>

## Conclusiones

### Resultados de la Prueba de Hipótesis

- **Duración promedio de los viajes en días lluviosos:** 2427.21 segundos
- **Duración promedio de los viajes en días no lluviosos:** 1999.68 segundos
- **Valor p de la prueba de hipótesis:** 6.517970327099473e-12

### Decisión

Se rechaza la hipótesis nula. Hay evidencia suficiente para afirmar que la duración promedio de los viajes difiere en días lluviosos en comparación con días no lluviosos.

### Observaciones

- La duración promedio de los viajes es mayor en días lluviosos (2427.21 segundos) en comparación con días no lluviosos (1999.68 segundos).
- El valor p (6.517970327099473e-12) es menor que el nivel alfa (0.05), lo que indica una diferencia entre las duraciones promedio de los viajes en días lluviosos y no lluviosos.
- Esta diferencia puede ser atribuida a factores como el tráfico más lento y las condiciones de conducción más difíciles en días lluviosos, lo que prolonga la duración de los viajes.

### Recomendaciones

- **Optimización de Rutas:** Las compañías de taxis podrían considerar optimizar las rutas durante los días lluviosos para minimizar el impacto de las condiciones climáticas adversas.
- **Información a los Clientes:** Informar a los pasajeros sobre posibles retrasos en días lluviosos puede ayudar a gestionar las expectativas y mejorar la satisfacción del cliente.
- **Análisis Adicional:** Se recomienda realizar un análisis adicional para identificar otros factores que pueden afectar la duración de los viajes, como la hora del día y el tráfico.

Estos hallazgos proporcionan una visión valiosa sobre cómo las condiciones climáticas pueden influir en la duración de los viajes en taxi, y pueden ser utilizados por las compañías de taxis para mejorar sus operaciones y servicios.


<div class="alert alert-block alert-success">
<b>Comentario del revisor #2</b> <a class="tocSkip"></a>
    
Buen trabajo con el desarrollo de la sección de conclusiones y recomendaciones.  </div>
