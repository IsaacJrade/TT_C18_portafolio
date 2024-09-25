# Hola Isaac!

Mi nombre es David Bautista, soy code reviewer de Tripleten y hoy tengo el gusto de revisar tu proyecto.

Cuando vea un error laa primera vez, lo señalaré. Deberás encontrarlo y arreglarlo. La intención es que te prepares para un espacio real de trabajo. En un trabajo, el líder de tu equipo hará lo mismo. Si no puedes solucionar el error, te daré más información en la próxima ocasión.

Encontrarás mis comentarios más abajo - por favor, no los muevas, no los modifiques ni los borres.

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
</div>

¡Empecemos!

# Déjame escuchar la música

# Contenido <a id='back'></a>

* [Introducción](#intro)
* [Etapa 1. Descripción de los datos](#data_review)
    * [Conclusiones](#data_review_conclusions)
* [Etapa 2. Preprocesamiento de datos](#data_preprocessing)
    * [2.1 Estilo del encabezado](#header_style)
    * [2.2 Valores ausentes](#missing_values)
    * [2.3 Duplicados](#duplicates)
    * [2.4 Conclusiones](#data_preprocessing_conclusions)
* [Etapa 3. Prueba de hipótesis](#hypothesis)
    * [3.1 Hipótesis 1: actividad de los usuarios y las usuarias en las dos ciudades](#activity)
* [Conclusiones](#end)

## Introducción <a id='intro'></a>
Como analista de datos, tu trabajo consiste en analizar datos para extraer información valiosa y tomar decisiones basadas en ellos. Esto implica diferentes etapas, como la descripción general de los datos, el preprocesamiento y la prueba de hipótesis.

Siempre que investigamos, necesitamos formular hipótesis que después podamos probar. A veces aceptamos estas hipótesis; otras veces, las rechazamos. Para tomar las decisiones correctas, una empresa debe ser capaz de entender si está haciendo las suposiciones correctas.

En este proyecto, compararás las preferencias musicales de las ciudades de Springfield y Shelbyville. Estudiarás datos reales de transmisión de música online para probar la hipótesis a continuación y comparar el comportamiento de los usuarios y las usuarias de estas dos ciudades.

### Objetivo:
Prueba la hipótesis:
1. La actividad de los usuarios y las usuarias difiere según el día de la semana y dependiendo de la ciudad.


### Etapas
Los datos del comportamiento del usuario se almacenan en el archivo `/datasets/music_project_en.csv`. No hay ninguna información sobre la calidad de los datos, así que necesitarás examinarlos antes de probar la hipótesis.

Primero, evaluarás la calidad de los datos y verás si los problemas son significativos. Entonces, durante el preprocesamiento de datos, tomarás en cuenta los problemas más críticos.

Tu proyecto consistirá en tres etapas:
 1. Descripción de los datos.
 2. Preprocesamiento de datos.
 3. Prueba de hipótesis.








[Volver a Contenidos](#back)

## Etapa 1. Descripción de los datos <a id='data_review'></a>

Abre los datos y examínalos.

Necesitarás `pandas`, así que impórtalo.


```python
import pandas as pd# Importar pandas

```

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Buen trabajo importando ``pandas``.</div>

Lee el archivo `music_project_en.csv` de la carpeta `/datasets/` y guárdalo en la variable `df`:


```python
df = pd.read_csv("/datasets/music_project_en.csv") # Leer el archivo y almacenarlo en df

```

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Buen trabajo cargando los datos necesarios para el desarrollo del proyecto. </div>

Muestra las 10 primeras filas de la tabla:


```python
print(df.head(10))# Obtener las 10 primeras filas de la tabla df

```

         userID                        Track            artist   genre  \
    0  FFB692EC            Kamigata To Boots  The Mass Missile    rock   
    1  55204538  Delayed Because of Accident  Andreas Rönnberg    rock   
    2    20EC38            Funiculì funiculà       Mario Lanza     pop   
    3  A3DD03C9        Dragons in the Sunset        Fire + Ice    folk   
    4  E2DC1FAE                  Soul People        Space Echo   dance   
    5  842029A1                       Chains          Obladaet  rusrap   
    6  4CB90AA5                         True      Roman Messer   dance   
    7  F03E1C1F             Feeling This Way   Polina Griffith   dance   
    8  8FA1D3BE                     L’estate       Julia Dalia  ruspop   
    9  E772D5C0                    Pessimist               NaN   dance   
    
            City        time        Day  
    0  Shelbyville  20:28:33  Wednesday  
    1  Springfield  14:07:09     Friday  
    2  Shelbyville  20:58:07  Wednesday  
    3  Shelbyville  08:37:09     Monday  
    4  Springfield  08:34:34     Monday  
    5  Shelbyville  13:09:41     Friday  
    6  Springfield  13:00:07  Wednesday  
    7  Springfield  20:47:49  Wednesday  
    8  Springfield  09:17:40     Friday  
    9  Shelbyville  21:20:49  Wednesday  


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Buen trabajo con el ``head()``, por otro lado, ten en cuenta que en notebooks de Jupyter se podría usar ``display()`` en vez de ``print()`` a la hora de mostrar las tablas para generar una salida mucho más estética.⁣</div>


Obtén la información general sobre la tabla con un comando. Conoces el método que muestra la información general que necesitamos.


```python
print(df.info())# Obtener la información general sobre nuestros datos

```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 65079 entries, 0 to 65078
    Data columns (total 7 columns):
     #   Column    Non-Null Count  Dtype 
    ---  ------    --------------  ----- 
     0     userID  65079 non-null  object
     1   Track     63736 non-null  object
     2   artist    57512 non-null  object
     3   genre     63881 non-null  object
     4     City    65079 non-null  object
     5   time      65079 non-null  object
     6   Day       65079 non-null  object
    dtypes: object(7)
    memory usage: 3.5+ MB
    None


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Buen trabajo Isaac, usas correctamente el método ``info()``.
⁣</div>


Estas son nuestras observaciones sobre la tabla. Contiene siete columnas. Almacenan los mismos tipos de datos: `object`.

Según la documentación:
- `' userID'`: identificador del usuario o la usuaria;
- `'Track'`: título de la canción;
- `'artist'`: nombre del artista;
- `'genre'`: género de la pista;
- `'City'`: ciudad del usuario o la usuaria;
- `'time'`: la hora exacta en la que se reprodujo la canción;
- `'Day'`: día de la semana.

Podemos ver tres problemas con el estilo en los encabezados de la tabla:
1. Algunos encabezados están en mayúsculas, otros en minúsculas.
2. Hay espacios en algunos encabezados.
3. `Detecta el tercer problema por tu cuenta y descríbelo aquí`.
hay espacios al principio de los encabezados de las columnas




### Escribe observaciones de tu parte. Estas son algunas de las preguntas que pueden ser útiles: <a id='data_review_conclusions'></a>

`1.   ¿Qué tipo de datos tenemos a nuestra disposición en las filas? ¿Y cómo podemos entender lo que almacenan las columnas?`
  userID'`: string
 `'Track'`: string
 `'artist'`: string
 `'genre'`: string
 `'City'`: string
 `'time'`: numero flotante
 `'Day'`: string
 
 podemos entender lo que almacenan analizando los datos por columna

`2.   ¿Hay suficientes datos para proporcionar respuestas a nuestra hipótesis o necesitamos más información?`
 si, tenemos tanto dias como horarios en los cuales los usuarios consumen el contenido. tambien tenemos su ciudad de origen
`3.   ¿Notaste algún problema en los datos, como valores ausentes, duplicados o tipos de datos incorrectos?`
 si, note valores ausentes en varios renglones.
 datos incorrectos, no estoy seguro como tomar "time" por que es un numero flotante pero no se si el formato que aparece se puede usar
 tambien note que hay problemas en el formato por que hay caracteres diferentes como Ã, ¬, ©, ¤, etc.
 tambien hay muchos conceptos en mayusculas
 


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Muy buen trabajo con las observaciones generadas Isaac.
⁣</div>


[Volver a Contenidos](#back)

## Etapa 2. Preprocesamiento de datos <a id='data_preprocessing'></a>

El objetivo aquí es preparar los datos para que sean analizados.
El primer paso es resolver cualquier problema con los encabezados. Luego podemos avanzar a los valores ausentes y duplicados. Empecemos.

Corrige el formato en los encabezados de la tabla.


### Estilo del encabezado <a id='header_style'></a>
Muestra los encabezados de la tabla (los nombres de las columnas):


```python
print(df.columns)# Muestra los nombres de las columnas

```

    Index(['  userID', 'Track', 'artist', 'genre', '  City  ', 'time', 'Day'], dtype='object')


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Buen trabajo mostrando los encabezados de la tabla.
⁣</div>


Cambia los encabezados de la tabla de acuerdo con las reglas del buen estilo:
* Todos los caracteres deben ser minúsculas.
* Elimina los espacios.
* Si el nombre tiene varias palabras, utiliza snake_case.

Anteriormente, aprendiste acerca de la forma automática de cambiar el nombre de las columnas. Vamos a aplicarla ahora. Utiliza el bucle for para iterar sobre los nombres de las columnas y poner todos los caracteres en minúsculas. Cuando hayas terminado, vuelve a mostrar los encabezados de la tabla:


```python
new_col_names = []

for old_name in df.columns:
    name_stripped = old_name.strip()
    name_lowered = name_stripped.lower()
    name_no_spaces = name_lowered.replace(' ', '_')
    new_col_names.append(name_no_spaces)

```

Ahora, utilizando el mismo método, elimina los espacios al principio y al final de los nombres de las columnas e imprime los nombres de las columnas nuevamente:


```python
df.columns = new_col_names

print(df.columns)# Bucle en los encabezados eliminando los espacios

```

    Index(['userid', 'track', 'artist', 'genre', 'city', 'time', 'day'], dtype='object')


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Perfecto, Isaac, solucionas varios problemas en un solo bucle, lo cual es óptimo. Muy buen trabajo. </div>

Necesitamos aplicar la regla de snake_case a la columna `userid`. Debe ser `user_id`. Cambia el nombre de esta columna y muestra los nombres de todas las columnas cuando hayas terminado.


```python
new_col_names = {
    "userid" : "user_id"
}
df.rename(columns = new_col_names, inplace = True)

```

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Buen trabajo aplicando el formatoa **snake_case** al encabezado ``user_id``. </div>

Comprueba el resultado. Muestra los encabezados una vez más:


```python
print(df.columns)# Comprobar el resultado: la lista de encabezados

```

    Index(['user_id', 'track', 'artist', 'genre', 'city', 'time', 'day'], dtype='object')


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Muy buen trabajo en la sección de la moficiación de los encabezados. </div>

[Volver a Contenidos](#back)

### Valores ausentes <a id='missing_values'></a>
 Primero, encuentra el número de valores ausentes en la tabla. Debes utilizar dos métodos en una secuencia para obtener el número de valores ausentes.


```python
print(df.isna().sum())# Calcular el número de valores ausentes

```

    user_id       0
    track      1343
    artist     7567
    genre      1198
    city          0
    time          0
    day           0
    dtype: int64


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Buen trabajo mostranado la cantidad de valores nulos de cada una de las columnas.⁣</div>

No todos los valores ausentes afectan a la investigación. Por ejemplo, los valores ausentes en `track` y `artist` no son cruciales. Simplemente puedes reemplazarlos con valores predeterminados como el string `'unknown'` (desconocido).

Pero los valores ausentes en `'genre'` pueden afectar la comparación entre las preferencias musicales de Springfield y Shelbyville. En la vida real, sería útil saber las razones por las cuales hay datos ausentes e intentar recuperarlos. Pero no tenemos esa oportunidad en este proyecto. Así que tendrás que:
* rellenar estos valores ausentes con un valor predeterminado;
* evaluar cuánto podrían afectar los valores ausentes a tus cómputos;

Reemplazar los valores ausentes en las columnas `'track'`, `'artist'` y `'genre'` con el string `'unknown'`. Como mostramos anteriormente en las lecciones, la mejor forma de hacerlo es crear una lista que almacene los nombres de las columnas donde se necesita el reemplazo. Luego, utiliza esta lista e itera sobre las columnas donde se necesita el reemplazo haciendo el propio reemplazo.


```python
columns_to_replace = ['track', 'artist' , 'genre']

for col in columns_to_replace:
    df[col].fillna('unknown', inplace=True)

```

Ahora comprueba el resultado para asegurarte de que después del reemplazo no haya valores ausentes en el conjunto de datos. Para hacer esto, cuenta los valores ausentes nuevamente.


```python
print(df.isna().sum())# Contar valores ausentes

```

    user_id    0
    track      0
    artist     0
    genre      0
    city       0
    time       0
    day        0
    dtype: int64


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Perfecto, buen trabajo solucionando el problema de los valores nulos dentro de la tabla.⁣</div>

[Volver a Contenidos](#back)

### Duplicados <a id='duplicates'></a>
Encuentra el número de duplicados explícitos en la tabla. Una vez más, debes aplicar dos métodos en una secuencia para obtener la cantidad de duplicados explícitos.


```python
print(df.duplicated().sum())# Contar duplicados explícitos

```

    3826


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Buen trabajo identificando la cantidad de registros duplicados dentro de la tabla.</div>

Ahora, elimina todos los duplicados. Para ello, llama al método que hace exactamente esto.


```python
df.drop_duplicates(inplace=True)# Eliminar duplicados explícitos

```

Comprobemos ahora si eliminamos con éxito todos los duplicados. Cuenta los duplicados explícitos una vez más para asegurarte de haberlos eliminado todos:


```python
print(df.duplicated().sum()) # Comprobar de nuevo si hay duplicados


```

    0


<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Muy bien, Isaac, lidias de buena manera con el problema de los valores duplicados explícitos dentro de la tabla. Ahora bien, para la próxima puedes tener en cuenta que al eliminar valores duplicados explícitos dentro de la tabla, pueden generarse problemas en el orden del índice de la tabla. Puedes usar el método ``reset_index()`` para reiniciar el índice de la tabla. Te mostraré un ejemplo:
    
```python
df = df.drop_duplicates().reset_index(drop=True)
    
```
</div>

Ahora queremos deshacernos de los duplicados implícitos en la columna `genre`. Por ejemplo, el nombre de un género se puede escribir de varias formas. Dichos errores también pueden afectar al resultado.

Para hacerlo, primero mostremos una lista de nombres de género únicos, ordenados en orden alfabético. Para ello:
* Extrae la columna `genre` del DataFrame.
* Llama al método que devolverá todos los valores únicos en la columna extraída.



```python
# Inspeccionar los nombres de géneros únicos
u_genres = df["genre"].unique()
u_genres.sort()

# Mostrar la lista de géneros únicos
print(u_genres)
```

    ['acid' 'acoustic' 'action' 'adult' 'africa' 'afrikaans' 'alternative'
     'ambient' 'americana' 'animated' 'anime' 'arabesk' 'arabic' 'arena'
     'argentinetango' 'art' 'audiobook' 'avantgarde' 'axé' 'baile' 'balkan'
     'beats' 'bigroom' 'black' 'bluegrass' 'blues' 'bollywood' 'bossa'
     'brazilian' 'breakbeat' 'breaks' 'broadway' 'cantautori' 'cantopop'
     'canzone' 'caribbean' 'caucasian' 'celtic' 'chamber' 'children' 'chill'
     'chinese' 'choral' 'christian' 'christmas' 'classical' 'classicmetal'
     'club' 'colombian' 'comedy' 'conjazz' 'contemporary' 'country' 'cuban'
     'dance' 'dancehall' 'dancepop' 'dark' 'death' 'deep' 'deutschrock'
     'deutschspr' 'dirty' 'disco' 'dnb' 'documentary' 'downbeat' 'downtempo'
     'drum' 'dub' 'dubstep' 'eastern' 'easy' 'electronic' 'electropop' 'emo'
     'entehno' 'epicmetal' 'estrada' 'ethnic' 'eurofolk' 'european'
     'experimental' 'extrememetal' 'fado' 'film' 'fitness' 'flamenco' 'folk'
     'folklore' 'folkmetal' 'folkrock' 'folktronica' 'forró' 'frankreich'
     'französisch' 'french' 'funk' 'future' 'gangsta' 'garage' 'german'
     'ghazal' 'gitarre' 'glitch' 'gospel' 'gothic' 'grime' 'grunge' 'gypsy'
     'handsup' "hard'n'heavy" 'hardcore' 'hardstyle' 'hardtechno' 'hip'
     'hip-hop' 'hiphop' 'historisch' 'holiday' 'hop' 'horror' 'house' 'idm'
     'independent' 'indian' 'indie' 'indipop' 'industrial' 'inspirational'
     'instrumental' 'international' 'irish' 'jam' 'japanese' 'jazz' 'jewish'
     'jpop' 'jungle' 'k-pop' 'karadeniz' 'karaoke' 'kayokyoku' 'korean'
     'laiko' 'latin' 'latino' 'leftfield' 'local' 'lounge' 'loungeelectronic'
     'lovers' 'malaysian' 'mandopop' 'marschmusik' 'meditative'
     'mediterranean' 'melodic' 'metal' 'metalcore' 'mexican' 'middle'
     'minimal' 'miscellaneous' 'modern' 'mood' 'mpb' 'muslim' 'native'
     'neoklassik' 'neue' 'new' 'newage' 'newwave' 'nu' 'nujazz' 'numetal'
     'oceania' 'old' 'opera' 'orchestral' 'other' 'piano' 'pop'
     'popelectronic' 'popeurodance' 'post' 'posthardcore' 'postrock' 'power'
     'progmetal' 'progressive' 'psychedelic' 'punjabi' 'punk' 'quebecois'
     'ragga' 'ram' 'rancheras' 'rap' 'rave' 'reggae' 'reggaeton' 'regional'
     'relax' 'religious' 'retro' 'rhythm' 'rnb' 'rnr' 'rock' 'rockabilly'
     'romance' 'roots' 'ruspop' 'rusrap' 'rusrock' 'salsa' 'samba' 'schlager'
     'self' 'sertanejo' 'shoegazing' 'showtunes' 'singer' 'ska' 'slow'
     'smooth' 'soul' 'soulful' 'sound' 'soundtrack' 'southern' 'specialty'
     'speech' 'spiritual' 'sport' 'stonerrock' 'surf' 'swing' 'synthpop'
     'sängerportrait' 'tango' 'tanzorchester' 'taraftar' 'tech' 'techno'
     'thrash' 'top' 'traditional' 'tradjazz' 'trance' 'tribal' 'trip'
     'triphop' 'tropical' 'türk' 'türkçe' 'unknown' 'urban' 'uzbek' 'variété'
     'vi' 'videogame' 'vocal' 'western' 'world' 'worldbeat' 'ïîï']


<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
~~Recuerda que el ideal es poder mostrar los valores únicos de la columna pero de formar ordenada alfabéticamente.~~</div>

<div class="alert alert-block alert-success">
<b>Comentario del revisor #2</b> <a class="tocSkip"></a>
    
Buen trabajo Isaac.</div>


Busca en la lista para encontrar duplicados implícitos del género `hiphop`. Estos pueden ser nombres escritos incorrectamente o nombres alternativos para el mismo género.

Verás los siguientes duplicados implícitos:
* `hip`
* `hop`
* `hip-hop`

Para deshacerte de ellos, crea una función llamada `replace_wrong_genres()` con dos parámetros:
* `wrong_genres=`: esta es una lista que contiene todos los valores que necesitas reemplazar.
* `correct_genre=`: este es un string que vas a utilizar como reemplazo.

Como resultado, la función debería corregir los nombres en la columna `'genre'` de la tabla `df`, es decir, remplazar cada valor de la lista `wrong_genres` por el valor en `correct_genre`.

Dentro del cuerpo de la función, utiliza un bucle `'for'` para iterar sobre la lista de géneros incorrectos, extrae la columna `'genre'` y aplica el método `replace` para hacer correcciones.


```python
def replace_wrong_genres(df, wrong_genres, correct_genre):
    df['genre'].replace(wrong_genres, correct_genre, inplace=True)
```

Ahora, llama a `replace_wrong_genres()` y pásale tales argumentos para que retire los duplicados implícitos (`hip`, `hop` y `hip-hop`) y los reemplace por `hiphop`:


```python
replace_wrong_genres(df, ["hip", "hop" , "hip-hop"], "hiphop")# Eliminar duplicados implícitos

```

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Buen trabajo aplicando la función para solucionar el problema de los valores duplicados implicitos dentro de la columna.</div>


Asegúrate de que los nombres duplicados han sido eliminados. Muestra la lista de valores únicos de la columna `'genre'` una vez más:


```python
u_genres = df["genre"].unique()
u_genres.sort()
print(u_genres)# Comprobación de duplicados implícitos

```

    ['acid' 'acoustic' 'action' 'adult' 'africa' 'afrikaans' 'alternative'
     'ambient' 'americana' 'animated' 'anime' 'arabesk' 'arabic' 'arena'
     'argentinetango' 'art' 'audiobook' 'avantgarde' 'axé' 'baile' 'balkan'
     'beats' 'bigroom' 'black' 'bluegrass' 'blues' 'bollywood' 'bossa'
     'brazilian' 'breakbeat' 'breaks' 'broadway' 'cantautori' 'cantopop'
     'canzone' 'caribbean' 'caucasian' 'celtic' 'chamber' 'children' 'chill'
     'chinese' 'choral' 'christian' 'christmas' 'classical' 'classicmetal'
     'club' 'colombian' 'comedy' 'conjazz' 'contemporary' 'country' 'cuban'
     'dance' 'dancehall' 'dancepop' 'dark' 'death' 'deep' 'deutschrock'
     'deutschspr' 'dirty' 'disco' 'dnb' 'documentary' 'downbeat' 'downtempo'
     'drum' 'dub' 'dubstep' 'eastern' 'easy' 'electronic' 'electropop' 'emo'
     'entehno' 'epicmetal' 'estrada' 'ethnic' 'eurofolk' 'european'
     'experimental' 'extrememetal' 'fado' 'film' 'fitness' 'flamenco' 'folk'
     'folklore' 'folkmetal' 'folkrock' 'folktronica' 'forró' 'frankreich'
     'französisch' 'french' 'funk' 'future' 'gangsta' 'garage' 'german'
     'ghazal' 'gitarre' 'glitch' 'gospel' 'gothic' 'grime' 'grunge' 'gypsy'
     'handsup' "hard'n'heavy" 'hardcore' 'hardstyle' 'hardtechno' 'hiphop'
     'historisch' 'holiday' 'horror' 'house' 'idm' 'independent' 'indian'
     'indie' 'indipop' 'industrial' 'inspirational' 'instrumental'
     'international' 'irish' 'jam' 'japanese' 'jazz' 'jewish' 'jpop' 'jungle'
     'k-pop' 'karadeniz' 'karaoke' 'kayokyoku' 'korean' 'laiko' 'latin'
     'latino' 'leftfield' 'local' 'lounge' 'loungeelectronic' 'lovers'
     'malaysian' 'mandopop' 'marschmusik' 'meditative' 'mediterranean'
     'melodic' 'metal' 'metalcore' 'mexican' 'middle' 'minimal'
     'miscellaneous' 'modern' 'mood' 'mpb' 'muslim' 'native' 'neoklassik'
     'neue' 'new' 'newage' 'newwave' 'nu' 'nujazz' 'numetal' 'oceania' 'old'
     'opera' 'orchestral' 'other' 'piano' 'pop' 'popelectronic' 'popeurodance'
     'post' 'posthardcore' 'postrock' 'power' 'progmetal' 'progressive'
     'psychedelic' 'punjabi' 'punk' 'quebecois' 'ragga' 'ram' 'rancheras'
     'rap' 'rave' 'reggae' 'reggaeton' 'regional' 'relax' 'religious' 'retro'
     'rhythm' 'rnb' 'rnr' 'rock' 'rockabilly' 'romance' 'roots' 'ruspop'
     'rusrap' 'rusrock' 'salsa' 'samba' 'schlager' 'self' 'sertanejo'
     'shoegazing' 'showtunes' 'singer' 'ska' 'slow' 'smooth' 'soul' 'soulful'
     'sound' 'soundtrack' 'southern' 'specialty' 'speech' 'spiritual' 'sport'
     'stonerrock' 'surf' 'swing' 'synthpop' 'sängerportrait' 'tango'
     'tanzorchester' 'taraftar' 'tech' 'techno' 'thrash' 'top' 'traditional'
     'tradjazz' 'trance' 'tribal' 'trip' 'triphop' 'tropical' 'türk' 'türkçe'
     'unknown' 'urban' 'uzbek' 'variété' 'vi' 'videogame' 'vocal' 'western'
     'world' 'worldbeat' 'ïîï']


<div class="alert alert-block alert-danger">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
~~Nuevamente, recuerda que el ideal es poder mostrar los valores únicos de la columna pero de formar ordenada alfabéticamente.~~</div>


<div class="alert alert-block alert-success">
<b>Comentario del revisor #2</b> <a class="tocSkip"></a>
    
Perfecto, buen trabajo.</div>


[Volver a Contenidos](#back)

### Tus observaciones <a id='data_preprocessing_conclusions'></a>

`Describe brevemente lo que has notado al analizar duplicados, cómo abordaste sus eliminaciones y qué resultados obtuviste.`

corregimos encabezados de columna. usando snake_case, minusculas y elimando espacios
valores ausentes. para track y artist se reemplazaron con unknown
duplicados explicitos. se quitaron con drpo_duplicates
duplicados implicitos. se reemplazaron de hiphop para estandarizar en un solo nombre

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Buen trabajo con las observaciones generdas. </div>


[Volver a Contenidos](#back)

## Etapa 3. Prueba de hipótesis <a id='hypothesis'></a>

### Hipótesis: comparar el comportamiento del usuario o la usuaria en las dos ciudades <a id='activity'></a>

La hipótesis afirma que existen diferencias en la forma en que los usuarios y las usuarias de Springfield y Shelbyville consumen música. Para comprobar esto, usa los datos de tres días de la semana: lunes, miércoles y viernes.

* Agrupa a los usuarios y las usuarias por ciudad.
* Compara el número de canciones que cada grupo reprodujo el lunes, el miércoles y el viernes.


Realiza cada cálculo por separado.

El primer paso es evaluar la actividad del usuario en cada ciudad. Recuerda las etapas dividir-aplicar-combinar de las que hablamos anteriormente en la lección. Tu objetivo ahora es agrupar los datos por ciudad, aplicar el método apropiado para contar durante la etapa de aplicación y luego encontrar la cantidad de canciones reproducidas en cada grupo especificando la columna para obtener el recuento.

A continuación se muestra un ejemplo de cómo debería verse el resultado final:
`df.groupby(by='....')['column'].method()`Realiza cada cálculo por separado.

Para evaluar la actividad de los usuarios y las usuarias en cada ciudad, agrupa los datos por ciudad y encuentra la cantidad de canciones reproducidas en cada grupo.




```python
city_song = df.groupby(by='city')['track'].count()# Contar las canciones reproducidas en cada ciudad
print(city_song)
```

    city
    Shelbyville    18512
    Springfield    42741
    Name: track, dtype: int64


`Comenta tus observaciones aquí` en Springfield se consume mas del doble que en Shelbyville

Ahora agrupemos los datos por día de la semana y encontremos el número de canciones reproducidas el lunes, miércoles y viernes. Utiliza el mismo método que antes, pero ahora necesitamos una agrupación diferente.



```python
songs_day = df.groupby("day")["track"].count()
print(songs_day)# Calcular las canciones reproducidas en cada uno de los tres días

```

    day
    Friday       21840
    Monday       21354
    Wednesday    18059
    Name: track, dtype: int64


`Comenta tus observaciones aquí` el viernes es el que tiene mayor cantidad seguido del lunes y miercoles. me llama la atencion que no tenemos datos de martes, jueves, sabado y domingo

<div class="alert alert-block alert-success">
<b>Comentario del revisor</b> <a class="tocSkip"></a>
    
Perfecto, Isaac. La estructura que usas para aplicar los ``groupby()`` y obtener la tabla con la información correcta es la ideal; por otro lado, tus comentarios son coherentes con la realidad que nos muestran los datos. 

Ya sabes cómo contar entradas agrupándolas por ciudad o día. Ahora necesitas escribir una función que pueda contar entradas según ambos criterios simultáneamente.

Crea la función `number_tracks()` para calcular el número de canciones reproducidas en un determinado día **y** ciudad. La función debe aceptar dos parámetros:

- `day`: un día de la semana para filtrar. Por ejemplo, `'Monday'` (lunes).
- `city`: una ciudad para filtrar. Por ejemplo, `'Springfield'`.

Dentro de la función, aplicarás un filtrado consecutivo con indexación lógica.

Primero filtra los datos por día y luego filtra la tabla resultante por ciudad.

Después de filtrar los datos por dos criterios, cuenta el número de valores de la columna 'user_id' en la tabla resultante. Este recuento representa el número de entradas que estás buscando. Guarda el resultado en una nueva variable y devuélvelo desde la función.


```python
def number_tracks(day, city):# Declara la función number_tracks() con dos parámetros: day= y city=.

    by_day = df[df['day'] == day]# Almacena las filas del DataFrame donde el valor en la columna 'day' es igual al parámetro day=

    by_city = by_day[by_day['city'] == city]# Filtra las filas donde el valor en la columna 'city' es igual al parámetro city=

    count = by_city['user_id'].count()# Extrae la columna 'user_id' de la tabla filtrada y aplica el método count()

    return count# Devolve el número de valores de la columna 'user_id'
```

Llama a `number_tracks()` seis veces, cambiando los valores de los parámetros para que recuperes los datos de ambas ciudades para cada uno de los tres días.


```python
springfield_monday = number_tracks('Monday', 'Springfield')
print(springfield_monday)# El número de canciones reproducidas en Springfield el lunes

```

    15740



```python
shelbyville_monday = number_tracks('Monday', 'Shelbyville')
print(shelbyville_monday)# El número de canciones reproducidas en Shelbyville el lunes

```

    5614



```python
springfield_wednesday = number_tracks('Wednesday', 'Springfield')
print(springfield_wednesday)# El número de canciones reproducidas en Springfield el miércoles

```

    11056



```python
shelbyville_wednesday = number_tracks('Wednesday', 'Shelbyville')
print(shelbyville_wednesday)# El número de canciones reproducidas en Shelbyville el miércoles

```

    7003



```python
springfield_friday = number_tracks('Friday', 'Springfield')
print(springfield_friday)# El número de canciones reproducidas en Springfield el viernes

```

    15945



```python
shelbyville_friday = number_tracks('Friday', 'Shelbyville')
print(shelbyville_friday)# El número de canciones reproducidas en Shelbyville el viernes

```

    5895


**Conclusiones**

`Comenta si la hipótesis es correcta o se debe rechazar. Explica tu razonamiento.`

Observaciones:

Springfield tiene más consumo de musica que Shelbyville.
Los viernes son los días con mayor consumo en las 2 ciudades.


La hipótesis que  dice que La actividad de los usuarios y las usuarias difiere según el día de la semana y dependiendo de la ciudad, creo que es correcta nos pudimos dar cuenta que hay una ciudad que tiene mas consumo que otra y hay un dia para las 2 ciudades(viernes) que es la de mayor consumo. esos datos son valiosos para el analisis de la empresa 






<div class="alert alert-block alert-success">
<b>Comentario del revisor </b> <a class="tocSkip"></a>
    
La función está cumpliendo su objetivo de buena manera, sin embargo te puedo sugerir anidar las condiciones que se dan a modo de filtro, esto con el fin de optimizar el código de una mejor manera. A continuación te mostraré como lo puedes hacer para que los apliques en tu código.
    
```python
def number_tracks(day,city):
    df_filter = df[(df['day']==day) & (df['city'] == city)]
    df_filter_count = df_filter['user_id'].count()
    return df_filter_count
    
```
    
Recuerda que tu función está funcionando correctamente, mi comentario solo es con ánimo de que explores formas de optimizar aún más tu código.


</div>

[Volver a Contenidos](#back)

# Conclusiones <a id='end'></a>

`Resume aquí tus conclusiones sobre la hipótesis.`

La hipótesis que  dice que La actividad de los usuarios y las usuarias difiere según el día de la semana y dependiendo de la ciudad, la veo correcta. Después de analizar los datos, tengo la siguientes conclusiones:

Consumo Musical:

Springfield tiene mayor consumo en comparación con Shelbyville total.
Los viernes son los días con mayor actividad para las 2 ciudades.


Diferencias:

La cantidad de canciones es consistente en los tres días (lunes, miércoles y viernes), nos damos cuenta cual de los 3 dias es el mayor y cual es el menor para las 2 ciudades 

Comentarios:

tenemos que considerar los factores diferentes de cada ciudad como el tamaño de la póblacion, el poder adquisitivo, la preferencias, etc. Las conclusiones que tenemos son solo de los numeros recibidos y se puede profundizar con mas informacion  



<div class="alert alert-block alert-success">
<b>Comentario del revisor </b> <a class="tocSkip"></a>
    
Muy buen trabajo con las conclusiones generales del proyecto.

</div>

### Nota
En proyectos de investigación reales, la prueba de hipótesis estadística es más precisa y cuantitativa. También ten en cuenta que no siempre se pueden sacar conclusiones sobre una ciudad entera a partir de datos de una sola fuente.

Aprenderás más sobre la prueba de hipótesis en el sprint de análisis estadístico de datos.

<div class="alert alert-block alert-danger">
<b>Comentario del revisor </b> <a class="tocSkip"></a>
    
# Comentario General
    
~~Hola Isaac, te felicito por el desarollo del proyecto hasta el momento. Ahora bien, he dejado algunos comentarios para que los puedas tener en cuenta par ala proxima revisión.~~
</div>

<div class="alert alert-block alert-success">
<b>Comentario del revisor </b> <a class="tocSkip"></a>
    
# Comentario General #2
    
Hola, Isaac, te felicito por la culminación del proyecto. Realizaste un muy buen trabajo.
</div>


[Volver a Contenidos](#back)
