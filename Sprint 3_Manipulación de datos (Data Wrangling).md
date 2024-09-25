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

# ¡Llena ese carrito!

# Introducción

Instacart es una plataforma de entregas de comestibles donde la clientela puede registrar un pedido y hacer que se lo entreguen, similar a Uber Eats y Door Dash.
El conjunto de datos que te hemos proporcionado tiene modificaciones del original. Redujimos el tamaño del conjunto para que tus cálculos se hicieran más rápido e introdujimos valores ausentes y duplicados. Tuvimos cuidado de conservar las distribuciones de los datos originales cuando hicimos los cambios.

Debes completar tres pasos. Para cada uno de ellos, escribe una breve introducción que refleje con claridad cómo pretendes resolver cada paso, y escribe párrafos explicatorios que justifiquen tus decisiones al tiempo que avanzas en tu solución.  También escribe una conclusión que resuma tus hallazgos y elecciones.


## Diccionario de datos

Hay cinco tablas en el conjunto de datos, y tendrás que usarlas todas para hacer el preprocesamiento de datos y el análisis exploratorio de datos. A continuación se muestra un diccionario de datos que enumera las columnas de cada tabla y describe los datos que contienen.

- `instacart_orders.csv`: cada fila corresponde a un pedido en la aplicación Instacart.
    - `'order_id'`: número de ID que identifica de manera única cada pedido.
    - `'user_id'`: número de ID que identifica de manera única la cuenta de cada cliente.
    - `'order_number'`: el número de veces que este cliente ha hecho un pedido.
    - `'order_dow'`: día de la semana en que se hizo el pedido (0 si es domingo).
    - `'order_hour_of_day'`: hora del día en que se hizo el pedido.
    - `'days_since_prior_order'`: número de días transcurridos desde que este cliente hizo su pedido anterior.
- `products.csv`: cada fila corresponde a un producto único que pueden comprar los clientes.
    - `'product_id'`: número ID que identifica de manera única cada producto.
    - `'product_name'`: nombre del producto.
    - `'aisle_id'`: número ID que identifica de manera única cada categoría de pasillo de víveres.
    - `'department_id'`: número ID que identifica de manera única cada departamento de víveres.
- `order_products.csv`: cada fila corresponde a un artículo pedido en un pedido.
    - `'order_id'`: número de ID que identifica de manera única cada pedido.
    - `'product_id'`: número ID que identifica de manera única cada producto.
    - `'add_to_cart_order'`: el orden secuencial en el que se añadió cada artículo en el carrito.
    - `'reordered'`: 0 si el cliente nunca ha pedido este producto antes, 1 si lo ha pedido.
- `aisles.csv`
    - `'aisle_id'`: número ID que identifica de manera única cada categoría de pasillo de víveres.
    - `'aisle'`: nombre del pasillo.
- `departments.csv`
    - `'department_id'`: número ID que identifica de manera única cada departamento de víveres.
    - `'department'`: nombre del departamento.

# Paso 1. Descripción de los datos

Lee los archivos de datos (`/datasets/instacart_orders.csv`, `/datasets/products.csv`, `/datasets/aisles.csv`, `/datasets/departments.csv` y `/datasets/order_products.csv`) con `pd.read_csv()` usando los parámetros adecuados para leer los datos correctamente. Verifica la información para cada DataFrame creado.


## Plan de solución

Escribe aquí tu plan de solución para el Paso 1. Descripción de los datos.


```python
import pandas as pd
from matplotlib import pyplot as plt# importar librerías
```


```python
orders = pd.read_csv('/datasets/instacart_orders.csv', sep=";")
products = pd.read_csv('/datasets/products.csv', sep=";")
order_products = pd.read_csv('/datasets/order_products.csv', sep=";")
aisles = pd.read_csv('/datasets/aisles.csv', sep=";")
departments = pd.read_csv('/datasets/departments.csv', sep=";")# leer conjuntos de datos en los DataFrames
```


```python
print("Información de 'orders':")
print(orders.info())
print("\nPrimeras filas de 'orders':")
print(orders.head())
# mostrar información del DataFrame
```

    Información de 'orders':
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 478967 entries, 0 to 478966
    Data columns (total 6 columns):
     #   Column                  Non-Null Count   Dtype  
    ---  ------                  --------------   -----  
     0   order_id                478967 non-null  int64  
     1   user_id                 478967 non-null  int64  
     2   order_number            478967 non-null  int64  
     3   order_dow               478967 non-null  int64  
     4   order_hour_of_day       478967 non-null  int64  
     5   days_since_prior_order  450148 non-null  float64
    dtypes: float64(1), int64(5)
    memory usage: 21.9 MB
    None
    
    Primeras filas de 'orders':
       order_id  user_id  order_number  order_dow  order_hour_of_day  \
    0   1515936   183418            11          6                 13   
    1   1690866   163593             5          5                 12   
    2   1454967    39980             4          5                 19   
    3   1768857    82516            56          0                 20   
    4   3007858   196724             2          4                 12   
    
       days_since_prior_order  
    0                    30.0  
    1                     9.0  
    2                     2.0  
    3                    10.0  
    4                    17.0  



```python
print("\nInformación de 'products':")
print(products.info())

print("\nPrimeras filas de 'products':")
print(products.head())
# mostrar información del DataFrame
```

    
    Información de 'products':
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 49694 entries, 0 to 49693
    Data columns (total 4 columns):
     #   Column         Non-Null Count  Dtype 
    ---  ------         --------------  ----- 
     0   product_id     49694 non-null  int64 
     1   product_name   48436 non-null  object
     2   aisle_id       49694 non-null  int64 
     3   department_id  49694 non-null  int64 
    dtypes: int64(3), object(1)
    memory usage: 1.5+ MB
    None
    
    Primeras filas de 'products':
       product_id                                       product_name  aisle_id  \
    0           1                         Chocolate Sandwich Cookies        61   
    1           2                                   All-Seasons Salt       104   
    2           3               Robust Golden Unsweetened Oolong Tea        94   
    3           4  Smart Ones Classic Favorites Mini Rigatoni Wit...        38   
    4           5                          Green Chile Anytime Sauce         5   
    
       department_id  
    0             19  
    1             13  
    2              7  
    3              1  
    4             13  



```python
print("\nInformación de 'order_products':")
print(order_products.info())
print("\nPrimeras filas de 'order_products':")
print(order_products.head())# mostrar información del DataFrame
```

    
    Información de 'order_products':
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 4545007 entries, 0 to 4545006
    Data columns (total 4 columns):
     #   Column             Dtype  
    ---  ------             -----  
     0   order_id           int64  
     1   product_id         int64  
     2   add_to_cart_order  float64
     3   reordered          int64  
    dtypes: float64(1), int64(3)
    memory usage: 138.7 MB
    None
    
    Primeras filas de 'order_products':
       order_id  product_id  add_to_cart_order  reordered
    0   2141543       11440               17.0          0
    1    567889        1560                1.0          1
    2   2261212       26683                1.0          1
    3    491251        8670               35.0          1
    4   2571142        1940                5.0          1



