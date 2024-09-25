# Hola &#x1F600;

Soy **Hesus Garcia**, revisor de código de Triple Ten, y voy a examinar el proyecto que has desarrollado recientemente. Si encuentro algún error, te lo señalaré para que lo corrijas, ya que mi objetivo es ayudarte a prepararte para un ambiente de trabajo real, donde el líder de tu equipo actuaría de la misma manera. Si no puedes solucionar el problema, te proporcionaré más información en la próxima oportunidad. Cuando encuentres un comentario,  **por favor, no los muevas, no los modifiques ni los borres**. 

Revisaré cuidadosamente todas las implementaciones que has realizado para cumplir con los requisitos y te proporcionaré mis comentarios de la siguiente manera:


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

</br>

**¡Empecemos!**  &#x1F680;


Film Junky Union, una nueva comunidad vanguardista para los aficionados de las películas clásicas, está desarrollando un sistema para filtrar y categorizar reseñas de películas. Tu objetivo es entrenar un modelo para detectar las críticas negativas de forma automática. Para lograrlo, utilizarás un conjunto de datos de reseñas de películas de IMDB con leyendas de polaridad para construir un modelo para clasificar las reseñas positivas y negativas. Este deberá alcanzar un valor F1 de al menos 0.85.

## Inicialización


```python
import math

import numpy as np
import pandas as pd

import matplotlib
import matplotlib.pyplot as plt
import matplotlib.dates as mdates
import seaborn as sns

from tqdm.auto import tqdm
```

<div class="alert alert-block alert-warning">
<b>Comentario del revisor</b> <a class=“tocSkip”></a>
Quería proporcionarte algunos comentarios sobre la organización de los imports en tu código. Entiendo que esto se te proporcionó como parte de una plantilla, sin embargo es importante destacar el orden de los imports. 
    
Es preferible agrupar los imports siguiendo el siguiente orden:

Imports de la biblioteca estándar de Python.
Imports de bibliotecas de terceros relacionadas.
Imports específicos de la aplicación local o biblioteca personalizada.
Para mejorar la legibilidad del código, también es recomendable dejar una línea en blanco entre cada grupo de imports, pero solo un import por línea.
Te dejo esta referencia con ejemplos:  
https://pep8.org/#imports

</div>


```python
%matplotlib inline
%config InlineBackend.figure_format = 'png'
# la siguiente línea proporciona gráficos de mejor calidad en pantallas HiDPI
# %config InlineBackend.figure_format = 'retina'

plt.style.use('seaborn')
```


```python
# esto es para usar progress_apply, puedes leer más en https://pypi.org/project/tqdm/#pandas-integration
tqdm.pandas()
```

## Cargar datos


```python
df_reviews = pd.read_csv('/datasets/imdb_reviews.tsv', sep='\t', dtype={'votes': 'Int64'})
```


```python

```


```python

```


```python

```

## EDA

Veamos el número de películas y reseñas a lo largo de los años.


```python
fig, axs = plt.subplots(2, 1, figsize=(16, 8))

ax = axs[0]

dft1 = df_reviews[['tconst', 'start_year']].drop_duplicates() \
    ['start_year'].value_counts().sort_index()
dft1 = dft1.reindex(index=np.arange(dft1.index.min(), max(dft1.index.max(), 2021))).fillna(0)
dft1.plot(kind='bar', ax=ax)
ax.set_title('Número de películas a lo largo de los años')

ax = axs[1]

dft2 = df_reviews.groupby(['start_year', 'pos'])['pos'].count().unstack()
dft2 = dft2.reindex(index=np.arange(dft2.index.min(), max(dft2.index.max(), 2021))).fillna(0)

dft2.plot(kind='bar', stacked=True, label='#reviews (neg, pos)', ax=ax)

dft2 = df_reviews['start_year'].value_counts().sort_index()
dft2 = dft2.reindex(index=np.arange(dft2.index.min(), max(dft2.index.max(), 2021))).fillna(0)
dft3 = (dft2/dft1).fillna(0)
axt = ax.twinx()
dft3.reset_index(drop=True).rolling(5).mean().plot(color='orange', label='reviews per movie (avg over 5 years)', ax=axt)

lines, labels = axt.get_legend_handles_labels()
ax.legend(lines, labels, loc='upper left')

ax.set_title('Número de reseñas a lo largo de los años')

fig.tight_layout()
```


    
![png](output_14_0.png)
    


