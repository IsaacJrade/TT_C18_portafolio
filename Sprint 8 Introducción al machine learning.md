# Hola Isaac! <a class="tocSkip"></a>

Mi nombre es Oscar Flores y tengo el gusto de revisar tu proyecto. Si tienes algún comentario que quieras agregar en tus respuestas te puedes referir a mi como Oscar, no hay problema que me trates de tú.

Si veo un error en la primera revisión solamente lo señalaré y dejaré que tú encuentres de qué se trata y cómo arreglarlo. Debo prepararte para que te desempeñes como especialista en Data, en un trabajo real, el responsable a cargo tuyo hará lo mismo. Si aún tienes dificultades para resolver esta tarea, te daré indicaciones más precisas en una siguiente iteración.

Te dejaré mis comentarios más abajo - **por favor, no los muevas, modifiques o borres**

Comenzaré mis comentarios con un resumen de los puntos que están bien, aquellos que debes corregir y aquellos que puedes mejorar. Luego deberás revisar todo el notebook para leer mis comentarios, los cuales estarán en rectángulos de color verde, amarillo o rojo como siguen:

<div class="alert alert-block alert-success">
<b>Comentario de Reviewer</b> <a class="tocSkip"></a>
    
Muy bien! Toda la respuesta fue lograda satisfactoriamente.
</div>

<div class="alert alert-block alert-warning">
<b>Comentario de Reviewer</b> <a class="tocSkip"></a>

Existen detalles a mejorar. Existen recomendaciones.
</div>

<div class="alert alert-block alert-danger">

<b>Comentario de Reviewer</b> <a class="tocSkip"></a>

Se necesitan correcciones en el bloque. El trabajo no puede ser aceptado con comentarios en rojo sin solucionar.
</div>

Cualquier comentario que quieras agregar entre iteraciones de revisión lo puedes hacer de la siguiente manera:

<div class="alert alert-block alert-info">
<b>Respuesta estudiante.</b> <a class="tocSkip"></a>
</div>

Mucho éxito en el proyecto!

## Resumen de la revisión 1 <a class="tocSkip"></a>

<div class="alert alert-block alert-danger">
<b>Comentario de Revisor</b> <a class="tocSkip"></a>

Bien hecho Isaac, tu notebook está casi terminado. Debes completarlo agregando un modelo trivial a modo de test de cordura y agregar conclusiones.
    
Saludos!    

</div>

## Resumen de la revisión 2 <a class="tocSkip"></a>

<div class="alert alert-block alert-success">
<b>Comentario de Revisor v2</b> <a class="tocSkip"></a>

Muy bien Isaac, has completado todo lo necesario del notebook. No tengo comentarios de corrección adicionales. Está aprobado.
    
    
Saludos!    

</div>

----


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score, classification_report
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.linear_model import LogisticRegression

```


```python
df = pd.read_csv("/datasets/users_behavior.csv")
```


```python
print(df.head())
```

       calls  minutes  messages   mb_used  is_ultra
    0   40.0   311.90      83.0  19915.42         0
    1   85.0   516.75      56.0  22696.96         0
    2   77.0   467.66      86.0  21060.45         0
    3  106.0   745.53      81.0   8437.39         1
    4   66.0   418.74       1.0  14502.75         0



```python
print(df.info())

print(df.describe())

print(df.isnull().sum())
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 3214 entries, 0 to 3213
    Data columns (total 5 columns):
     #   Column    Non-Null Count  Dtype  
    ---  ------    --------------  -----  
     0   calls     3214 non-null   float64
     1   minutes   3214 non-null   float64
     2   messages  3214 non-null   float64
     3   mb_used   3214 non-null   float64
     4   is_ultra  3214 non-null   int64  
    dtypes: float64(4), int64(1)
    memory usage: 125.7 KB
    None
                 calls      minutes     messages       mb_used     is_ultra
    count  3214.000000  3214.000000  3214.000000   3214.000000  3214.000000
    mean     63.038892   438.208787    38.281269  17207.673836     0.306472
    std      33.236368   234.569872    36.148326   7570.968246     0.461100
    min       0.000000     0.000000     0.000000      0.000000     0.000000
    25%      40.000000   274.575000     9.000000  12491.902500     0.000000
    50%      62.000000   430.600000    30.000000  16943.235000     0.000000
    75%      82.000000   571.927500    57.000000  21424.700000     1.000000
    max     244.000000  1632.060000   224.000000  49745.730000     1.000000
    calls       0
    minutes     0
    messages    0
    mb_used     0
    is_ultra    0
    dtype: int64


<div class="alert alert-block alert-success">
<b>Comentario de Revisor</b> <a class="tocSkip"></a>

Ok, al parecer la data está bastante completa.

</div>