```python
print("\nInformación de 'aisles':")
print(aisles.info())
print("\nPrimeras filas de 'aisles':")
print(aisles.head())
# mostrar información del DataFrame
```

    
    Información de 'aisles':
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 134 entries, 0 to 133
    Data columns (total 2 columns):
     #   Column    Non-Null Count  Dtype 
    ---  ------    --------------  ----- 
     0   aisle_id  134 non-null    int64 
     1   aisle     134 non-null    object
    dtypes: int64(1), object(1)
    memory usage: 2.2+ KB
    None
    
    Primeras filas de 'aisles':
       aisle_id                       aisle
    0         1       prepared soups salads
    1         2           specialty cheeses
    2         3         energy granola bars
    3         4               instant foods
    4         5  marinades meat preparation



```python
print("\nInformación de 'departments':")
print(departments.info())
print("\nPrimeras filas de 'departments':")
print(departments.head())# mostrar información del DataFrame
```

    
    Información de 'departments':
    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 21 entries, 0 to 20
    Data columns (total 2 columns):
     #   Column         Non-Null Count  Dtype 
    ---  ------         --------------  ----- 
     0   department_id  21 non-null     int64 
     1   department     21 non-null     object
    dtypes: int64(1), object(1)
    memory usage: 464.0+ bytes
    None
    
    Primeras filas de 'departments':
       department_id department
    0              1     frozen
    1              2      other
    2              3     bakery
    3              4    produce
    4              5    alcohol


## Conclusiones

Escribe aquí tus conclusiones intermedias sobre el Paso 1. Descripción de los datos.

Orders:

información sobre pedidos, con un total de 478,967 registros.
La columna "days_since_prior_order" tiene  28817 valores nulos 


Products:

información sobre productos, con 49,694 registros.
La columna "product_name" tiene 1,258 valores nulos.

Order_Products:

información sobre los productos en cada pedido, con 4,545,007 registros.
La columna "add_to_cart_order" tiene 836 valores nulos.

Aisles:

tiene información sobre los pasillos, con 134 registros.
No hay valores nulos.

Departments:

información sobre los departamentos, con 21 registros.
No hay valores nulos.


# Paso 2. Preprocesamiento de los datos

Preprocesa los datos de la siguiente manera:

- Verifica y corrige los tipos de datos (por ejemplo, asegúrate de que las columnas de ID sean números enteros).
- Identifica y completa los valores ausentes.
- Identifica y elimina los valores duplicados.

Asegúrate de explicar qué tipos de valores ausentes y duplicados encontraste, cómo los completaste o eliminaste y por qué usaste esos métodos. ¿Por qué crees que estos valores ausentes y duplicados pueden haber estado presentes en el conjunto de datos?

## Plan de solución

Escribe aquí tu plan para el Paso 2. Preprocesamiento de los datos.

encontrar y eliminar valores duplicados
encontrar y eliminar valores ausentes
verificar y corregir los tipos de datos

## Encuentra y elimina los valores duplicados (y describe cómo tomaste tus decisiones).

### `orders` data frame


```python
duplicates = orders.duplicated()

orders[duplicates]# Revisa si hay pedidos duplicados

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
      <th>order_id</th>
      <th>user_id</th>
      <th>order_number</th>
      <th>order_dow</th>
      <th>order_hour_of_day</th>
      <th>days_since_prior_order</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>145574</th>
      <td>794638</td>
      <td>50898</td>
      <td>24</td>
      <td>3</td>
      <td>2</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>223105</th>
      <td>2160484</td>
      <td>107525</td>
      <td>16</td>
      <td>3</td>
      <td>2</td>
      <td>30.0</td>
    </tr>
    <tr>
      <th>230807</th>
      <td>1918001</td>
      <td>188546</td>
      <td>14</td>
      <td>3</td>
      <td>2</td>
      <td>16.0</td>
    </tr>
    <tr>
      <th>266232</th>
      <td>1782114</td>
      <td>106752</td>
      <td>1</td>
      <td>3</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>273805</th>
      <td>1112182</td>
      <td>202304</td>
      <td>84</td>
      <td>3</td>
      <td>2</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>284038</th>
      <td>2845099</td>
      <td>31189</td>
      <td>11</td>
      <td>3</td>
      <td>2</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>311713</th>
      <td>1021560</td>
      <td>53767</td>
      <td>3</td>
      <td>3</td>
      <td>2</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>321100</th>
      <td>408114</td>
      <td>68324</td>
      <td>4</td>
      <td>3</td>
      <td>2</td>
      <td>18.0</td>
    </tr>
    <tr>
      <th>323900</th>
      <td>1919531</td>
      <td>191501</td>
      <td>32</td>
      <td>3</td>
      <td>2</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>345917</th>
      <td>2232988</td>
      <td>82565</td>
      <td>1</td>
      <td>3</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>371905</th>
      <td>391768</td>
      <td>57671</td>
      <td>19</td>
      <td>3</td>
      <td>2</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>394347</th>
      <td>467134</td>
      <td>63189</td>
      <td>21</td>
      <td>3</td>
      <td>2</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>411408</th>
      <td>1286742</td>
      <td>183220</td>
      <td>48</td>
      <td>3</td>
      <td>2</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>415163</th>
      <td>2282673</td>
      <td>86751</td>
      <td>49</td>
      <td>3</td>
      <td>2</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>441599</th>
      <td>2125197</td>
      <td>14050</td>
      <td>48</td>
      <td>3</td>
      <td>2</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>
</div>



¿Tienes líneas duplicadas? Si sí, ¿qué tienen en común? Sí, hay líneas duplicadas. Las filas duplicadas tienen el mismo valor en todas las columnas.


```python
wednesday_2_am_orders = orders[(orders['order_dow'] == 3) & (orders['order_hour_of_day'] == 2)]
wednesday_2_am_orders
# Basándote en tus hallazgos,
# Verifica todos los pedidos que se hicieron el miércoles a las 2:00 a.m.


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
      <th>order_id</th>
      <th>user_id</th>
      <th>order_number</th>
      <th>order_dow</th>
      <th>order_hour_of_day</th>
      <th>days_since_prior_order</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4838</th>
      <td>2766110</td>
      <td>162084</td>
      <td>41</td>
      <td>3</td>
      <td>2</td>
      <td>16.0</td>
    </tr>
    <tr>
      <th>5156</th>
      <td>2190225</td>
      <td>138285</td>
      <td>18</td>
      <td>3</td>
      <td>2</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>15506</th>
      <td>553049</td>
      <td>58599</td>
      <td>13</td>
      <td>3</td>
      <td>2</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>18420</th>
      <td>382357</td>
      <td>120200</td>
      <td>19</td>
      <td>3</td>
      <td>2</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>24691</th>
      <td>690242</td>
      <td>77357</td>
      <td>2</td>
      <td>3</td>
      <td>2</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>457013</th>
      <td>3384021</td>
      <td>14881</td>
      <td>6</td>
      <td>3</td>
      <td>2</td>
      <td>30.0</td>
    </tr>
    <tr>
      <th>458816</th>
      <td>910166</td>
      <td>164782</td>
      <td>18</td>
      <td>3</td>
      <td>2</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>459635</th>
      <td>1680532</td>
      <td>106435</td>
      <td>6</td>
      <td>3</td>
      <td>2</td>
      <td>21.0</td>
    </tr>
    <tr>
      <th>468324</th>
      <td>222962</td>
      <td>54979</td>
      <td>59</td>
      <td>3</td>
      <td>2</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>477526</th>
      <td>2592344</td>
      <td>46860</td>
      <td>38</td>
      <td>3</td>
      <td>2</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>