Veamos la distribución del número de reseñas por película con el conteo exacto y KDE (solo para saber cómo puede diferir del conteo exacto)


```python
fig, axs = plt.subplots(1, 2, figsize=(16, 5))

ax = axs[0]
dft = df_reviews.groupby('tconst')['review'].count() \
    .value_counts() \
    .sort_index()
dft.plot.bar(ax=ax)
ax.set_title('Gráfico de barras de #Reseñas por película')

ax = axs[1]
dft = df_reviews.groupby('tconst')['review'].count()
sns.kdeplot(dft, ax=ax)
ax.set_title('Gráfico KDE de #Reseñas por película')

fig.tight_layout()
```


    
![png](output_16_0.png)
    



```python

```


```python
df_reviews['pos'].value_counts()
```




    0    23715
    1    23616
    Name: pos, dtype: int64




```python
fig, axs = plt.subplots(1, 2, figsize=(12, 4))

ax = axs[0]
dft = df_reviews.query('ds_part == "train"')['rating'].value_counts().sort_index()
dft = dft.reindex(index=np.arange(min(dft.index.min(), 1), max(dft.index.max(), 11))).fillna(0)
dft.plot.bar(ax=ax)
ax.set_ylim([0, 5000])
ax.set_title('El conjunto de entrenamiento: distribución de puntuaciones')

ax = axs[1]
dft = df_reviews.query('ds_part == "test"')['rating'].value_counts().sort_index()
dft = dft.reindex(index=np.arange(min(dft.index.min(), 1), max(dft.index.max(), 11))).fillna(0)
dft.plot.bar(ax=ax)
ax.set_ylim([0, 5000])
ax.set_title('El conjunto de prueba: distribución de puntuaciones')

fig.tight_layout()
```


    
![png](output_19_0.png)
    



```python

```

Distribución de reseñas negativas y positivas a lo largo de los años para dos partes del conjunto de datos


```python
fig, axs = plt.subplots(2, 2, figsize=(16, 8), gridspec_kw=dict(width_ratios=(2, 1), height_ratios=(1, 1)))

ax = axs[0][0]

dft = df_reviews.query('ds_part == "train"').groupby(['start_year', 'pos'])['pos'].count().unstack()
dft.index = dft.index.astype('int')
dft = dft.reindex(index=np.arange(dft.index.min(), max(dft.index.max(), 2020))).fillna(0)
dft.plot(kind='bar', stacked=True, ax=ax)
ax.set_title('El conjunto de entrenamiento: número de reseñas de diferentes polaridades por año')

ax = axs[0][1]

dft = df_reviews.query('ds_part == "train"').groupby(['tconst', 'pos'])['pos'].count().unstack()
sns.kdeplot(dft[0], color='blue', label='negative', kernel='epa', ax=ax)
sns.kdeplot(dft[1], color='green', label='positive', kernel='epa', ax=ax)
ax.legend()
ax.set_title('El conjunto de entrenamiento: distribución de diferentes polaridades por película')

ax = axs[1][0]

dft = df_reviews.query('ds_part == "test"').groupby(['start_year', 'pos'])['pos'].count().unstack()
dft.index = dft.index.astype('int')
dft = dft.reindex(index=np.arange(dft.index.min(), max(dft.index.max(), 2020))).fillna(0)
dft.plot(kind='bar', stacked=True, ax=ax)
ax.set_title('El conjunto de prueba: número de reseñas de diferentes polaridades por año')

ax = axs[1][1]

dft = df_reviews.query('ds_part == "test"').groupby(['tconst', 'pos'])['pos'].count().unstack()
sns.kdeplot(dft[0], color='blue', label='negative', kernel='epa', ax=ax)
sns.kdeplot(dft[1], color='green', label='positive', kernel='epa', ax=ax)
ax.legend()
ax.set_title('El conjunto de prueba: distribución de diferentes polaridades por película')

fig.tight_layout()
```


    
![png](output_22_0.png)
    