```python
from sklearn.model_selection import train_test_split

X = df.drop(columns=['is_ultra'])
y = df['is_ultra']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

X_train, X_val, y_train, y_val = train_test_split(X_train, y_train, test_size=0.25, random_state=42)

print("Tamaño del conjunto de entrenamiento:", X_train.shape[0])
print("Tamaño del conjunto de validación:", X_val.shape[0])
print("Tamaño del conjunto de prueba:", X_test.shape[0])
```

    Tamaño del conjunto de entrenamiento: 1928
    Tamaño del conjunto de validación: 643
    Tamaño del conjunto de prueba: 643


<div class="alert alert-block alert-success">
<b>Comentario de Revisor</b> <a class="tocSkip"></a>

Correcto, muy bien con la separación de los datasets

</div>


```python

dt_model = DecisionTreeClassifier(random_state=42)

dt_model.fit(X_train, y_train)

y_val_pred_dt = dt_model.predict(X_val)

accuracy_dt = accuracy_score(y_val, y_val_pred_dt)

print("Árbol de Decisión - Exactitud en el conjunto de validación:", accuracy_dt)
print("\nReporte de clasificación en el conjunto de validación:")
print(classification_report(y_val, y_val_pred_dt))

```

    Árbol de Decisión - Exactitud en el conjunto de validación: 0.7309486780715396
    
    Reporte de clasificación en el conjunto de validación:
                  precision    recall  f1-score   support
    
               0       0.81      0.81      0.81       451
               1       0.55      0.54      0.55       192
    
        accuracy                           0.73       643
       macro avg       0.68      0.68      0.68       643
    weighted avg       0.73      0.73      0.73       643
    


### Resumen de los Hallazgos del Estudio

#### Árbol de Decisión

- **Exactitud en Validación:** 0.7309
- **Precisiones y Recalls:**
  - El modelo clasifica correctamente el 81% de los clientes en el plan Smart (Clase 0), pero solo el 55% de los clientes en el plan Ultra (Clase 1).
  - Recall de 81% para el plan Smart y 54% para el plan Ultra.
- **F1-Scores:**
  - F1-Score de 0.81 para el plan Smart y 0.55 para el plan Ultra.


<div class="alert alert-block alert-success">
<b>Comentario de Revisor</b> <a class="tocSkip"></a>

Ok, muy bien

</div>


```python
rf_model = RandomForestClassifier(random_state=42)

rf_model.fit(X_train, y_train)

y_val_pred_rf = rf_model.predict(X_val)

accuracy_rf = accuracy_score(y_val, y_val_pred_rf)

print("Bosque Aleatorio - Exactitud en el conjunto de validación:", accuracy_rf)
print("\nReporte de clasificación en el conjunto de validación:")
print(classification_report(y_val, y_val_pred_rf))

```

    Bosque Aleatorio - Exactitud en el conjunto de validación: 0.7947122861586314
    
    Reporte de clasificación en el conjunto de validación:
                  precision    recall  f1-score   support
    
               0       0.82      0.91      0.86       451
               1       0.71      0.52      0.60       192
    
        accuracy                           0.79       643
       macro avg       0.77      0.72      0.73       643
    weighted avg       0.79      0.79      0.78       643
    


### Resumen de los Hallazgos del Estudio

#### Bosque Aleatorio

- **Exactitud en Validación:** 0.7947
- **Precisiones y Recalls:**
  - El modelo clasifica correctamente el 82% de los clientes en el plan Smart (Clase 0) y el 71% de los clientes en el plan Ultra (Clase 1).
  - Recall de 91% para el plan Smart y 52% para el plan Ultra.
- **F1-Scores:**
  - F1-Score de 0.86 para el plan Smart y 0.60 para el plan Ultra.


<div class="alert alert-block alert-success">
<b>Comentario de Revisor</b> <a class="tocSkip"></a>

Bien con el entranemitno, nota que en general el desempeño es mejor

</div>


```python

lr_model = LogisticRegression(random_state=42)

lr_model.fit(X_train, y_train)

y_val_pred_lr = lr_model.predict(X_val)

accuracy_lr = accuracy_score(y_val, y_val_pred_lr)

print("Regresión Logística - Exactitud en el conjunto de validación:", accuracy_lr)
print("\nReporte de clasificación en el conjunto de validación:")
print(classification_report(y_val, y_val_pred_lr))

```

    Regresión Logística - Exactitud en el conjunto de validación: 0.7200622083981337
    
    Reporte de clasificación en el conjunto de validación:
                  precision    recall  f1-score   support
    
               0       0.72      0.97      0.83       451
               1       0.65      0.14      0.22       192
    
        accuracy                           0.72       643
       macro avg       0.69      0.55      0.53       643
    weighted avg       0.70      0.72      0.65       643
    