<p>121 rows × 6 columns</p>
</div>



<div class="alert alert-block alert-danger">
<b>Comentario revisor</b> <a class="tocSkip"></a>

Muy buena conclusión, pero te sugiero verificar que el miércoles es el orders['order_dow'] == 2, o puedes ser que el 2 corresponda al martes.
</div>

¿Qué sugiere este resultado? sugiere que hay 121 pedidos los miercoles a las 2 am.
esto nos enseña los patrones de compra en una fecha y horario especifico, podemos comprender como se comporta cada usuario y analizarlo
tambien pueden ser operaciones programadas. por el horario en la madrugada es pósible que como sistema la empresa se concentra en esos dias y horarios en donde el trafico es menor para hacer sus compras programadas. seria importante investigarlo

hice la correccion, el error fue poner el nuemro 2 en lugar del 3 para el dia miercoles 


```python
orders = orders.drop_duplicates()
orders.info()# Elimina los pedidos duplicados
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 478952 entries, 0 to 478966
    Data columns (total 6 columns):
     #   Column                  Non-Null Count   Dtype  
    ---  ------                  --------------   -----  
     0   order_id                478952 non-null  int64  
     1   user_id                 478952 non-null  int64  
     2   order_number            478952 non-null  int64  
     3   order_dow               478952 non-null  int64  
     4   order_hour_of_day       478952 non-null  int64  
     5   days_since_prior_order  450135 non-null  float64
    dtypes: float64(1), int64(5)
    memory usage: 25.6 MB



```python
duplicates_ar = orders[orders.duplicated()]
duplicates_ar# Vuelve a verificar si hay filas duplicadas

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
      <th>order_id</th>
      <th>user_id</th>
      <th>order_number</th>
      <th>order_dow</th>
      <th>order_hour_of_day</th>
      <th>days_since_prior_order</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>




```python
order_ids_duplicated_ar = orders[orders.duplicated(subset='order_id', keep=False)]

order_ids_duplicated_ar# Vuelve a verificar únicamente si hay IDs duplicados de pedidos

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
      <th>order_id</th>
      <th>user_id</th>
      <th>order_number</th>
      <th>order_dow</th>
      <th>order_hour_of_day</th>
      <th>days_since_prior_order</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>



Describe brevemente tus hallazgos y lo que hiciste con ellos
Identifique los Duplicados, revision y Manejo de Datos Nulos y Actualización del DataFrame

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Muy buen trabajo!! Eliminaste esos casos. 
    
</div>

### `products` data frame


```python
products.duplicated().sum()# Verifica si hay filas totalmente duplicadas

```




    0




```python
products['department_id'].duplicated().sum()
# Revisa únicamente si hay ID de departamentos duplicados

```




    49673




```python
duplicates = products['product_name'].str.upper().duplicated().sum()
duplicates
# Revisa únicamente si hay nombres duplicados de productos (convierte los nombres a letras mayúsculas para compararlos mejor)

```




    1361




```python
duplicates = products['product_name'].str.upper().duplicated(keep=False)

duplicated_products = products[duplicates]

duplicated_products['product_name'].str.upper()# Revisa si hay nombres duplicados de productos no faltantes

```




    37                                                   NaN
    41                                       BIOTIN 1000 MCG
    71                                                   NaN
    109                                                  NaN
    185           FRESH SCENT DISHWASHER DETERGENT WITH DAWN
                                  ...                       
    49689                      HIGH PERFORMANCE ENERGY DRINK
    49690                      ORIGINAL PANCAKE & WAFFLE MIX
    49691    ORGANIC INSTANT OATMEAL LIGHT MAPLE BROWN SUGAR
    49692                             SPRING WATER BODY WASH
    49693                            BURRITO- STEAK & CHEESE
    Name: product_name, Length: 1465, dtype: object



<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Muy buen trabajo!! Desarrollaste de manera excelente el análisis de duplicados. Para complementar el análisis, qué podríamos decir de estos 104 productos duplicados? 
    
</div>

Describe brevemente tus hallazgos y lo que hiciste con ellos. identifique y examine los productos duplicados en función de los nombres y se tomaron acciones para entender mejor los duplicados

### `departments` data frame


```python
departments.duplicated().sum()# Revisa si hay filas totalmente duplicadas
```




    0




```python
department_duplicates = departments['department_id'].duplicated().sum()
department_duplicates# Revisa únicamente si hay IDs duplicadas de productos
```




    0



Describe brevemente tus hallazgos y lo que hiciste con ellos. no hay duplicados

### `aisles` data frame


```python
duplicates_aisles = aisles.duplicated().sum()
duplicates_aisles# Revisa si hay filas totalmente duplicadas
```




    0




```python
aisles['aisle_id'].duplicated().sum()# Revisa únicamente si hay IDs duplicadas de productos
```




    0



Describe brevemente tus hallazgos y lo que hiciste con ellos. no hay duplicados

### `order_products` data frame


```python
order_products.duplicated().sum()# Revisa si hay filas totalmente duplicadas

```




    0




```python
order_products["order_id"].duplicated().sum()# Vuelve a verificar si hay cualquier otro duplicado engañoso

```




    4094961



Describe brevemente tus hallazgos y lo que hiciste con ellos. se encontraron muchos IDs de pedidos duplicados. esto puede ser que cada fila representa un producto dentro de un pedido y, por lo tanto, varios productos pueden tener el mismo ID de pedido. 

## Encuentra y elimina los valores ausentes

Al trabajar con valores duplicados, pudimos observar que también nos falta investigar valores ausentes:

* La columna `'product_name'` de la tabla products.
* La columna `'days_since_prior_order'` de la tabla orders.
* La columna `'add_to_cart_order'` de la tabla order_productos.

### `products` data frame


```python
missing_values = products['product_name'].isna().sum()
missing_values# Encuentra los valores ausentes en la columna 'product_name'
```




    1258



Describe brevemente cuáles son tus hallazgos. hay 1258 ausentes


```python
productos_pasillo_100 = products[products['aisle_id'] == 100].isna().sum()

productos_pasillo_100#  ¿Todos los nombres de productos ausentes están relacionados con el pasillo con ID 100?

```




    product_id          0
    product_name     1258
    aisle_id            0
    department_id       0
    dtype: int64



Describe brevemente cuáles son tus hallazgos. es correcto todos los ausentes estan en el pasillo 100


```python
productos_ausentes_departamento_21 = products[products['department_id'] == 21].isna().sum()
productos_ausentes_departamento_21# ¿Todos los nombres de productos ausentes están relacionados con el departamento con ID 21?

```




    product_id          0
    product_name     1258
    aisle_id            0
    department_id       0
    dtype: int64



Describe brevemente cuáles son tus hallazgos. es correcto, tambien esta relacionado con el ID 21


```python
merged_products = products.merge(departments).merge(aisles)
merged_products = merged_products[merged_products["department_id"] == 21]
merged_products = merged_products[merged_products['aisle_id'] == 100]