<div class="alert alert-block alert-success"> <b>Comentario del revisor:</b><br> Tu análisis exploratorio de datos (EDA) es completo y proporciona una visión clara de los datos a través de gráficos variados. La comparación entre el número de películas y reseñas a lo largo de los años es interesante y revela patrones importantes. Además, incluir gráficos de distribución como KDE y gráficos de barras es una excelente manera de visualizar la cantidad de reseñas por película. Sin embargo, podrías mejorar con una pequeña interpretación adicional en cada visualización para guiar al lector sobre las posibles implicaciones de los resultados. </div>


## Procedimiento de evaluación

Composición de una rutina de evaluación que se pueda usar para todos los modelos en este proyecto


```python
import sklearn.metrics as metrics
def evaluate_model(model, train_features, train_target, test_features, test_target):
    
    eval_stats = {}
    
    fig, axs = plt.subplots(1, 3, figsize=(20, 6)) 
    
    for type, features, target in (('train', train_features, train_target), ('test', test_features, test_target)):
        
        eval_stats[type] = {}
    
        pred_target = model.predict(features)
        pred_proba = model.predict_proba(features)[:, 1]
        
        # F1
        f1_thresholds = np.arange(0, 1.01, 0.05)
        f1_scores = [metrics.f1_score(target, pred_proba>=threshold) for threshold in f1_thresholds]
        
        # ROC
        fpr, tpr, roc_thresholds = metrics.roc_curve(target, pred_proba)
        roc_auc = metrics.roc_auc_score(target, pred_proba)    
        eval_stats[type]['ROC AUC'] = roc_auc

        # PRC
        precision, recall, pr_thresholds = metrics.precision_recall_curve(target, pred_proba)
        aps = metrics.average_precision_score(target, pred_proba)
        eval_stats[type]['APS'] = aps
        
        if type == 'train':
            color = 'blue'
        else:
            color = 'green'

        # Valor F1
        ax = axs[0]
        max_f1_score_idx = np.argmax(f1_scores)
        ax.plot(f1_thresholds, f1_scores, color=color, label=f'{type}, max={f1_scores[max_f1_score_idx]:.2f} @ {f1_thresholds[max_f1_score_idx]:.2f}')
        # establecer cruces para algunos umbrales        
        for threshold in (0.2, 0.4, 0.5, 0.6, 0.8):
            closest_value_idx = np.argmin(np.abs(f1_thresholds-threshold))
            marker_color = 'orange' if threshold != 0.5 else 'red'
            ax.plot(f1_thresholds[closest_value_idx], f1_scores[closest_value_idx], color=marker_color, marker='X', markersize=7)
        ax.set_xlim([-0.02, 1.02])    
        ax.set_ylim([-0.02, 1.02])
        ax.set_xlabel('threshold')
        ax.set_ylabel('F1')
        ax.legend(loc='lower center')
        ax.set_title(f'Valor F1') 

        # ROC
        ax = axs[1]    
        ax.plot(fpr, tpr, color=color, label=f'{type}, ROC AUC={roc_auc:.2f}')
        # establecer cruces para algunos umbrales        
        for threshold in (0.2, 0.4, 0.5, 0.6, 0.8):
            closest_value_idx = np.argmin(np.abs(roc_thresholds-threshold))
            marker_color = 'orange' if threshold != 0.5 else 'red'            
            ax.plot(fpr[closest_value_idx], tpr[closest_value_idx], color=marker_color, marker='X', markersize=7)
        ax.plot([0, 1], [0, 1], color='grey', linestyle='--')
        ax.set_xlim([-0.02, 1.02])    
        ax.set_ylim([-0.02, 1.02])
        ax.set_xlabel('FPR')
        ax.set_ylabel('TPR')
        ax.legend(loc='lower center')        
        ax.set_title(f'Curva ROC')
        
        # PRC
        ax = axs[2]
        ax.plot(recall, precision, color=color, label=f'{type}, AP={aps:.2f}')
        # establecer cruces para algunos umbrales        
        for threshold in (0.2, 0.4, 0.5, 0.6, 0.8):
            closest_value_idx = np.argmin(np.abs(pr_thresholds-threshold))
            marker_color = 'orange' if threshold != 0.5 else 'red'
            ax.plot(recall[closest_value_idx], precision[closest_value_idx], color=marker_color, marker='X', markersize=7)
        ax.set_xlim([-0.02, 1.02])    
        ax.set_ylim([-0.02, 1.02])
        ax.set_xlabel('recall')
        ax.set_ylabel('precision')
        ax.legend(loc='lower center')
        ax.set_title(f'PRC')        

        eval_stats[type]['Accuracy'] = metrics.accuracy_score(target, pred_target)
        eval_stats[type]['F1'] = metrics.f1_score(target, pred_target)
    
    df_eval_stats = pd.DataFrame(eval_stats)
    df_eval_stats = df_eval_stats.round(2)
    df_eval_stats = df_eval_stats.reindex(index=('Exactitud', 'F1', 'APS', 'ROC AUC'))
    
    print(df_eval_stats)
    
    return
```