### Resumen de los Hallazgos del Estudio

#### Regresión Logística

- **Exactitud en Validación:** 0.7201
- **Precisiones y Recalls:**
  - El modelo clasifica correctamente el 72% de los clientes en el plan Smart (Clase 0) y el 65% de los clientes en el plan Ultra (Clase 1).
  - Recall de 97% para el plan Smart y 14% para el plan Ultra.
- **F1-Scores:**
  - F1-Score de 0.83 para el plan Smart y 0.22 para el plan Ultra.


<div class="alert alert-block alert-success">
<b>Comentario de Revisor</b> <a class="tocSkip"></a>

Muy bien!

</div>


```python

rf_model = RandomForestClassifier(random_state=42)

rf_model.fit(X_train, y_train)

y_test_pred_rf = rf_model.predict(X_test)

accuracy_test = accuracy_score(y_test, y_test_pred_rf)

print("Exactitud en el conjunto de prueba:", accuracy_test)
print("\nReporte de clasificación en el conjunto de prueba:")
print(classification_report(y_test, y_test_pred_rf))

```

    Exactitud en el conjunto de prueba: 0.8087091757387247
    
    Reporte de clasificación en el conjunto de prueba:
                  precision    recall  f1-score   support
    
               0       0.83      0.91      0.87       455
               1       0.73      0.55      0.63       188
    
        accuracy                           0.81       643
       macro avg       0.78      0.73      0.75       643
    weighted avg       0.80      0.81      0.80       643
    



```python
from sklearn.dummy import DummyClassifier


dummy_clf = DummyClassifier(strategy='most_frequent')
dummy_clf.fit(X_train, y_train)

y_test_pred_dummy = dummy_clf.predict(X_test)

accuracy_test_dummy = accuracy_score(y_test, y_test_pred_dummy)

print("Exactitud del modelo trivial en el conjunto de prueba:", accuracy_test_dummy)
print("\nReporte de clasificación del modelo trivial en el conjunto de prueba:")
print(classification_report(y_test, y_test_pred_dummy, zero_division=0))

print("\nExactitud del modelo de Bosque Aleatorio en el conjunto de prueba:", accuracy_test)
print("\nReporte de clasificación del modelo de Bosque Aleatorio en el conjunto de prueba:")
print(classification_report(y_test, y_test_pred_rf, zero_division=0))

```

    Exactitud del modelo trivial en el conjunto de prueba: 0.7076205287713841
    
    Reporte de clasificación del modelo trivial en el conjunto de prueba:
                  precision    recall  f1-score   support
    
               0       0.71      1.00      0.83       455
               1       0.00      0.00      0.00       188
    
        accuracy                           0.71       643
       macro avg       0.35      0.50      0.41       643
    weighted avg       0.50      0.71      0.59       643
    
    
    Exactitud del modelo de Bosque Aleatorio en el conjunto de prueba: 0.8087091757387247
    
    Reporte de clasificación del modelo de Bosque Aleatorio en el conjunto de prueba:
                  precision    recall  f1-score   support
    
               0       0.83      0.91      0.87       455
               1       0.73      0.55      0.63       188
    
        accuracy                           0.81       643
       macro avg       0.78      0.73      0.75       643
    weighted avg       0.80      0.81      0.80       643
    


<div class="alert alert-block alert-success">
<b>Comentario de Revisor v2</b> <a class="tocSkip"></a>

Muy bien, correcto!  

</div>

#### Comparación y Hallazgos
- El **modelo de Bosque Aleatorio** proporciona un rendimiento significativamente mejor en comparación con el **modelo trivial**.
- La mejora en la exactitud y las métricas de clasificación para ambas clases indica que el modelo de Bosque Aleatorio está capturando patrones útiles en los datos.
- **Conclusión Final:** El modelo de Bosque Aleatorio es efectivo para recomendar los planes Smart y Ultra basándose en el comportamiento de los clientes, superando claramente el rendimiento de un modelo trivial.

Estos resultados demuestran que utilizar modelos complejos como el Bosque Aleatorio puede proporcionar valor adicional al identificar correctamente los planes de los clientes en comparación con un enfoque trivial.

<div class="alert alert-block alert-success">
<b>Comentario de Revisor v2</b> <a class="tocSkip"></a>

OK, bien con las conclusiones
    

</div>

<div class="alert alert-block alert-danger">
<b>Comentario de Revisor</b> <a class="tocSkip"></a>

Ok, entiendo que este es el modelo final con el dataset de test, pero qué conclusiones obtienes de esto?

</div>

<div class="alert alert-block alert-danger">
<b>Comentario de Revisor</b> <a class="tocSkip"></a>

Por otro lado, te recomiendo realizar una prueba de cordura con un clasificador trivial

</div>