merged_products

# Usa las tablas department y aisle para revisar los datos del pasillo con ID 100 y el departamento con ID 21.

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
      <th>product_id</th>
      <th>product_name</th>
      <th>aisle_id</th>
      <th>department_id</th>
      <th>department</th>
      <th>aisle</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>42819</th>
      <td>38</td>
      <td>NaN</td>
      <td>100</td>
      <td>21</td>
      <td>missing</td>
      <td>missing</td>
    </tr>
    <tr>
      <th>42820</th>
      <td>72</td>
      <td>NaN</td>
      <td>100</td>
      <td>21</td>
      <td>missing</td>
      <td>missing</td>
    </tr>
    <tr>
      <th>42821</th>
      <td>110</td>
      <td>NaN</td>
      <td>100</td>
      <td>21</td>
      <td>missing</td>
      <td>missing</td>
    </tr>
    <tr>
      <th>42822</th>
      <td>297</td>
      <td>NaN</td>
      <td>100</td>
      <td>21</td>
      <td>missing</td>
      <td>missing</td>
    </tr>
    <tr>
      <th>42823</th>
      <td>417</td>
      <td>NaN</td>
      <td>100</td>
      <td>21</td>
      <td>missing</td>
      <td>missing</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>44072</th>
      <td>49553</td>
      <td>NaN</td>
      <td>100</td>
      <td>21</td>
      <td>missing</td>
      <td>missing</td>
    </tr>
    <tr>
      <th>44073</th>
      <td>49575</td>
      <td>NaN</td>
      <td>100</td>
      <td>21</td>
      <td>missing</td>
      <td>missing</td>
    </tr>
    <tr>
      <th>44074</th>
      <td>49641</td>
      <td>NaN</td>
      <td>100</td>
      <td>21</td>
      <td>missing</td>
      <td>missing</td>
    </tr>
    <tr>
      <th>44075</th>
      <td>49664</td>
      <td>NaN</td>
      <td>100</td>
      <td>21</td>
      <td>missing</td>
      <td>missing</td>
    </tr>
    <tr>
      <th>44076</th>
      <td>49669</td>
      <td>NaN</td>
      <td>100</td>
      <td>21</td>
      <td>missing</td>
      <td>missing</td>
    </tr>
  </tbody>
</table>
<p>1258 rows × 6 columns</p>
</div>



Describe brevemente cuáles son tus hallazgos. los productos en el pasillo con ID 100 y el departamento con ID 21 tienen información faltante en varias columnas, lo que podría indicar falta de información en esos registros específicos. 



```python
products["product_name"].fillna('Unknown', inplace=True)
# Completa los nombres de productos ausentes con 'Unknown'

```

Describe brevemente tus hallazgos y lo que hiciste con ellos.

### `orders` data frame


```python
missing_values_orders = orders.isna().sum()
missing_values_orders# Encuentra los valores ausentes
```




    order_id                      0
    user_id                       0
    order_number                  0
    order_dow                     0
    order_hour_of_day             0
    days_since_prior_order    28817
    dtype: int64




```python
primer_pedido = orders[orders["order_number"] > 1]
primer_pedido_ausente = primer_pedido["days_since_prior_order"].isna().sum()
primer_pedido_ausente# ¿Hay algún valor ausente que no sea el primer pedido del cliente?

```




    0



Describe brevemente tus hallazgos y lo que hiciste con ellos. todos los valores ausentes en la columna days_since_prior_order están relacionados con el primer pedido de un cliente


### `order_products` data frame


```python
missing_order_products = order_products.isna().sum()
missing_order_products# Encuentra los valores ausentes
```




    order_id               0
    product_id             0
    add_to_cart_order    836
    reordered              0
    dtype: int64




```python
min_add_to_cart_order  = order_products['add_to_cart_order'].min()
max_add_to_cart_order  = order_products['add_to_cart_order'].max()

min_add_to_cart_order, max_add_to_cart_order

# ¿Cuáles son los valores mínimos y máximos en esta columna?

```




    (1.0, 64.0)



Describe brevemente cuáles son tus hallazgos.  tiene algunos valores ausentes, y los valores presentes en esta columna estan entre 1 y 64


```python
add_to_cart_missing = order_products[order_products['add_to_cart_order'].isna()]['order_id'].unique()# Guarda todas las IDs de pedidos que tengan un valor ausente en 'add_to_cart_order'
add_to_cart_missing.sum()
```




    112724954




```python
orders_with_missing = order_products.query("order_id in @add_to_cart_missing")
product_count_per_order = orders_with_missing.groupby('order_id')['product_id'].count()
min_product_count = product_count_per_order.min()
min_product_count

# ¿Todos los pedidos con valores ausentes tienen más de 64 productos?
# Agrupa todos los pedidos con datos ausentes por su ID de pedido.
# Cuenta el número de 'product_id' en cada pedido y revisa el valor mínimo del conteo.
pedidos_mas_64 = product_count_per_order[product_count_per_order > 64]

pedidos_mas_64.describe()

```




    count     70.000000
    mean      75.942857
    std       12.898585
    min       65.000000
    25%       67.000000
    50%       71.000000
    75%       78.000000
    max      127.000000
    Name: product_id, dtype: float64



Describe brevemente cuáles son tus hallazgos. si hay mas de 64, son 65
para poder decir de los pedidos que tiene mas de 64 productos use describe()

mi conclusion es la siguiente:

El promedio de productos en estos pedidos es 75.94.
La desviación estándar es de aproximadamente 12.90
El pedido más pequeño tiene 65 productos, mientras que el más grande tiene 127.
El 25% de los pedidos tienen 67 productos o menos.
El 50% de los pedidos tienen 71 productos o menos.
El 75% de los pedidos tienen 78 productos o menos.


<div class="alert alert-block alert-warning">
<b>Comentario revisor</b> <a class="tocSkip"></a>


Muy buena conclusión de esta base. Pero qué podríamos decir de los pedidos que tienen más de 64 productos?
</div>


```python
order_products["add_to_cart_order"] = order_products["add_to_cart_order"].fillna(999).astype(int) # Remplaza los valores ausentes en la columna 'add_to_cart? con 999 y convierte la columna al tipo entero.

```

Describe brevemente tus hallazgos y lo que hiciste con ellos.

## Conclusiones

Escribe aquí tus conclusiones intermedias sobre el Paso 2. Preprocesamiento de los datos
hice las siguientes acciones:

Identificación de Valores Ausentes, 
Exploración de Duplicados, 
Análisis de Características Específicas, 
Modificación de Datos, 
Validación de Rangos.

Con todas estas acciones seria muy importante hacer preguntas especificas para lograr un estudio completo

# Paso 3. Análisis de los datos

Una vez los datos estén procesados y listos, haz el siguiente análisis:

# [A] Fácil (deben completarse todos para aprobar)

1. Verifica que los valores en las columnas `'order_hour_of_day'` y `'order_dow'` en la tabla orders sean razonables (es decir, `'order_hour_of_day'` oscile entre 0 y 23 y `'order_dow'` oscile entre 0 y 6).
2. Crea un gráfico que muestre el número de personas que hacen pedidos dependiendo de la hora del día.
3. Crea un gráfico que muestre qué día de la semana la gente hace sus compras.
4. Crea un gráfico que muestre el tiempo que la gente espera hasta hacer su siguiente pedido, y comenta sobre los valores mínimos y máximos.