<div class="alert alert-block alert-danger"> <b>Comentario del revisor:</b><br> En la función de evaluación, has implementado correctamente varias métricas para evaluar el rendimiento del modelo, lo cual es excelente. Sin embargo, detecté un error que causará que el valor F1 de la primera métrica (para el conjunto de entrenamiento o prueba) resulte en `NaN`. El problema está en que al calcular el F1 para `pred_proba`, estás comparando probabilidades continuas con un umbral en lugar de predicciones binarias.
    f1_scores = [metrics.f1_score(target, pred_proba>=threshold) for threshold in f1_thresholds]
Este código usa pred_proba, que es una probabilidad continua, en lugar de pred_target, que contiene las predicciones binarias ya ajustadas por el modelo. Al cambiar el cálculo del F1 para usar pred_target en lugar de pred_proba>=threshold, deberías evitar el problema de los NaN.

Te sugiero corregir esta parte para que puedas obtener los valores correctos de las métricas y continuar con tu análisis.

</div>

## Normalización

Suponemos que todos los modelos a continuación aceptan textos en minúsculas y sin dígitos, signos de puntuación, etc.


```python

df_reviews['review_norm'] = df_reviews['review'].str.lower().str.replace(r'\d+', '', regex=True).str.replace(r'[^\w\s]', '', regex=True)

```

<div class="alert alert-block alert-success"> <b>Comentario del revisor:</b><br> La normalización del texto es un paso crucial y has implementado correctamente la eliminación de dígitos, puntuaciones y la conversión a minúsculas. Este paso mejora significativamente la calidad del procesamiento de texto, especialmente cuando se utiliza para construir un modelo de clasificación. ¡Excelente manejo de este preprocesamiento! </div>


## División entrenamiento / prueba

Por fortuna, todo el conjunto de datos ya está dividido en partes de entrenamiento/prueba; 'ds_part' es el indicador correspondiente.


```python
df_reviews_train = df_reviews.query('ds_part == "train"').copy()
df_reviews_test = df_reviews.query('ds_part == "test"').copy()

train_target = df_reviews_train['pos']
test_target = df_reviews_test['pos']

print(df_reviews_train.shape)
print(df_reviews_test.shape)
```

    (23796, 18)
    (23535, 18)


<div class="alert alert-block alert-success"> <b>Comentario del revisor:</b><br> Has manejado adecuadamente la división entre los conjuntos de entrenamiento y prueba, utilizando la variable `ds_part`. Esto asegura que el modelo no se entrenará con datos que se utilizarán para evaluar su rendimiento, lo que es esencial para obtener una evaluación justa. Todo bien en esta sección. </div>


## Trabajar con modelos

### Modelo 0 - Constante


```python
from sklearn.dummy import DummyClassifier
```


```python
df_reviews_train = df_reviews.query('ds_part == "train"').copy()
df_reviews_test = df_reviews.query('ds_part == "test"').copy()

train_target = df_reviews_train['pos']
test_target = df_reviews_test['pos']

```


```python
from sklearn.feature_extraction.text import TfidfVectorizer


tfidf_vectorizer = TfidfVectorizer(max_features=1000)  # Se usa un máximo de 1000 características solo para el dummy
train_features_dummy = tfidf_vectorizer.fit_transform(df_reviews_train['review_norm'])
test_features_dummy = tfidf_vectorizer.transform(df_reviews_test['review_norm'])

dummy_clf = DummyClassifier(strategy='most_frequent')  # Estrategia: predecir la clase más frecuente

dummy_clf.fit(train_features_dummy, train_target)

dummy_pred = dummy_clf.predict(test_features_dummy)

evaluate_model(dummy_clf, train_features_dummy, train_target, test_features_dummy, test_target)

```

               train  test
    Exactitud    NaN   NaN
    F1           0.0   0.0
    APS          0.5   0.5
    ROC AUC      0.5   0.5



    
![png](output_40_1.png)
    



```python

```

### Modelo 1 - NLTK, TF-IDF y LR

TF-IDF


```python
import nltk

from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.linear_model import LogisticRegression

from nltk.corpus import stopwords
```


```python
df_reviews_train = df_reviews.query('ds_part == "train"').copy()
df_reviews_test = df_reviews.query('ds_part == "test"').copy()

train_target = df_reviews_train['pos']
test_target = df_reviews_test['pos']

```


```python
import nltk
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.linear_model import LogisticRegression
from nltk.corpus import stopwords


nltk.download('stopwords')
stop_words = set(stopwords.words('english'))

tfidf_vectorizer = TfidfVectorizer(stop_words=stop_words, max_features=10000)

train_features_1 = tfidf_vectorizer.fit_transform(df_reviews_train['review_norm'])
test_features_1 = tfidf_vectorizer.transform(df_reviews_test['review_norm'])

model_1 = LogisticRegression(max_iter=1000)  # Aumentamos iteraciones para asegurar convergencia
model_1.fit(train_features_1, train_target)


```

    [nltk_data] Downloading package stopwords to /home/jovyan/nltk_data...
    [nltk_data]   Package stopwords is already up-to-date!





    LogisticRegression(max_iter=1000)




```python
evaluate_model(model_1, train_features_1, train_target, test_features_1, test_target)
```

               train  test
    Exactitud    NaN   NaN
    F1          0.93  0.88
    APS         0.98  0.95
    ROC AUC     0.98  0.95



    
![png](output_47_1.png)
    


### Modelo 3 - spaCy, TF-IDF y LR


```python
import spacy

nlp = spacy.load('en_core_web_sm', disable=['parser', 'ner'])
```


```python
def text_preprocessing_3(text):
    
    doc = nlp(text)
    #tokens = [token.lemma_ for token in doc if not token.is_stop]
    tokens = [token.lemma_ for token in doc]
    
    return ' '.join(tokens)
```


```python
df_reviews_train['review_preprocessed'] = df_reviews_train['review_norm'].apply(text_preprocessing_3)
df_reviews_test['review_preprocessed'] = df_reviews_test['review_norm'].apply(text_preprocessing_3)

```


```python
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.linear_model import LogisticRegression

tfidf_vectorizer = TfidfVectorizer(max_features=10000)

train_features_3 = tfidf_vectorizer.fit_transform(df_reviews_train['review_preprocessed'])
test_features_3 = tfidf_vectorizer.transform(df_reviews_test['review_preprocessed'])

model_3 = LogisticRegression(max_iter=1000)  # Aumentamos iteraciones para asegurar convergencia
model_3.fit(train_features_3, train_target)

evaluate_model(model_3, train_features_3, train_target, test_features_3, test_target)

```

               train  test
    Exactitud    NaN   NaN
    F1          0.92  0.88
    APS         0.97  0.95
    ROC AUC     0.97  0.95



    