### [A1] Verifica que los valores sean sensibles


```python
orders['order_hour_of_day'].value_counts().sort_index()
```




    0      3180
    1      1763
    2       989
    3       770
    4       765
    5      1371
    6      4215
    7     13043
    8     25024
    9     35896
    10    40578
    11    40032
    12    38034
    13    39007
    14    39631
    15    39789
    16    38112
    17    31930
    18    25510
    19    19547
    20    14624
    21    11019
    22     8512
    23     5611
    Name: order_hour_of_day, dtype: int64




```python
orders['order_dow'].value_counts().sort_index()
```




    0    84090
    1    82185
    2    65833
    3    60897
    4    59810
    5    63488
    6    62649
    Name: order_dow, dtype: int64



Escribe aquí tus conclusiones. las 2 columnas son razonables por que en hour of the day tiene del 0 al 23(24 horas del dia) y order dow del 0 al 6(7 dias de la semana)

### [A2] Para cada hora del día, ¿cuántas personas hacen órdenes?


```python
import pandas as pd
from matplotlib import pyplot as plt
order_hour_counts = orders['order_hour_of_day'].value_counts().sort_index()
hour_names = ['1 am', '2 am', '3 am', '4 am', '5 am', '6 am', '7 am', "8 am", "9 am", "10 am", "11 am", "12 pm", "1 pm", "2 pm", "3 pm", "4 pm", "5 pm", "6 pm", "7 pm", "8 pm", "9pm", "10pm", "11 pm", "12 am"]
order_hour_counts.index = hour_names

order_hour_counts.plot(kind="bar",
                      color= "blue",
                       figsize= (10,6),
                      title= "Para cada hora del día, ¿cuántas personas hacen órdenes?",
                      xlabel= "Hora del Día",
                      ylabel= "Número de Personas")


plt.show
```




    <function matplotlib.pyplot.show(close=None, block=None)>




    
![png](output_81_1.png)
    


Escribe aquí tus conclusiones el horario con mas ordenes es las 11 am y el menor las 4 am

las horas con mayores pedidos son las 11 am, de ahi se van a las 4 y 3 pm

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Muy buen trabajo!! Buen uso de la gráfica de barras para mostrar la distribución por horas.
    
</div>

<div class="alert alert-block alert-warning">
<b>Comentario Revisor</b> <a class="tocSkip"></a>

Cuáles son las horas con mayores pedidos?
</div>

### [A3] ¿Qué día de la semana compran víveres las personas?


```python
import pandas as pd
from matplotlib import pyplot as plt


order_dow_counts = orders['order_dow'].value_counts().sort_index()

day_names = ['Domingo', 'Lunes', 'Martes', 'Miércoles', 'Jueves', 'Viernes', 'Sábado']
order_dow_counts.index = day_names

# Crea el gráfico de barras
order_dow_counts.plot(kind="bar",
                      color="green",
                      figsize=(10, 6),
                      title="Número de Pedidos por Día de la Semana",
                      xlabel="Día de la Semana",
                      ylabel="Número de Pedidos")

plt.show()
```


    
![png](output_86_0.png)
    


Escribe aquí tus conclusiones domingo es el que mas pedidos tiene y jueves el que menos

### [A4] ¿Cuánto tiempo esperan las personas hasta hacer otro pedido? Comenta sobre los valores mínimos y máximos.


```python
import pandas as pd
from matplotlib import pyplot as plt

plt.figure(figsize=(12, 6))
waiting_time = orders['days_since_prior_order']

plt.hist(waiting_time, bins=30, color="purple")

min_waiting_time = waiting_time.min()
max_waiting_time = waiting_time.max()

plt.plot([min_waiting_time, min_waiting_time], [0, plt.ylim()[1]], color='red', label='Min Waiting Time')
plt.plot([max_waiting_time, max_waiting_time], [0, plt.ylim()[1]], color='green', label='Max Waiting Time')

plt.xlabel('Días para el Próximo Pedido')
plt.ylabel('Frecuencia')
plt.title('¿Cuánto tiempo esperan las personas hasta hacer otro pedido? ')
plt.legend()

plt.show()

tardan_cero = orders[orders['days_since_prior_order'] == 0]
tardan_cero.shape[0]
```


    
![png](output_89_0.png)
    





    9589



<div class="alert alert-block alert-warning">
<b>Comentario Revisor</b> <a class="tocSkip"></a>

Qué podemos decir de los que tardar 0 días?
</div>

Escribe aquí tus conclusiones. la mayoria espera casi los 30 dias

use shape para saber cuantos pedidos tenemos si tardan 0 dias y tenemos 9589


# [B] Intermedio (deben completarse todos para aprobar)

1. ¿Existe alguna diferencia entre las distribuciones `'order_hour_of_day'` de los miércoles y los sábados? Traza gráficos de barra de `'order_hour_of_day'` para ambos días en la misma figura y describe las diferencias que observes.
2. Grafica la distribución para el número de órdenes que hacen los clientes (es decir, cuántos clientes hicieron solo 1 pedido, cuántos hicieron 2, cuántos 3, y así sucesivamente...).
3. ¿Cuáles son los 20 principales productos que se piden con más frecuencia (muestra su identificación y nombre)?

### [B1] Diferencia entre miércoles y sábados para  `'order_hour_of_day'`. Traza gráficos de barra para los dos días y describe las diferencias que veas.


```python
import pandas as pd
from matplotlib import pyplot as plt

miercoles_data = orders[orders['order_dow'] == 3]
sabado_data = orders[orders['order_dow'] == 6]

miercoles_hour_counts = miercoles_data['order_hour_of_day'].value_counts().sort_index()
sabado_hour_counts = sabado_data['order_hour_of_day'].value_counts().sort_index()

plt.figure(figsize=(12, 6))

plt.plot(miercoles_hour_counts, label='Miércoles', color='blue')
plt.plot(sabado_hour_counts, label='Sábado', color='green')

plt.xlabel('Hora del Día')
plt.ylabel('Número de Pedidos')
plt.title('Distribución de "order_hour_of_day" para Miércoles y Sábado')
plt.legend()

plt.show()
```


    
![png](output_94_0.png)
    


<div class="alert alert-block alert-danger">
<b>Comentario revisor</b> <a class="tocSkip"></a>


La gráfica la desarrollaste de gran forma. Solamente te recomiendo verificar que el sábado corresponde al día 5. 
</div>


```python

```


```python

```

Escribe aquí tus conclusiones el sabado es mayor. ya lo corregi, me equivoque con el numero de dia

### [B2] ¿Cuál es la distribución para el número de pedidos por cliente?


```python
import pandas as pd
from matplotlib import pyplot as plt

orders_per_user = orders.groupby('user_id')['order_number'].max().value_counts().sort_index()

plt.figure(figsize=(12, 6))

plt.plot(
    orders_per_user.index, 
    orders_per_user.values, 
    marker='o', 
    linestyle='-', 
    color='purple'
)

plt.xlabel('Número de Órdenes por Cliente')
plt.ylabel('Número de Clientes')
plt.title('Distribución del Número de Órdenes por Cliente')
plt.grid(True)
plt.show()
```


    
![png](output_100_0.png)
    