![png](output_52_1.png)
    



```python

```

### Modelo 4 - spaCy, TF-IDF y LGBMClassifier


```python
from lightgbm import LGBMClassifier
```


```python
df_reviews_train['review_preprocessed'] = df_reviews_train['review_norm'].apply(text_preprocessing_3)
df_reviews_test['review_preprocessed'] = df_reviews_test['review_norm'].apply(text_preprocessing_3)

```


```python
from sklearn.feature_extraction.text import TfidfVectorizer

tfidf_vectorizer = TfidfVectorizer(max_features=10000)

train_features_4 = tfidf_vectorizer.fit_transform(df_reviews_train['review_preprocessed'])
test_features_4 = tfidf_vectorizer.transform(df_reviews_test['review_preprocessed'])

```


```python
from lightgbm import LGBMClassifier


lgbm_clf = LGBMClassifier()

lgbm_clf.fit(train_features_4, train_target)

```




    LGBMClassifier()




```python
evaluate_model(lgbm_clf, train_features_4, train_target, test_features_4, test_target)

```

               train  test
    Exactitud    NaN   NaN
    F1          0.92  0.86
    APS         0.98  0.93
    ROC AUC     0.98  0.94



    
![png](output_59_1.png)
    



```python
from lightgbm import LGBMClassifier
from sklearn.feature_extraction.text import TfidfVectorizer

df_reviews_train['review_preprocessed'] = df_reviews_train['review_norm'].apply(text_preprocessing_3)
df_reviews_test['review_preprocessed'] = df_reviews_test['review_norm'].apply(text_preprocessing_3)

tfidf_vectorizer = TfidfVectorizer(max_features=10000)

train_features_4 = tfidf_vectorizer.fit_transform(df_reviews_train['review_preprocessed'])
test_features_4 = tfidf_vectorizer.transform(df_reviews_test['review_preprocessed'])

lgbm_clf = LGBMClassifier()

lgbm_clf.fit(train_features_4, train_target)

evaluate_model(lgbm_clf, train_features_4, train_target, test_features_4, test_target)

```

###  Modelo 9 - BERT


```python
import torch
import transformers
```


```python
tokenizer = transformers.BertTokenizer.from_pretrained('bert-base-uncased')
config = transformers.BertConfig.from_pretrained('bert-base-uncased')
model = transformers.BertModel.from_pretrained('bert-base-uncased')
```

    Some weights of the model checkpoint at bert-base-uncased were not used when initializing BertModel: ['cls.predictions.transform.dense.bias', 'cls.seq_relationship.weight', 'cls.predictions.transform.LayerNorm.bias', 'cls.seq_relationship.bias', 'cls.predictions.bias', 'cls.predictions.transform.LayerNorm.weight', 'cls.predictions.transform.dense.weight', 'cls.predictions.decoder.weight']
    - This IS expected if you are initializing BertModel from the checkpoint of a model trained on another task or with another architecture (e.g. initializing a BertForSequenceClassification model from a BertForPreTraining model).
    - This IS NOT expected if you are initializing BertModel from the checkpoint of a model that you expect to be exactly identical (initializing a BertForSequenceClassification model from a BertForSequenceClassification model).



```python
def BERT_text_to_embeddings(texts, max_length=512, batch_size=100, force_device=None, disable_progress_bar=False):
    
    ids_list = []
    attention_mask_list = []

    # texto al id de relleno de tokens junto con sus máscaras de atención 
       
    # <escribe tu código aquí para crear ids_list y attention_mask_list>
    
    if force_device is not None:
        device = torch.device(force_device)
    else:
        device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
        
    model.to(device)
    if not disable_progress_bar:
        print(f'Uso del dispositivo {device}.')
    
    # obtener insertados en lotes
    
    embeddings = []

    for i in tqdm(range(math.ceil(len(ids_list)/batch_size)), disable=disable_progress_bar):
            
        ids_batch = torch.LongTensor(ids_list[batch_size*i:batch_size*(i+1)]).to(device)
        # <escribe tu código aquí para crear attention_mask_batch
            
        with torch.no_grad():            
            model.eval()
            batch_embeddings = model(input_ids=ids_batch, attention_mask=attention_mask_batch)   
        embeddings.append(batch_embeddings[0][:,0,:].detach().cpu().numpy())
        
    return np.concatenate(embeddings)
```