```python

```

Escribe aquí tus conclusiones donde mas hay son menos de 20

### [B3] ¿Cuáles son los 20 productos más populares (muestra su ID y nombre)?


```python
top_products_frequency = order_products['product_id'].value_counts().head(20)


top_products = pd.merge(top_products_frequency, products, left_index=True, right_on='product_id')

top_products
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
      <th>product_id</th>
      <th>product_id_x</th>
      <th>product_id_y</th>
      <th>product_name</th>
      <th>aisle_id</th>
      <th>department_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>24851</th>
      <td>24852</td>
      <td>66050</td>
      <td>24852</td>
      <td>Banana</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>13175</th>
      <td>13176</td>
      <td>53297</td>
      <td>13176</td>
      <td>Bag of Organic Bananas</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>21136</th>
      <td>21137</td>
      <td>37039</td>
      <td>21137</td>
      <td>Organic Strawberries</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>21902</th>
      <td>21903</td>
      <td>33971</td>
      <td>21903</td>
      <td>Organic Baby Spinach</td>
      <td>123</td>
      <td>4</td>
    </tr>
    <tr>
      <th>47208</th>
      <td>47209</td>
      <td>29773</td>
      <td>47209</td>
      <td>Organic Hass Avocado</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>47765</th>
      <td>47766</td>
      <td>24689</td>
      <td>47766</td>
      <td>Organic Avocado</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>47625</th>
      <td>47626</td>
      <td>21495</td>
      <td>47626</td>
      <td>Large Lemon</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>16796</th>
      <td>16797</td>
      <td>20018</td>
      <td>16797</td>
      <td>Strawberries</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>26208</th>
      <td>26209</td>
      <td>19690</td>
      <td>26209</td>
      <td>Limes</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>27844</th>
      <td>27845</td>
      <td>19600</td>
      <td>27845</td>
      <td>Organic Whole Milk</td>
      <td>84</td>
      <td>16</td>
    </tr>
    <tr>
      <th>27965</th>
      <td>27966</td>
      <td>19197</td>
      <td>27966</td>
      <td>Organic Raspberries</td>
      <td>123</td>
      <td>4</td>
    </tr>
    <tr>
      <th>22934</th>
      <td>22935</td>
      <td>15898</td>
      <td>22935</td>
      <td>Organic Yellow Onion</td>
      <td>83</td>
      <td>4</td>
    </tr>
    <tr>
      <th>24963</th>
      <td>24964</td>
      <td>15292</td>
      <td>24964</td>
      <td>Organic Garlic</td>
      <td>83</td>
      <td>4</td>
    </tr>
    <tr>
      <th>45006</th>
      <td>45007</td>
      <td>14584</td>
      <td>45007</td>
      <td>Organic Zucchini</td>
      <td>83</td>
      <td>4</td>
    </tr>
    <tr>
      <th>39274</th>
      <td>39275</td>
      <td>13879</td>
      <td>39275</td>
      <td>Organic Blueberries</td>
      <td>123</td>
      <td>4</td>
    </tr>
    <tr>
      <th>49682</th>
      <td>49683</td>
      <td>13675</td>
      <td>49683</td>
      <td>Cucumber Kirby</td>
      <td>83</td>
      <td>4</td>
    </tr>
    <tr>
      <th>28203</th>
      <td>28204</td>
      <td>12544</td>
      <td>28204</td>
      <td>Organic Fuji Apple</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5875</th>
      <td>5876</td>
      <td>12232</td>
      <td>5876</td>
      <td>Organic Lemon</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>8276</th>
      <td>8277</td>
      <td>11993</td>
      <td>8277</td>
      <td>Apple Honeycrisp Organic</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>40705</th>
      <td>40706</td>
      <td>11781</td>
      <td>40706</td>
      <td>Organic Grape Tomatoes</td>
      <td>123</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize=(12, 8))
plt.bar(top_products['product_name'], top_products['product_id_x'], color='blue')
plt.xlabel('Nombre del Producto')
plt.ylabel('Frecuencia')
plt.title('20 principales productos que se piden con más frecuencia')
plt.xticks(rotation=90) 
plt.show()
```


    
![png](output_105_0.png)
    



```python

```

Escribe aquí tus conclusiones Los 20 productos más frecuentes en los pedidos son productos comunes y esenciales, como frutas (bananas, fresas), verduras (espinaca, aguacate), lácteos (leche orgánica) y cítricos (limones)

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Muy buen desarrollo de la sección. Desarrollaste de buena manera todos los análisis y lo complementaste con una gráfica. Solamente te recomiendo escribir la conclusión de cada resultado con tus hallazgos. 
</div>

# [C] Difícil (deben completarse todos para aprobar)