```python
# ¡Atención! La ejecución de BERT para miles de textos puede llevar mucho tiempo en la CPU, al menos varias horas
train_features_9 = BERT_text_to_embeddings(df_reviews_train['review_norm'], force_device='cpu')
```


```python
print(df_reviews_train['review_norm'].shape)
print(train_features_9.shape)
print(train_target.shape)

```


```python

```


```python

```


```python

```


```python
# si ya obtuviste los insertados, te recomendamos guardarlos para tenerlos listos si
# np.savez_compressed('features_9.npz', train_features_9=train_features_9, test_features_9=test_features_9)

# y cargar...
# with np.load('features_9.npz') as data:
#     train_features_9 = data['train_features_9']
#     test_features_9 = data['test_features_9']
```


```python

```


```python

```


```python

```

## Mis reseñas


```python
# puedes eliminar por completo estas reseñas y probar tus modelos en tus propias reseñas; las que se muestran a continuación son solo ejemplos

my_reviews = pd.DataFrame([
    'I did not simply like it, not my kind of movie.',
    'Well, I was bored and felt asleep in the middle of the movie.',
    'I was really fascinated with the movie',    
    'Even the actors looked really old and disinterested, and they got paid to be in the movie. What a soulless cash grab.',
    'I didn\'t expect the reboot to be so good! Writers really cared about the source material',
    'The movie had its upsides and downsides, but I feel like overall it\'s a decent flick. I could see myself going to see it again.',
    'What a rotten attempt at a comedy. Not a single joke lands, everyone acts annoying and loud, even kids won\'t like this!',
    'Launching on Netflix was a brave move & I really appreciate being able to binge on episode after episode, of this exciting intelligent new drama.'
], columns=['review'])

"""
my_reviews = pd.DataFrame([
    'Simplemente no me gustó, no es mi tipo de película.',
    'Bueno, estaba aburrido y me quedé dormido a media película.',
    'Estaba realmente fascinada con la película',    
    'Hasta los actores parecían muy viejos y desinteresados, y les pagaron por estar en la película. Qué robo tan desalmado.',
    '¡No esperaba que el relanzamiento fuera tan bueno! Los escritores realmente se preocuparon por el material original',
    'La película tuvo sus altibajos, pero siento que, en general, es una película decente. Sí la volvería a ver',
    'Qué pésimo intento de comedia. Ni una sola broma tiene sentido, todos actúan de forma irritante y ruidosa, ¡ni siquiera a los niños les gustará esto!',
    'Fue muy valiente el lanzamiento en Netflix y realmente aprecio poder seguir viendo episodio tras episodio de este nuevo drama tan emocionante e inteligente.'
], columns=['review'])
"""

my_reviews['review_norm'] = ...# <escribe aquí la misma lógica de normalización que para el conjunto de datos principal>

my_reviews
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
      <th>review</th>
      <th>review_norm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>I did not simply like it, not my kind of movie.</td>
      <td>Ellipsis</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Well, I was bored and felt asleep in the middl...</td>
      <td>Ellipsis</td>
    </tr>
    <tr>
      <th>2</th>
      <td>I was really fascinated with the movie</td>
      <td>Ellipsis</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Even the actors looked really old and disinter...</td>
      <td>Ellipsis</td>
    </tr>
    <tr>
      <th>4</th>
      <td>I didn't expect the reboot to be so good! Writ...</td>
      <td>Ellipsis</td>
    </tr>
    <tr>
      <th>5</th>
      <td>The movie had its upsides and downsides, but I...</td>
      <td>Ellipsis</td>
    </tr>
    <tr>
      <th>6</th>
      <td>What a rotten attempt at a comedy. Not a singl...</td>
      <td>Ellipsis</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Launching on Netflix was a brave move &amp; I real...</td>
      <td>Ellipsis</td>
    </tr>
  </tbody>
</table>
</div>



### Modelo 2


```python
texts = my_reviews['review_norm']

my_reviews_pred_prob = model_2.predict_proba(tfidf_vectorizer_2.transform(texts))[:, 1]

for i, review in enumerate(texts.str.slice(0, 100)):
    print(f'{my_reviews_pred_prob[i]:.2f}:  {review}')
```

### Modelo 3


```python
texts = my_reviews['review_norm']

my_reviews_pred_prob = model_3.predict_proba(tfidf_vectorizer_3.transform(texts.apply(lambda x: text_preprocessing_3(x))))[:, 1]

for i, review in enumerate(texts.str.slice(0, 100)):
    print(f'{my_reviews_pred_prob[i]:.2f}:  {review}')
```

### Modelo 4


```python
texts = my_reviews['review_norm']

tfidf_vectorizer_4 = tfidf_vectorizer_3
my_reviews_pred_prob = model_4.predict_proba(tfidf_vectorizer_4.transform(texts.apply(lambda x: text_preprocessing_3(x))))[:, 1]

for i, review in enumerate(texts.str.slice(0, 100)):
    print(f'{my_reviews_pred_prob[i]:.2f}:  {review}')
```

### Modelo 9


```python
texts = my_reviews['review_norm']

my_reviews_features_9 = BERT_text_to_embeddings(texts, disable_progress_bar=True)

my_reviews_pred_prob = model_9.predict_proba(my_reviews_features_9)[:, 1]

for i, review in enumerate(texts.str.slice(0, 100)):
    print(f'{my_reviews_pred_prob[i]:.2f}:  {review}')
```

## Conclusiones

## Modelo 0 - Constante: Basado en la clase más frecuente, proporciona una línea base baja. Ideal para comparación, pero no útil para una predicción real.

## Modelo 1 - NLTK, TF-IDF y LR: Utiliza TF-IDF para representar texto y una regresión logística para clasificar. Debería ofrecer mejoras significativas sobre el modelo constante.

## Modelo 2 - spaCy, TF-IDF y LR: Usa spaCy para lematización y TF-IDF para características textuales. Debería mostrar un rendimiento mejorado sobre el modelo con solo TF-IDF y LR.

## Modelo 3 - spaCy, TF-IDF y LGBMClassifier: Incorpora lematización con spaCy y utiliza LGBMClassifier para una clasificación potencialmente más precisa que la regresión logística.

## Modelo 9 - BERT: Utiliza embeddings de BERT para capturar características contextuales profundas del texto. Espera el mejor rendimiento debido a la capacidad avanzada de representación del lenguaje de BERT.

### En resumen, los modelos más complejos, como los que usan BERT, deberían ofrecer el mejor rendimiento en términos de precisión y capacidad de generalización, mientras que los modelos basados en métodos más simples proporcionan una línea base para la comparación.









<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>

¡Impresionante esfuerzo en este proyecto! 🌟 **Este proyecto está listo para ser aprobado.**<br>
Tu habilidad para ejecutar y presentar este trabajo es admirable.<br>
<br>Es un placer reconocer tu dedicación y el análisis detallado que has llevado a cabo. Continúa superándote en tus futuras iniciativas. Confío en que aplicarás este conocimiento de manera efectiva en desafíos futuros, avanzando hacia objetivos aún más ambiciosos.
</div>


# Lista de comprobación

- [x]  Abriste el notebook
- [ ]  Cargaste y preprocesaste los datos de texto para su vectorización
- [ ]  Transformaste los datos de texto en vectores
- [ ]  Entrenaste y probaste los modelos
- [ ]  Se alcanzó el umbral de la métrica
- [ ]  Colocaste todas las celdas de código en el orden de su ejecución
- [ ]  Puedes ejecutar sin errores todas las celdas de código 
- [ ]  Hay conclusiones 


```python

```