1. ¿Cuántos artículos suelen comprar las personas en un pedido? ¿Cómo es la distribución?
2. ¿Cuáles son los 20 principales artículos que vuelven a pedirse con mayor frecuencia (muestra sus nombres e IDs de los productos)?
3. Para cada producto, ¿cuál es la tasa de repetición del pedido (número de repeticiones de pedido/total de pedidos?
4. Para cada cliente, ¿qué proporción de los productos que pidió ya los había pedido? Calcula la tasa de repetición de pedido para cada usuario en lugar de para cada producto.
5. ¿Cuáles son los 20 principales artículos que la gente pone primero en sus carritos (muestra las IDs de los productos, sus nombres, y el número de veces en que fueron el primer artículo en añadirse al carrito)?

### [C1] ¿Cuántos artículos compran normalmente las personas en un pedido? ¿Cómo es la distribución?


```python
items_per_order = order_products.groupby('order_id')['add_to_cart_order'].max()

items_per_order

filtered_items_per_order = items_per_order[items_per_order <= 35]

items_counts = filtered_items_per_order.value_counts().sort_index()

items_counts


```




    1     21847
    2     26292
    3     29046
    4     31054
    5     31923
    6     31698
    7     30822
    8     28539
    9     25742
    10    23248
    11    20406
    12    18539
    13    16497
    14    14472
    15    12696
    16    11465
    17    10002
    18     8726
    19     7612
    20     6771
    21     5738
    22     5096
    23     4422
    24     3838
    25     3382
    26     2812
    27     2458
    28     2137
    29     1899
    30     1618
    31     1328
    32     1171
    33     1003
    34      845
    35      686
    Name: add_to_cart_order, dtype: int64




```python
plt.figure(figsize=(12, 6))
items_counts.plot(kind="bar", color="green")
plt.xlabel("Número de Artículos por Pedido")
plt.ylabel("Número de Pedidos")
plt.title("Distribución de la Cantidad de Artículos por Pedido")
plt.show()
```


    
![png](output_112_0.png)
    


<div class="alert alert-block alert-warning">
<b>Comentario Revisor</b> <a class="tocSkip"></a>

Muy buen trabajo, pero pareciera que las personas que tardan 35 artículos puede ser un error. Entonces te sugiero complementar este análisis con una gráfica donde se muestren los valores sin contar los mayores de 35.
</div>

Escribe aquí tus conclusiones  La mayoría de los pedidos contienen entre 5 y 15 productos

listo, lo limite hasta 35 articulos y la grafica se ve mucho mas clara

### [C2] ¿Cuáles son los 20 principales artículos que vuelven a pedirse con mayor frecuencia (muestra sus nombres e IDs de los productos)?


```python
reordered_products = order_products[order_products['reordered'] == 1]['product_id'].value_counts().head(20)

reordered_products_info = pd.merge(reordered_products, products, left_index=True, right_on='product_id')


reordered_products_info
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
      <th>product_id</th>
      <th>product_id_x</th>
      <th>product_id_y</th>
      <th>product_name</th>
      <th>aisle_id</th>
      <th>department_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>24851</th>
      <td>24852</td>
      <td>55763</td>
      <td>24852</td>
      <td>Banana</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>13175</th>
      <td>13176</td>
      <td>44450</td>
      <td>13176</td>
      <td>Bag of Organic Bananas</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>21136</th>
      <td>21137</td>
      <td>28639</td>
      <td>21137</td>
      <td>Organic Strawberries</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>21902</th>
      <td>21903</td>
      <td>26233</td>
      <td>21903</td>
      <td>Organic Baby Spinach</td>
      <td>123</td>
      <td>4</td>
    </tr>
    <tr>
      <th>47208</th>
      <td>47209</td>
      <td>23629</td>
      <td>47209</td>
      <td>Organic Hass Avocado</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>47765</th>
      <td>47766</td>
      <td>18743</td>
      <td>47766</td>
      <td>Organic Avocado</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>27844</th>
      <td>27845</td>
      <td>16251</td>
      <td>27845</td>
      <td>Organic Whole Milk</td>
      <td>84</td>
      <td>16</td>
    </tr>
    <tr>
      <th>47625</th>
      <td>47626</td>
      <td>15044</td>
      <td>47626</td>
      <td>Large Lemon</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>27965</th>
      <td>27966</td>
      <td>14748</td>
      <td>27966</td>
      <td>Organic Raspberries</td>
      <td>123</td>
      <td>4</td>
    </tr>
    <tr>
      <th>16796</th>
      <td>16797</td>
      <td>13945</td>
      <td>16797</td>
      <td>Strawberries</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>26208</th>
      <td>26209</td>
      <td>13327</td>
      <td>26209</td>
      <td>Limes</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>22934</th>
      <td>22935</td>
      <td>11145</td>
      <td>22935</td>
      <td>Organic Yellow Onion</td>
      <td>83</td>
      <td>4</td>
    </tr>
    <tr>
      <th>24963</th>
      <td>24964</td>
      <td>10411</td>
      <td>24964</td>
      <td>Organic Garlic</td>
      <td>83</td>
      <td>4</td>
    </tr>
    <tr>
      <th>45006</th>
      <td>45007</td>
      <td>10076</td>
      <td>45007</td>
      <td>Organic Zucchini</td>
      <td>83</td>
      <td>4</td>
    </tr>
    <tr>
      <th>49682</th>
      <td>49683</td>
      <td>9538</td>
      <td>49683</td>
      <td>Cucumber Kirby</td>
      <td>83</td>
      <td>4</td>
    </tr>
    <tr>
      <th>28203</th>
      <td>28204</td>
      <td>8989</td>
      <td>28204</td>
      <td>Organic Fuji Apple</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>8276</th>
      <td>8277</td>
      <td>8836</td>
      <td>8277</td>
      <td>Apple Honeycrisp Organic</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>39274</th>
      <td>39275</td>
      <td>8799</td>
      <td>39275</td>
      <td>Organic Blueberries</td>
      <td>123</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5875</th>
      <td>5876</td>
      <td>8412</td>
      <td>5876</td>
      <td>Organic Lemon</td>
      <td>24</td>
      <td>4</td>
    </tr>
    <tr>
      <th>49234</th>
      <td>49235</td>
      <td>8389</td>
      <td>49235</td>
      <td>Organic Half &amp; Half</td>
      <td>53</td>
      <td>16</td>
    </tr>
  </tbody>
</table>
</div>




```python
top_products_frequency = order_products['product_id'].value_counts().head(20)
top_products = pd.merge(top_products_frequency, products, left_index=True, right_on='product_id')


plt.figure(figsize=(12, 6))
plt.bar(top_products['product_name'], top_products['product_id_x'], color='red')
plt.xlabel('Nombre del Producto')
plt.ylabel('Frecuencia de Pedido')
plt.title('Top 20 Productos Más Populares')
plt.xticks(rotation=45, ha='right')  
plt.show()
```


    
![png](output_117_0.png)
    



```python

```


```python

```

Escribe aquí tus conclusiones Los 20 principales artículos que se vuelven a pedir con mayor frecuencia incluyen productos como bananas, bolsas de plátanos orgánicos, fresas orgánicas y aguacates orgánicos.

### [C3] Para cada producto, ¿cuál es la proporción de las veces que se pide y que se vuelve a pedir?


```python
reorder_proportion = order_products.groupby('product_id')['reordered'].mean().reset_index()

reorder_proportion = pd.merge(reorder_proportion, products, on='product_id')

reorder_proportion
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
      <th>product_id</th>
      <th>reordered</th>
      <th>product_name</th>
      <th>aisle_id</th>
      <th>department_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.564286</td>
      <td>Chocolate Sandwich Cookies</td>
      <td>61</td>
      <td>19</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.000000</td>
      <td>All-Seasons Salt</td>
      <td>104</td>
      <td>13</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.738095</td>
      <td>Robust Golden Unsweetened Oolong Tea</td>
      <td>94</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.510204</td>
      <td>Smart Ones Classic Favorites Mini Rigatoni Wit...</td>
      <td>38</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7</td>
      <td>0.500000</td>
      <td>Pure Coconut Water With Orange</td>
      <td>98</td>
      <td>7</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>45568</th>
      <td>49690</td>
      <td>0.800000</td>
      <td>HIGH PERFORMANCE ENERGY DRINK</td>
      <td>64</td>
      <td>7</td>
    </tr>
    <tr>
      <th>45569</th>
      <td>49691</td>
      <td>0.430556</td>
      <td>ORIGINAL PANCAKE &amp; WAFFLE MIX</td>
      <td>130</td>
      <td>14</td>
    </tr>
    <tr>
      <th>45570</th>
      <td>49692</td>
      <td>0.416667</td>
      <td>ORGANIC INSTANT OATMEAL LIGHT MAPLE BROWN SUGAR</td>
      <td>130</td>
      <td>14</td>
    </tr>
    <tr>
      <th>45571</th>
      <td>49693</td>
      <td>0.440000</td>
      <td>SPRING WATER BODY WASH</td>
      <td>127</td>
      <td>11</td>
    </tr>
    <tr>
      <th>45572</th>
      <td>49694</td>
      <td>0.333333</td>
      <td>BURRITO- STEAK &amp; CHEESE</td>
      <td>38</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>45573 rows × 5 columns</p>
</div>




```python
reorder_proportion = order_products.groupby('product_id')['reordered'].mean().reset_index()


reorder_proportion = pd.merge(reorder_proportion, products[['product_id', 'product_name']], on='product_id')

reorder_proportion = reorder_proportion.sort_values(by='reordered', ascending=False)

plt.figure(figsize=(12, 6))
plt.bar(reorder_proportion['product_name'][:20], reorder_proportion['reordered'][:20], color='blue')
plt.xticks(rotation=90)
plt.xlabel('Producto')
plt.ylabel('Proporción de Veces que se Vuelve a Pedir')
plt.title('Proporción de Veces que se Vuelve a Pedir para los 20 Principales Productos')
plt.show()
```


    
![png](output_123_0.png)
    



```python



```

Escribe aquí tus conclusiones  Algunos productos tienen una alta proporción, mientras que otros tienen una proporción más baja.

### [C4] Para cada cliente, ¿qué proporción de sus productos ya los había pedido?


```python

```

<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

Muy buena utilización del merge y de la agrupación de los valores. Pero en este caso nos piden sacar el dato para cada cliente, en este sentido dentro del groupby te sugiero utilizar la variable 'user_id'.
    
</div>


```python
merged_df = pd.merge(order_products, orders[['order_id', 'user_id']], on='order_id')

user_reorder_proportion = merged_df.groupby('user_id')['reordered'].mean().reset_index()
user_reorder_proportion = user_reorder_proportion.sort_values(by='reordered', ascending=False)

plt.figure(figsize=(14, 6))
plt.bar(user_reorder_proportion['user_id'], user_reorder_proportion['reordered'], color='orange')
plt.xlabel('Usuario')
plt.ylabel('Proporción Promedio de Reincidencia')
plt.title('Proporción Promedio de Reincidencia para Todos los Usuarios')
plt.show()
```


    
![png](output_129_0.png)
    



```python
merged_df = pd.merge(orders, order_products, on='order_id', how='inner')

user_reorder_proportion = merged_df.groupby('user_id')['reordered'].mean().reset_index()
user_reorder_proportion = user_reorder_proportion.sort_values(by='reordered', ascending=False)

reorder_stats = user_reorder_proportion['reordered'].describe()
print(reorder_stats)

plt.hist(user_reorder_proportion['reordered'], bins=20, color='blue', alpha=0.7)
plt.xlabel('Proporción de Reincidencia')
plt.ylabel('Frecuencia')
plt.title('Histograma de Proporción de Reincidencia por Cliente')
plt.show()
```

    count    149626.000000
    mean          0.494853
    std           0.292685
    min           0.000000
    25%           0.272727
    50%           0.500000
    75%           0.724138
    max           1.000000
    Name: reordered, dtype: float64



    
![png](output_130_1.png)
    


Escribe aquí tus conclusiones 

### [C5] ¿Cuáles son los 20 principales artículos que las personas ponen primero en sus carritos?


```python
first_in_cart = order_products[order_products['add_to_cart_order'] == 1]

top_first_in_cart = first_in_cart['product_id'].value_counts().head(20).reset_index()
top_first_in_cart.columns = ['product_id', 'count']

top_first_in_cart = pd.merge(top_first_in_cart, products[['product_id', 'product_name']], on='product_id')

top_first_in_cart
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
      <th>product_id</th>
      <th>count</th>
      <th>product_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>24852</td>
      <td>15562</td>
      <td>Banana</td>
    </tr>
    <tr>
      <th>1</th>
      <td>13176</td>
      <td>11026</td>
      <td>Bag of Organic Bananas</td>
    </tr>
    <tr>
      <th>2</th>
      <td>27845</td>
      <td>4363</td>
      <td>Organic Whole Milk</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21137</td>
      <td>3946</td>
      <td>Organic Strawberries</td>
    </tr>
    <tr>
      <th>4</th>
      <td>47209</td>
      <td>3390</td>
      <td>Organic Hass Avocado</td>
    </tr>
    <tr>
      <th>5</th>
      <td>21903</td>
      <td>3336</td>
      <td>Organic Baby Spinach</td>
    </tr>
    <tr>
      <th>6</th>
      <td>47766</td>
      <td>3044</td>
      <td>Organic Avocado</td>
    </tr>
    <tr>
      <th>7</th>
      <td>19660</td>
      <td>2336</td>
      <td>Spring Water</td>
    </tr>
    <tr>
      <th>8</th>
      <td>16797</td>
      <td>2308</td>
      <td>Strawberries</td>
    </tr>
    <tr>
      <th>9</th>
      <td>27966</td>
      <td>2024</td>
      <td>Organic Raspberries</td>
    </tr>
    <tr>
      <th>10</th>
      <td>44632</td>
      <td>1914</td>
      <td>Sparkling Water Grapefruit</td>
    </tr>
    <tr>
      <th>11</th>
      <td>49235</td>
      <td>1797</td>
      <td>Organic Half &amp; Half</td>
    </tr>
    <tr>
      <th>12</th>
      <td>47626</td>
      <td>1737</td>
      <td>Large Lemon</td>
    </tr>
    <tr>
      <th>13</th>
      <td>196</td>
      <td>1733</td>
      <td>Soda</td>
    </tr>
    <tr>
      <th>14</th>
      <td>38689</td>
      <td>1397</td>
      <td>Organic Reduced Fat Milk</td>
    </tr>
    <tr>
      <th>15</th>
      <td>26209</td>
      <td>1370</td>
      <td>Limes</td>
    </tr>
    <tr>
      <th>16</th>
      <td>12341</td>
      <td>1340</td>
      <td>Hass Avocados</td>
    </tr>
    <tr>
      <th>17</th>
      <td>5785</td>
      <td>1310</td>
      <td>Organic Reduced Fat 2% Milk</td>
    </tr>
    <tr>
      <th>18</th>
      <td>27086</td>
      <td>1309</td>
      <td>Half &amp; Half</td>
    </tr>
    <tr>
      <th>19</th>
      <td>22935</td>
      <td>1246</td>
      <td>Organic Yellow Onion</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.figure(figsize=(12, 6))
plt.bar(top_first_in_cart['product_name'], top_first_in_cart['count'], color='purple')
plt.xticks(rotation=90)
plt.xlabel('Producto')
plt.ylabel('Cantidad de Veces Primero en el Carrito')
plt.title('20 Principales Productos Primero en el Carrito')
plt.show()
```


    
![png](output_134_0.png)
    



```python

```

Escribe aquí tus conclusiones Los 20 principales artículos que las personas suelen poner primero en sus carritos incluyen productos como "Banana", "Bag of Organic Bananas", "Organic Whole Milk", entre otros.


### Conclusion general del proyecto:

<div class="alert alert-block alert-warning">
<b>Comentario revisor</b> <a class="tocSkip"></a>

En general creo que hiciste un muy buen trabajo con el proyecto, pudiste limpiar y trabajar las bases de datos de beuna manera, análisis de duplicados, y de valores faltantes. Además dearrollaste de buena manera los diferentes anális que se solicitaban y cuando podías los complementabas con greaficas. No obstante, recuerda que siempre podemos mejorar y te menciono algunos puntos que debes considerar:

* Revisar que en la variable 'order_dow' estamos clasificando bien los días
    
*  Realizar análisis complementarios eliminando los valores que parecen ser atípicos. 
    
    
*  Profundizar en los resultados intermedios y en la conclusión final.

</div>
