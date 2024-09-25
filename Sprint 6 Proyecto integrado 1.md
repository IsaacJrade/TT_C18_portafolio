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


```python
import pandas as pd



```


```python
file_path = "/datasets/games.csv"

df = pd.read_csv(file_path)

df.head()
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
      <th>Name</th>
      <th>Platform</th>
      <th>Year_of_Release</th>
      <th>Genre</th>
      <th>NA_sales</th>
      <th>EU_sales</th>
      <th>JP_sales</th>
      <th>Other_sales</th>
      <th>Critic_Score</th>
      <th>User_Score</th>
      <th>Rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Wii Sports</td>
      <td>Wii</td>
      <td>2006.0</td>
      <td>Sports</td>
      <td>41.36</td>
      <td>28.96</td>
      <td>3.77</td>
      <td>8.45</td>
      <td>76.0</td>
      <td>8</td>
      <td>E</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Super Mario Bros.</td>
      <td>NES</td>
      <td>1985.0</td>
      <td>Platform</td>
      <td>29.08</td>
      <td>3.58</td>
      <td>6.81</td>
      <td>0.77</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mario Kart Wii</td>
      <td>Wii</td>
      <td>2008.0</td>
      <td>Racing</td>
      <td>15.68</td>
      <td>12.76</td>
      <td>3.79</td>
      <td>3.29</td>
      <td>82.0</td>
      <td>8.3</td>
      <td>E</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Wii Sports Resort</td>
      <td>Wii</td>
      <td>2009.0</td>
      <td>Sports</td>
      <td>15.61</td>
      <td>10.93</td>
      <td>3.28</td>
      <td>2.95</td>
      <td>80.0</td>
      <td>8</td>
      <td>E</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pokemon Red/Pokemon Blue</td>
      <td>GB</td>
      <td>1996.0</td>
      <td>Role-Playing</td>
      <td>11.27</td>
      <td>8.89</td>
      <td>10.22</td>
      <td>1.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



<div class="alert alert-block alert-warning">
<b>Comentario revisor</b> <a class="tocSkip"></a>


Te recomiendo que como buena práctica separes la carga de las librerías y la carga de las bases de datos. 
</div>


```python
df.columns = df.columns.str.lower()


df.head()
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
      <th>name</th>
      <th>platform</th>
      <th>year_of_release</th>
      <th>genre</th>
      <th>na_sales</th>
      <th>eu_sales</th>
      <th>jp_sales</th>
      <th>other_sales</th>
      <th>critic_score</th>
      <th>user_score</th>
      <th>rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Wii Sports</td>
      <td>Wii</td>
      <td>2006.0</td>
      <td>Sports</td>
      <td>41.36</td>
      <td>28.96</td>
      <td>3.77</td>
      <td>8.45</td>
      <td>76.0</td>
      <td>8</td>
      <td>E</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Super Mario Bros.</td>
      <td>NES</td>
      <td>1985.0</td>
      <td>Platform</td>
      <td>29.08</td>
      <td>3.58</td>
      <td>6.81</td>
      <td>0.77</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mario Kart Wii</td>
      <td>Wii</td>
      <td>2008.0</td>
      <td>Racing</td>
      <td>15.68</td>
      <td>12.76</td>
      <td>3.79</td>
      <td>3.29</td>
      <td>82.0</td>
      <td>8.3</td>
      <td>E</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Wii Sports Resort</td>
      <td>Wii</td>
      <td>2009.0</td>
      <td>Sports</td>
      <td>15.61</td>
      <td>10.93</td>
      <td>3.28</td>
      <td>2.95</td>
      <td>80.0</td>
      <td>8</td>
      <td>E</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pokemon Red/Pokemon Blue</td>
      <td>GB</td>
      <td>1996.0</td>
      <td>Role-Playing</td>
      <td>11.27</td>
      <td>8.89</td>
      <td>10.22</td>
      <td>1.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['na_sales'] = pd.to_numeric(df['na_sales'], errors='coerce')
df['eu_sales'] = pd.to_numeric(df['eu_sales'], errors='coerce')
df['jp_sales'] = pd.to_numeric(df['jp_sales'], errors='coerce')
df['other_sales'] = pd.to_numeric(df['other_sales'], errors='coerce')

df['rating'] = df['rating'].astype(str)

df.dtypes

df.sample(20)
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
      <th>name</th>
      <th>platform</th>
      <th>year_of_release</th>
      <th>genre</th>
      <th>na_sales</th>
      <th>eu_sales</th>
      <th>jp_sales</th>
      <th>other_sales</th>
      <th>critic_score</th>
      <th>user_score</th>
      <th>rating</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7447</th>
      <td>de Blob 2</td>
      <td>PS3</td>
      <td>2011.0</td>
      <td>Platform</td>
      <td>0.11</td>
      <td>0.07</td>
      <td>0.00</td>
      <td>0.03</td>
      <td>74.0</td>
      <td>7.1</td>
      <td>E10+</td>
    </tr>
    <tr>
      <th>10706</th>
      <td>Nihon Keizai Shinbunsha Kanshuu: Shiranai Mama...</td>
      <td>DS</td>
      <td>2009.0</td>
      <td>Misc</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.10</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>13789</th>
      <td>Company of Heroes: Opposing Fronts</td>
      <td>PC</td>
      <td>2007.0</td>
      <td>Strategy</td>
      <td>0.01</td>
      <td>0.03</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>87.0</td>
      <td>8.6</td>
      <td>M</td>
    </tr>
    <tr>
      <th>12249</th>
      <td>Penguins of Madagascar</td>
      <td>3DS</td>
      <td>2014.0</td>
      <td>Action</td>
      <td>0.00</td>
      <td>0.06</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>51.0</td>
      <td>tbd</td>
      <td>E</td>
    </tr>
    <tr>
      <th>7599</th>
      <td>The Chronicles of Narnia: The Lion, The Witch ...</td>
      <td>XB</td>
      <td>2005.0</td>
      <td>Action</td>
      <td>0.15</td>
      <td>0.04</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>72.0</td>
      <td>6</td>
      <td>T</td>
    </tr>
    <tr>
      <th>13548</th>
      <td>Shaun the Sheep</td>
      <td>DS</td>
      <td>2008.0</td>
      <td>Adventure</td>
      <td>0.04</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>58.0</td>
      <td>tbd</td>
      <td>E</td>
    </tr>
    <tr>
      <th>2315</th>
      <td>Skylanders: Trap Team</td>
      <td>X360</td>
      <td>2014.0</td>
      <td>Action</td>
      <td>0.54</td>
      <td>0.27</td>
      <td>0.00</td>
      <td>0.08</td>
      <td>NaN</td>
      <td>tbd</td>
      <td>E10+</td>
    </tr>
    <tr>
      <th>7901</th>
      <td>Tamagotchi Party On!</td>
      <td>Wii</td>
      <td>2006.0</td>
      <td>Misc</td>
      <td>0.12</td>
      <td>0.00</td>
      <td>0.06</td>
      <td>0.01</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>11093</th>
      <td>Space Invaders Extreme</td>
      <td>PSP</td>
      <td>2008.0</td>
      <td>Shooter</td>
      <td>0.06</td>
      <td>0.01</td>
      <td>0.01</td>
      <td>0.01</td>
      <td>84.0</td>
      <td>6.8</td>
      <td>E</td>
    </tr>
    <tr>
      <th>12805</th>
      <td>Dino Pets</td>
      <td>DS</td>
      <td>2009.0</td>
      <td>Simulation</td>
      <td>0.05</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>tbd</td>
      <td>E</td>
    </tr>
    <tr>
      <th>7047</th>
      <td>The Italian Job</td>
      <td>PS2</td>
      <td>2003.0</td>
      <td>Racing</td>
      <td>0.11</td>
      <td>0.09</td>
      <td>0.00</td>
      <td>0.03</td>
      <td>55.0</td>
      <td>6.3</td>
      <td>T</td>
    </tr>
    <tr>
      <th>9218</th>
      <td>Bejeweled 3</td>
      <td>X360</td>
      <td>NaN</td>
      <td>Puzzle</td>
      <td>0.13</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>78.0</td>
      <td>8.4</td>
      <td>E</td>
    </tr>
    <tr>
      <th>15294</th>
      <td>Azada</td>
      <td>3DS</td>
      <td>2012.0</td>
      <td>Puzzle</td>
      <td>0.00</td>
      <td>0.02</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>tbd</td>
      <td>E</td>
    </tr>
    <tr>
      <th>16082</th>
      <td>Chameleon: To Dye For!</td>
      <td>DS</td>
      <td>2006.0</td>
      <td>Puzzle</td>
      <td>0.01</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>2269</th>
      <td>Nickelodeon Fit</td>
      <td>Wii</td>
      <td>2010.0</td>
      <td>Sports</td>
      <td>0.76</td>
      <td>0.09</td>
      <td>0.00</td>
      <td>0.06</td>
      <td>NaN</td>
      <td>tbd</td>
      <td>E</td>
    </tr>
    <tr>
      <th>8399</th>
      <td>Tokimeki Memorial: Private Collection</td>
      <td>PS</td>
      <td>1996.0</td>
      <td>Misc</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.16</td>
      <td>0.01</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>753</th>
      <td>ATV Offroad Fury 2</td>
      <td>PS2</td>
      <td>2002.0</td>
      <td>Racing</td>
      <td>1.92</td>
      <td>0.20</td>
      <td>0.00</td>
      <td>0.06</td>
      <td>82.0</td>
      <td>8.9</td>
      <td>E</td>
    </tr>
    <tr>
      <th>11131</th>
      <td>NFL Blitz 20-02</td>
      <td>GC</td>
      <td>2002.0</td>
      <td>Sports</td>
      <td>0.07</td>
      <td>0.02</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>77.0</td>
      <td>tbd</td>
      <td>E</td>
    </tr>
    <tr>
      <th>10718</th>
      <td>Higurashi no Nakukoru ni Kizuna: Dai-Ni-Kan - Sou</td>
      <td>DS</td>
      <td>2008.0</td>
      <td>Adventure</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.10</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
    </tr>
    <tr>
      <th>6815</th>
      <td>Burnout 2: Point of Impact</td>
      <td>XB</td>
      <td>2003.0</td>
      <td>Racing</td>
      <td>0.18</td>
      <td>0.05</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>88.0</td>
      <td>5.1</td>
      <td>E</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Cambios realizados en los tipos de datos:
# - 'year_of_release': Convertido a tipo entero (Int64) para análisis temporal.
# - 'na_sales', 'eu_sales', 'jp_sales', 'other_sales': Convertidos a tipo flotante (float64) para análisis de ventas.
# - 'user_score': Convertido a tipo flotante (float64) para manejar 'tbd' como NaN.
# - 'rating': Convertido a tipo cadena (object) para facilitar el manejo de la clasificación de edad.
```


```python
df['user_score'] = df['user_score'].replace('tbd', pd.NA)
df['user_score'] = pd.to_numeric(df['user_score'], errors='coerce')

df['critic_score'] = pd.to_numeric(df['critic_score'], errors='coerce')
df['na_sales'] = pd.to_numeric(df['na_sales'], errors='coerce')
df['eu_sales'] = pd.to_numeric(df['eu_sales'], errors='coerce')
df['jp_sales'] = pd.to_numeric(df['jp_sales'], errors='coerce')
df['other_sales'] = pd.to_numeric(df['other_sales'], errors='coerce')


df['critic_score'] = df['critic_score'].fillna('Unknown')

df.sample(20)
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
      <th>name</th>
      <th>platform</th>
      <th>year_of_release</th>
      <th>genre</th>
      <th>na_sales</th>
      <th>eu_sales</th>
      <th>jp_sales</th>
      <th>other_sales</th>
      <th>critic_score</th>
      <th>user_score</th>
      <th>rating</th>
      <th>total_sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>16478</th>
      <td>Cartoon Network Battle Crashers</td>
      <td>3DS</td>
      <td>2016.0</td>
      <td>Action</td>
      <td>0.01</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>E10+</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>12863</th>
      <td>7 Days to Die</td>
      <td>XOne</td>
      <td>2016.0</td>
      <td>Action</td>
      <td>0.03</td>
      <td>0.02</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>35.0</td>
      <td>5.2</td>
      <td>M</td>
      <td>0.05</td>
    </tr>
    <tr>
      <th>877</th>
      <td>NBA Street Vol. 2</td>
      <td>PS2</td>
      <td>2003.0</td>
      <td>Sports</td>
      <td>1.69</td>
      <td>0.20</td>
      <td>0.00</td>
      <td>0.06</td>
      <td>90.0</td>
      <td>8.8</td>
      <td>E</td>
      <td>1.95</td>
    </tr>
    <tr>
      <th>4622</th>
      <td>Metro: Last Light</td>
      <td>PS3</td>
      <td>2013.0</td>
      <td>Action</td>
      <td>0.14</td>
      <td>0.18</td>
      <td>0.03</td>
      <td>0.07</td>
      <td>80.0</td>
      <td>8.2</td>
      <td>nan</td>
      <td>0.42</td>
    </tr>
    <tr>
      <th>11144</th>
      <td>Viewtiful Joe: Red Hot Rumble</td>
      <td>PSP</td>
      <td>2006.0</td>
      <td>Action</td>
      <td>0.08</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>63.0</td>
      <td>6.3</td>
      <td>T</td>
      <td>0.09</td>
    </tr>
    <tr>
      <th>5843</th>
      <td>Lizzie McGuire 3: Homecoming Havoc</td>
      <td>GBA</td>
      <td>2005.0</td>
      <td>Platform</td>
      <td>0.22</td>
      <td>0.08</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>59.0</td>
      <td>NaN</td>
      <td>E</td>
      <td>0.31</td>
    </tr>
    <tr>
      <th>3524</th>
      <td>FIFA World Cup Germany 2006</td>
      <td>PS2</td>
      <td>2006.0</td>
      <td>Sports</td>
      <td>0.47</td>
      <td>0.02</td>
      <td>0.00</td>
      <td>0.08</td>
      <td>77.0</td>
      <td>8.1</td>
      <td>E</td>
      <td>0.57</td>
    </tr>
    <tr>
      <th>10047</th>
      <td>Animal Genius</td>
      <td>DS</td>
      <td>2007.0</td>
      <td>Puzzle</td>
      <td>0.10</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>E</td>
      <td>0.11</td>
    </tr>
    <tr>
      <th>6057</th>
      <td>Final Fantasy X-2: International + Last Mission</td>
      <td>PS2</td>
      <td>2004.0</td>
      <td>Role-Playing</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.29</td>
      <td>0.00</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>nan</td>
      <td>0.29</td>
    </tr>
    <tr>
      <th>1682</th>
      <td>Ganbare Goemon! Karakuri Douchuu</td>
      <td>NES</td>
      <td>1986.0</td>
      <td>Platform</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>1.20</td>
      <td>0.00</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>nan</td>
      <td>1.20</td>
    </tr>
    <tr>
      <th>10370</th>
      <td>Fight Club</td>
      <td>XB</td>
      <td>2004.0</td>
      <td>Fighting</td>
      <td>0.08</td>
      <td>0.02</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>37.0</td>
      <td>4.7</td>
      <td>M</td>
      <td>0.10</td>
    </tr>
    <tr>
      <th>7915</th>
      <td>Tom Clancy's Splinter Cell: Blacklist</td>
      <td>PC</td>
      <td>2013.0</td>
      <td>Action</td>
      <td>0.04</td>
      <td>0.13</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>82.0</td>
      <td>7.4</td>
      <td>M</td>
      <td>0.18</td>
    </tr>
    <tr>
      <th>7884</th>
      <td>Big Air</td>
      <td>PS</td>
      <td>1999.0</td>
      <td>Sports</td>
      <td>0.10</td>
      <td>0.07</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>nan</td>
      <td>0.18</td>
    </tr>
    <tr>
      <th>7481</th>
      <td>Gallop Racer 2003: A New Breed</td>
      <td>PS2</td>
      <td>2002.0</td>
      <td>Sports</td>
      <td>0.04</td>
      <td>0.03</td>
      <td>0.12</td>
      <td>0.01</td>
      <td>68.0</td>
      <td>8.5</td>
      <td>E</td>
      <td>0.20</td>
    </tr>
    <tr>
      <th>9315</th>
      <td>Your Shape: Fitness Evolved 2013</td>
      <td>WiiU</td>
      <td>2012.0</td>
      <td>Action</td>
      <td>0.06</td>
      <td>0.07</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>76.0</td>
      <td>6.3</td>
      <td>E10+</td>
      <td>0.14</td>
    </tr>
    <tr>
      <th>12258</th>
      <td>Worms Forts: Under Siege</td>
      <td>XB</td>
      <td>2004.0</td>
      <td>Strategy</td>
      <td>0.05</td>
      <td>0.01</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>67.0</td>
      <td>8.0</td>
      <td>T</td>
      <td>0.06</td>
    </tr>
    <tr>
      <th>14735</th>
      <td>Wrestle Angels: Survivor 2</td>
      <td>PS2</td>
      <td>2008.0</td>
      <td>Fighting</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.03</td>
      <td>0.00</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>nan</td>
      <td>0.03</td>
    </tr>
    <tr>
      <th>8385</th>
      <td>Disney Golf</td>
      <td>PS2</td>
      <td>2002.0</td>
      <td>Sports</td>
      <td>0.07</td>
      <td>0.06</td>
      <td>0.02</td>
      <td>0.02</td>
      <td>72.0</td>
      <td>8.3</td>
      <td>E</td>
      <td>0.17</td>
    </tr>
    <tr>
      <th>2211</th>
      <td>The Sims 2</td>
      <td>DS</td>
      <td>2005.0</td>
      <td>Simulation</td>
      <td>0.81</td>
      <td>0.05</td>
      <td>0.00</td>
      <td>0.07</td>
      <td>70.0</td>
      <td>6.1</td>
      <td>E10+</td>
      <td>0.93</td>
    </tr>
    <tr>
      <th>12480</th>
      <td>Speed</td>
      <td>Wii</td>
      <td>2010.0</td>
      <td>Racing</td>
      <td>0.04</td>
      <td>0.02</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>Unknown</td>
      <td>NaN</td>
      <td>E</td>
      <td>0.07</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Tratamiento de valores ausentes y abreviatura TBD:

# - Los valores ausentes en las columnas de puntuaciones y ventas se han dejado como NaN en lugar de ser rellenados. Esta decisión se tomó para evitar distorsiones en el análisis de datos posteriores.

# - Los valores 'TBD' en la columna de puntuaciones de usuarios se han convertido a NaN para indicar que la información está faltante.

# - Los valores ausentes en las columnas de puntuaciones y ventas se han dejado como NaN. 

# Esta estrategia de manejo de valores ausentes se ha hizo para garantizar la integridad y la calidad de los datos.
```


```python
df['total_sales'] = df['na_sales'] + df['eu_sales'] + df['jp_sales'] + df['other_sales']


df.head()
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
      <th>name</th>
      <th>platform</th>
      <th>year_of_release</th>
      <th>genre</th>
      <th>na_sales</th>
      <th>eu_sales</th>
      <th>jp_sales</th>
      <th>other_sales</th>
      <th>critic_score</th>
      <th>user_score</th>
      <th>rating</th>
      <th>total_sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Wii Sports</td>
      <td>Wii</td>
      <td>2006.0</td>
      <td>Sports</td>
      <td>41.36</td>
      <td>28.96</td>
      <td>3.77</td>
      <td>8.45</td>
      <td>76.0</td>
      <td>8.0</td>
      <td>E</td>
      <td>82.54</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Super Mario Bros.</td>
      <td>NES</td>
      <td>1985.0</td>
      <td>Platform</td>
      <td>29.08</td>
      <td>3.58</td>
      <td>6.81</td>
      <td>0.77</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>40.24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mario Kart Wii</td>
      <td>Wii</td>
      <td>2008.0</td>
      <td>Racing</td>
      <td>15.68</td>
      <td>12.76</td>
      <td>3.79</td>
      <td>3.29</td>
      <td>82.0</td>
      <td>8.3</td>
      <td>E</td>
      <td>35.52</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Wii Sports Resort</td>
      <td>Wii</td>
      <td>2009.0</td>
      <td>Sports</td>
      <td>15.61</td>
      <td>10.93</td>
      <td>3.28</td>
      <td>2.95</td>
      <td>80.0</td>
      <td>8.0</td>
      <td>E</td>
      <td>32.77</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pokemon Red/Pokemon Blue</td>
      <td>GB</td>
      <td>1996.0</td>
      <td>Role-Playing</td>
      <td>11.27</td>
      <td>8.89</td>
      <td>10.22</td>
      <td>1.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>31.38</td>
    </tr>
  </tbody>
</table>
</div>



<div class="alert alert-block alert-success">
<b>Comentario del revisor:</b> <a class="tocSkip"></a>
    
Hola, Isacc! Muy buen trabajo en la sección, ajustaste los nombres de las columnas a minúsculas con el uso de la función str.lower(), cambiaste el tipo de variable de dos de las variables de la base de datos, consideraste ajustar los valores ausentes de las variables identificadas de score y muy buen trabajo con la suma de todas las ventas. 
    
   

</div>

<div class="alert alert-block alert-warning">
<b>Comentario del revisor:</b> <a class="tocSkip"></a>
    

    
Solamente te recomiendo que en estas columnas de 'critic_score'  mejor los completes con 'Unknown', puede ser en una columna duplicada para que puedas desarrollar los análisis posteriores. Además, te sugiero verificar si en el resto de las columnas no cuentas con datos ausentes que se deban ajustar.     

</div>


```python
missing_data = df.isnull().sum()
missing_data
```




    name                  2
    platform              0
    year_of_release     269
    genre                 2
    na_sales              0
    eu_sales              0
    jp_sales              0
    other_sales           0
    critic_score       8578
    user_score         9125
    rating                0
    total_sales           0
    dtype: int64




```python
games_per_year = df['year_of_release'].value_counts().sort_index()

games_per_year
```




    1980.0       9
    1981.0      46
    1982.0      36
    1983.0      17
    1984.0      14
    1985.0      14
    1986.0      21
    1987.0      16
    1988.0      15
    1989.0      17
    1990.0      16
    1991.0      41
    1992.0      43
    1993.0      62
    1994.0     121
    1995.0     219
    1996.0     263
    1997.0     289
    1998.0     379
    1999.0     338
    2000.0     350
    2001.0     482
    2002.0     829
    2003.0     775
    2004.0     762
    2005.0     939
    2006.0    1006
    2007.0    1197
    2008.0    1427
    2009.0    1426
    2010.0    1255
    2011.0    1136
    2012.0     653
    2013.0     544
    2014.0     581
    2015.0     606
    2016.0     502
    Name: year_of_release, dtype: int64




```python
# Observamos una tendencia creciente en el número de juegos lanzados desde la década de 1990 hasta alrededor de 2008, seguido de una disminución en los años posteriores. Sin embargo, todavía hay una cantidad considerable de juegos lanzados en los años más recientes.
```


```python
platform_total_sales = df.groupby('platform')['total_sales'].sum()
platform_total_sales = platform_total_sales.sort_values(ascending=False)
top_platforms = platform_total_sales.head(5)
top_platforms
```




    platform
    PS2     1255.77
    X360     971.42
    PS3      939.65
    Wii      907.51
    DS       806.12
    Name: total_sales, dtype: float64




```python
top_platforms_data = df[df['platform'].isin(top_platforms.index)]
platform_yearly_sales = top_platforms_data.groupby(['platform', 'year_of_release'])['total_sales'].sum().unstack()
platform_yearly_sales
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
      <th>year_of_release</th>
      <th>1985.0</th>
      <th>2000.0</th>
      <th>2001.0</th>
      <th>2002.0</th>
      <th>2003.0</th>
      <th>2004.0</th>
      <th>2005.0</th>
      <th>2006.0</th>
      <th>2007.0</th>
      <th>2008.0</th>
      <th>2009.0</th>
      <th>2010.0</th>
      <th>2011.0</th>
      <th>2012.0</th>
      <th>2013.0</th>
      <th>2014.0</th>
      <th>2015.0</th>
      <th>2016.0</th>
    </tr>
    <tr>
      <th>platform</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
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
      <th>DS</th>
      <td>0.02</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>17.27</td>
      <td>130.14</td>
      <td>119.81</td>
      <td>146.94</td>
      <td>145.31</td>
      <td>119.54</td>
      <td>85.02</td>
      <td>26.18</td>
      <td>11.01</td>
      <td>1.54</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>PS2</th>
      <td>NaN</td>
      <td>39.17</td>
      <td>166.43</td>
      <td>205.38</td>
      <td>184.31</td>
      <td>211.81</td>
      <td>160.66</td>
      <td>103.42</td>
      <td>75.99</td>
      <td>53.90</td>
      <td>26.40</td>
      <td>5.64</td>
      <td>0.45</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>PS3</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>20.96</td>
      <td>73.19</td>
      <td>118.52</td>
      <td>130.93</td>
      <td>142.17</td>
      <td>156.78</td>
      <td>107.36</td>
      <td>113.25</td>
      <td>47.76</td>
      <td>16.82</td>
      <td>3.60</td>
    </tr>
    <tr>
      <th>Wii</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>137.15</td>
      <td>152.77</td>
      <td>171.32</td>
      <td>206.97</td>
      <td>127.95</td>
      <td>59.65</td>
      <td>21.71</td>
      <td>8.59</td>
      <td>3.75</td>
      <td>1.14</td>
      <td>0.18</td>
    </tr>
    <tr>
      <th>X360</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.25</td>
      <td>51.62</td>
      <td>95.41</td>
      <td>135.26</td>
      <td>120.29</td>
      <td>170.03</td>
      <td>143.84</td>
      <td>99.74</td>
      <td>88.58</td>
      <td>34.74</td>
      <td>11.96</td>
      <td>1.52</td>
    </tr>
  </tbody>
</table>
</div>




```python
obsolete_platforms = df.groupby('platform')['total_sales'].sum()
obsolete_platforms = obsolete_platforms[obsolete_platforms == 0].index.tolist()

latest_release_years = df[df['platform'].isin(obsolete_platforms)].groupby('platform')['year_of_release'].max()
disappearance_time = 2016 - latest_release_years

earliest_release_years = df[~df['platform'].isin(obsolete_platforms)].groupby('platform')['year_of_release'].min()
appearance_time = 2016 - earliest_release_years


disappearance_time, appearance_time
```




    (Series([], Name: year_of_release, dtype: float64),
     platform
     2600    36.0
     3DO     22.0
     3DS      5.0
     DC      18.0
     DS      31.0
     GB      28.0
     GBA     16.0
     GC      15.0
     GEN     26.0
     GG      24.0
     N64     20.0
     NES     33.0
     NG      23.0
     PC      31.0
     PCFX    20.0
     PS      22.0
     PS2     16.0
     PS3     10.0
     PS4      3.0
     PSP     12.0
     PSV      5.0
     SAT     22.0
     SCD     23.0
     SNES    26.0
     TG16    21.0
     WS      17.0
     Wii     10.0
     WiiU     4.0
     X360    11.0
     XB      16.0
     XOne     3.0
     Name: year_of_release, dtype: float64)




```python
# Nuevas plataformas: El tiempo promedio que tardan las nuevas plataformas en aparecer es de aproximadamente 10 años. 
# Antiguas plataformas: El tiempo promedio que tardan las antiguas plataformas en desaparecer es de aproximadamente 19 años.  que las antiguas plataformas tienden a desaparecer aproximadamente cada 19 años.
```


```python
data_2010_2016 = df[df['year_of_release'].between(2010, 2016)]
data_2010_2016.head()
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
      <th>name</th>
      <th>platform</th>
      <th>year_of_release</th>
      <th>genre</th>
      <th>na_sales</th>
      <th>eu_sales</th>
      <th>jp_sales</th>
      <th>other_sales</th>
      <th>critic_score</th>
      <th>user_score</th>
      <th>rating</th>
      <th>total_sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>14</th>
      <td>Kinect Adventures!</td>
      <td>X360</td>
      <td>2010.0</td>
      <td>Misc</td>
      <td>15.00</td>
      <td>4.89</td>
      <td>0.24</td>
      <td>1.69</td>
      <td>61.0</td>
      <td>6.3</td>
      <td>E</td>
      <td>21.82</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Grand Theft Auto V</td>
      <td>PS3</td>
      <td>2013.0</td>
      <td>Action</td>
      <td>7.02</td>
      <td>9.09</td>
      <td>0.98</td>
      <td>3.96</td>
      <td>97.0</td>
      <td>8.2</td>
      <td>M</td>
      <td>21.05</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Grand Theft Auto V</td>
      <td>X360</td>
      <td>2013.0</td>
      <td>Action</td>
      <td>9.66</td>
      <td>5.14</td>
      <td>0.06</td>
      <td>1.41</td>
      <td>97.0</td>
      <td>8.1</td>
      <td>M</td>
      <td>16.27</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Pokemon Black/Pokemon White</td>
      <td>DS</td>
      <td>2010.0</td>
      <td>Role-Playing</td>
      <td>5.51</td>
      <td>3.17</td>
      <td>5.65</td>
      <td>0.80</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>15.13</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Call of Duty: Modern Warfare 3</td>
      <td>X360</td>
      <td>2011.0</td>
      <td>Shooter</td>
      <td>9.04</td>
      <td>4.24</td>
      <td>0.13</td>
      <td>1.32</td>
      <td>88.0</td>
      <td>3.4</td>
      <td>M</td>
      <td>14.73</td>
    </tr>
  </tbody>
</table>
</div>




```python
sales_per_year_platform = data_2010_2016.groupby(['year_of_release', 'platform'])['total_sales'].sum()
sales_per_year_platform.unstack().fillna(0)
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
      <th>platform</th>
      <th>3DS</th>
      <th>DS</th>
      <th>PC</th>
      <th>PS2</th>
      <th>PS3</th>
      <th>PS4</th>
      <th>PSP</th>
      <th>PSV</th>
      <th>Wii</th>
      <th>WiiU</th>
      <th>X360</th>
      <th>XOne</th>
    </tr>
    <tr>
      <th>year_of_release</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
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
      <th>2010.0</th>
      <td>0.00</td>
      <td>85.02</td>
      <td>24.28</td>
      <td>5.64</td>
      <td>142.17</td>
      <td>0.00</td>
      <td>35.04</td>
      <td>0.00</td>
      <td>127.95</td>
      <td>0.00</td>
      <td>170.03</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2011.0</th>
      <td>63.20</td>
      <td>26.18</td>
      <td>35.03</td>
      <td>0.45</td>
      <td>156.78</td>
      <td>0.00</td>
      <td>17.82</td>
      <td>4.63</td>
      <td>59.65</td>
      <td>0.00</td>
      <td>143.84</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2012.0</th>
      <td>51.36</td>
      <td>11.01</td>
      <td>23.22</td>
      <td>0.00</td>
      <td>107.36</td>
      <td>0.00</td>
      <td>7.69</td>
      <td>16.19</td>
      <td>21.71</td>
      <td>17.56</td>
      <td>99.74</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>2013.0</th>
      <td>56.57</td>
      <td>1.54</td>
      <td>12.38</td>
      <td>0.00</td>
      <td>113.25</td>
      <td>25.99</td>
      <td>3.14</td>
      <td>10.59</td>
      <td>8.59</td>
      <td>21.65</td>
      <td>88.58</td>
      <td>18.96</td>
    </tr>
    <tr>
      <th>2014.0</th>
      <td>43.76</td>
      <td>0.00</td>
      <td>13.28</td>
      <td>0.00</td>
      <td>47.76</td>
      <td>100.00</td>
      <td>0.24</td>
      <td>11.90</td>
      <td>3.75</td>
      <td>22.03</td>
      <td>34.74</td>
      <td>54.07</td>
    </tr>
    <tr>
      <th>2015.0</th>
      <td>27.78</td>
      <td>0.00</td>
      <td>8.52</td>
      <td>0.00</td>
      <td>16.82</td>
      <td>118.90</td>
      <td>0.12</td>
      <td>6.25</td>
      <td>1.14</td>
      <td>16.35</td>
      <td>11.96</td>
      <td>60.14</td>
    </tr>
    <tr>
      <th>2016.0</th>
      <td>15.14</td>
      <td>0.00</td>
      <td>5.25</td>
      <td>0.00</td>
      <td>3.60</td>
      <td>69.25</td>
      <td>0.00</td>
      <td>4.25</td>
      <td>0.18</td>
      <td>4.60</td>
      <td>1.52</td>
      <td>26.15</td>
    </tr>
  </tbody>
</table>
</div>




```python
data_2010_2016 = df[df['year_of_release'].between(2010, 2016)]
data_2010_2016
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
      <th>name</th>
      <th>platform</th>
      <th>year_of_release</th>
      <th>genre</th>
      <th>na_sales</th>
      <th>eu_sales</th>
      <th>jp_sales</th>
      <th>other_sales</th>
      <th>critic_score</th>
      <th>user_score</th>
      <th>rating</th>
      <th>total_sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>14</th>
      <td>Kinect Adventures!</td>
      <td>X360</td>
      <td>2010.0</td>
      <td>Misc</td>
      <td>15.00</td>
      <td>4.89</td>
      <td>0.24</td>
      <td>1.69</td>
      <td>61.0</td>
      <td>6.3</td>
      <td>E</td>
      <td>21.82</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Grand Theft Auto V</td>
      <td>PS3</td>
      <td>2013.0</td>
      <td>Action</td>
      <td>7.02</td>
      <td>9.09</td>
      <td>0.98</td>
      <td>3.96</td>
      <td>97.0</td>
      <td>8.2</td>
      <td>M</td>
      <td>21.05</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Grand Theft Auto V</td>
      <td>X360</td>
      <td>2013.0</td>
      <td>Action</td>
      <td>9.66</td>
      <td>5.14</td>
      <td>0.06</td>
      <td>1.41</td>
      <td>97.0</td>
      <td>8.1</td>
      <td>M</td>
      <td>16.27</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Pokemon Black/Pokemon White</td>
      <td>DS</td>
      <td>2010.0</td>
      <td>Role-Playing</td>
      <td>5.51</td>
      <td>3.17</td>
      <td>5.65</td>
      <td>0.80</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>15.13</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Call of Duty: Modern Warfare 3</td>
      <td>X360</td>
      <td>2011.0</td>
      <td>Shooter</td>
      <td>9.04</td>
      <td>4.24</td>
      <td>0.13</td>
      <td>1.32</td>
      <td>88.0</td>
      <td>3.4</td>
      <td>M</td>
      <td>14.73</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>16703</th>
      <td>Strawberry Nauts</td>
      <td>PSV</td>
      <td>2016.0</td>
      <td>Adventure</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>16707</th>
      <td>Aiyoku no Eustia</td>
      <td>PSV</td>
      <td>2014.0</td>
      <td>Misc</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>16710</th>
      <td>Samurai Warriors: Sanada Maru</td>
      <td>PS3</td>
      <td>2016.0</td>
      <td>Action</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>16712</th>
      <td>Haitaka no Psychedelica</td>
      <td>PSV</td>
      <td>2016.0</td>
      <td>Adventure</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>16714</th>
      <td>Winning Post 8 2016</td>
      <td>PSV</td>
      <td>2016.0</td>
      <td>Simulation</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>0.01</td>
    </tr>
  </tbody>
</table>
<p>5277 rows × 12 columns</p>
</div>




```python
sales_per_platform = df.groupby('platform')['total_sales'].sum().sort_values(ascending=False)


top_platforms = sales_per_platform.head(5)

print("Plataformas líderes en ventas:")
print(top_platforms)

platform_trend = df[df['platform'].isin(top_platforms.index)].groupby(['platform', 'year_of_release'])['total_sales'].sum().unstack()

print("\nTendencia de ventas para las plataformas líderes:")
print(platform_trend)
```

    Plataformas líderes en ventas:
    platform
    PS2     1255.77
    X360     971.42
    PS3      939.65
    Wii      907.51
    DS       806.12
    Name: total_sales, dtype: float64
    
    Tendencia de ventas para las plataformas líderes:
    year_of_release  1985.0  2000.0  2001.0  2002.0  2003.0  2004.0  2005.0  \
    platform                                                                  
    DS                 0.02     NaN     NaN     NaN     NaN   17.27  130.14   
    PS2                 NaN   39.17  166.43  205.38  184.31  211.81  160.66   
    PS3                 NaN     NaN     NaN     NaN     NaN     NaN     NaN   
    Wii                 NaN     NaN     NaN     NaN     NaN     NaN     NaN   
    X360                NaN     NaN     NaN     NaN     NaN     NaN    8.25   
    
    year_of_release  2006.0  2007.0  2008.0  2009.0  2010.0  2011.0  2012.0  \
    platform                                                                  
    DS               119.81  146.94  145.31  119.54   85.02   26.18   11.01   
    PS2              103.42   75.99   53.90   26.40    5.64    0.45     NaN   
    PS3               20.96   73.19  118.52  130.93  142.17  156.78  107.36   
    Wii              137.15  152.77  171.32  206.97  127.95   59.65   21.71   
    X360              51.62   95.41  135.26  120.29  170.03  143.84   99.74   
    
    year_of_release  2013.0  2014.0  2015.0  2016.0  
    platform                                         
    DS                 1.54     NaN     NaN     NaN  
    PS2                 NaN     NaN     NaN     NaN  
    PS3              113.25   47.76   16.82    3.60  
    Wii                8.59    3.75    1.14    0.18  
    X360              88.58   34.74   11.96    1.52  



```python
# Plataformas líderes en ventas: PS2, X360, PS3, Wii y DS.

# Tendencia de ventas para las plataformas líderes:

# PS2: Fue muy popular entre 2000 y 2006, con un pico en 2002. Después de 2006, las ventas disminuyeron significativamente.
# X360: aumento en las ventas a partir de 2006, alcanzando su punto máximo en 2010. Luego, las ventas disminuyeron gradualmente.
# PS3: Tuvo un aumento constante en las ventas desde su lanzamiento en 2006 hasta alrededor de 2011, seguido de una disminución gradual.
# Wii: Alcanzó su punto máximo en ventas en 2009, luego experimentó una disminución constante en las ventas.
# DS: Experimentó un gran éxito entre 2005 y 2009, con un pico en 2006. Sin embargo, las ventas han disminuido considerablemente desde entonces.
# podríamos considerar que las plataformas X360 y PS3 tienen un potencial interesante, ya que experimentaron un crecimiento significativo y aún mantienen cierto nivel de ventas.
```


```python
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=(14, 10))

sns.boxplot(x='platform', y='total_sales', data=df)

plt.title('Diagrama de Caja de Ventas Globales por Plataforma')
plt.xlabel('Plataforma')
plt.ylabel('Ventas Globales (en millones)')

plt.xticks(rotation=45)


plt.tight_layout()
plt.show()
```


    
![png](output_24_0.png)
    



```python
sales_summary = df.groupby('platform')['total_sales'].describe()


print(sales_summary)
```

               count      mean       std   min     25%    50%     75%    max
    platform                                                                
    2600       133.0  0.729173  0.917799  0.07  0.3000  0.460  0.7800   7.81
    3DO          3.0  0.033333  0.023094  0.02  0.0200  0.020  0.0400   0.06
    3DS        520.0  0.498077  1.430876  0.01  0.0500  0.120  0.3300  14.60
    DC          52.0  0.306731  0.468660  0.02  0.0775  0.135  0.2975   2.41
    DS        2151.0  0.374765  1.426451  0.01  0.0500  0.110  0.2700  29.80
    GB          98.0  2.606735  5.365478  0.06  0.3025  1.165  2.1650  31.38
    GBA        822.0  0.386679  0.896897  0.01  0.0525  0.160  0.3900  15.84
    GC         556.0  0.357788  0.686346  0.01  0.0600  0.150  0.3525   7.06
    GEN         29.0  1.061034  1.470645  0.03  0.0700  0.150  1.7600   6.02
    GG           1.0  0.040000       NaN  0.04  0.0400  0.040  0.0400   0.04
    N64        319.0  0.685517  1.316733  0.01  0.1350  0.270  0.5950  11.90
    NES         98.0  2.561735  5.108012  0.06  1.0000  1.375  2.2225  40.24
    NG          12.0  0.120000  0.082241  0.02  0.0550  0.100  0.2000   0.25
    PC         974.0  0.266448  0.675577  0.01  0.0200  0.050  0.1700   8.01
    PCFX         1.0  0.030000       NaN  0.03  0.0300  0.030  0.0300   0.03
    PS        1197.0  0.610576  1.054502  0.01  0.1100  0.260  0.6600  10.95
    PS2       2161.0  0.581106  1.137927  0.00  0.0800  0.230  0.5600  20.81
    PS3       1331.0  0.705973  1.391749  0.00  0.1100  0.270  0.7500  21.05
    PS4        392.0  0.801378  1.609456  0.01  0.0600  0.200  0.7300  14.63
    PSP       1209.0  0.243218  0.520210  0.01  0.0300  0.090  0.2300   7.68
    PSV        430.0  0.125744  0.212193  0.01  0.0200  0.055  0.1300   1.96
    SAT        173.0  0.194162  0.218092  0.02  0.0800  0.120  0.2600   1.93
    SCD          6.0  0.310000  0.584055  0.04  0.0525  0.065  0.1225   1.50
    SNES       239.0  0.836987  1.869469  0.01  0.1350  0.320  0.7050  20.62
    TG16         2.0  0.080000  0.084853  0.02  0.0500  0.080  0.1100   0.14
    WS           6.0  0.236667  0.159457  0.03  0.1725  0.215  0.2725   0.51
    Wii       1320.0  0.687508  3.126609  0.01  0.0800  0.190  0.4825  82.54
    WiiU       147.0  0.559116  1.058836  0.01  0.0800  0.220  0.5250   7.09
    X360      1262.0  0.769746  1.615674  0.01  0.1100  0.280  0.7575  21.82
    XB         824.0  0.312791  0.534791  0.01  0.0600  0.150  0.3500   8.48
    XOne       247.0  0.645020  1.036139  0.01  0.0600  0.220  0.6850   7.39



```python
# Promedio de ventas globales: La plataforma con las ventas promedio más altas es GB, seguida de NES y SNES.

# Diferencias en las ventas: Las ventas globales varían entre las plataformas. Por ejemplo, las ventas promedio de PS4 son mucho más altas que las de PS3 y Xbox 360.

# Dispersión de las ventas: Las plataformas con desviaciones estándar más altas, como Wii y PS2, muestran una mayor variabilidad en las ventas de sus juegos.

# Diferencias en el tamaño del mercado: Algunas plataformas tienen un número  mayor de juegos en comparación con otras, como PS2, PS3 y Xbox 360.
```


```python
import matplotlib.pyplot as plt
import seaborn as sns


xbox_360_data = df[df['platform'] == 'X360'].dropna(subset=['critic_score', 'user_score', 'total_sales'])


plt.figure(figsize=(10, 6))
sns.scatterplot(x='critic_score', y='total_sales', data=xbox_360_data, label='Critic Score')
sns.scatterplot(x='user_score', y='total_sales', data=xbox_360_data, label='User Score')
plt.title('Scatter Plot of Xbox 360 Sales vs. Reviews')
plt.xlabel('Review Score')
plt.ylabel('Global Sales')
plt.legend()
plt.grid(True)
plt.show()


correlation_critic = xbox_360_data['critic_score'].corr(xbox_360_data['total_sales'])
correlation_user = xbox_360_data['user_score'].corr(xbox_360_data['total_sales'])

print(f"Correlation between Critic Score and Sales: {correlation_critic}")
print(f"Correlation between User Score and Sales: {correlation_user}")
```


    
![png](output_27_0.png)
    


    Correlation between Critic Score and Sales: 0.38951312357066675
    Correlation between User Score and Sales: 0.1104115038347283



```python
#  A medida que las puntuaciones de los críticos aumentan, es más probable que las ventas también aumenten, pero la relación no es tan fuerte
# puede haber una ligera tendencia de que las ventas aumenten con puntuaciones de usuario más altas

```


```python
multiplatform_games = df[df.duplicated(subset='name', keep=False)]
multiplatform_games
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
      <th>name</th>
      <th>platform</th>
      <th>year_of_release</th>
      <th>genre</th>
      <th>na_sales</th>
      <th>eu_sales</th>
      <th>jp_sales</th>
      <th>other_sales</th>
      <th>critic_score</th>
      <th>user_score</th>
      <th>rating</th>
      <th>total_sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Super Mario Bros.</td>
      <td>NES</td>
      <td>1985.0</td>
      <td>Platform</td>
      <td>29.08</td>
      <td>3.58</td>
      <td>6.81</td>
      <td>0.77</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>40.24</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Tetris</td>
      <td>GB</td>
      <td>1989.0</td>
      <td>Puzzle</td>
      <td>23.20</td>
      <td>2.26</td>
      <td>4.22</td>
      <td>0.58</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>30.26</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Grand Theft Auto V</td>
      <td>PS3</td>
      <td>2013.0</td>
      <td>Action</td>
      <td>7.02</td>
      <td>9.09</td>
      <td>0.98</td>
      <td>3.96</td>
      <td>97.0</td>
      <td>8.2</td>
      <td>M</td>
      <td>21.05</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Grand Theft Auto: San Andreas</td>
      <td>PS2</td>
      <td>2004.0</td>
      <td>Action</td>
      <td>9.43</td>
      <td>0.40</td>
      <td>0.41</td>
      <td>10.57</td>
      <td>95.0</td>
      <td>9.0</td>
      <td>M</td>
      <td>20.81</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Super Mario World</td>
      <td>SNES</td>
      <td>1990.0</td>
      <td>Platform</td>
      <td>12.78</td>
      <td>3.75</td>
      <td>3.54</td>
      <td>0.55</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>20.62</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>16706</th>
      <td>Men in Black II: Alien Escape</td>
      <td>GC</td>
      <td>2003.0</td>
      <td>Shooter</td>
      <td>0.01</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>T</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>16709</th>
      <td>SCORE International Baja 1000: The Official Game</td>
      <td>PS2</td>
      <td>2008.0</td>
      <td>Racing</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>16710</th>
      <td>Samurai Warriors: Sanada Maru</td>
      <td>PS3</td>
      <td>2016.0</td>
      <td>Action</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>16713</th>
      <td>Spirits &amp; Spells</td>
      <td>GBA</td>
      <td>2003.0</td>
      <td>Platform</td>
      <td>0.01</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>16714</th>
      <td>Winning Post 8 2016</td>
      <td>PSV</td>
      <td>2016.0</td>
      <td>Simulation</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.01</td>
      <td>0.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>nan</td>
      <td>0.01</td>
    </tr>
  </tbody>
</table>
<p>7961 rows × 12 columns</p>
</div>




```python
sales_by_platform = multiplatform_games.groupby(['name', 'platform'])[['total_sales']].sum().reset_index()
sales_by_platform
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
      <th>name</th>
      <th>platform</th>
      <th>total_sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Frozen: Olaf's Quest</td>
      <td>3DS</td>
      <td>0.59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Frozen: Olaf's Quest</td>
      <td>DS</td>
      <td>0.51</td>
    </tr>
    <tr>
      <th>2</th>
      <td>007: Quantum of Solace</td>
      <td>DS</td>
      <td>0.13</td>
    </tr>
    <tr>
      <th>3</th>
      <td>007: Quantum of Solace</td>
      <td>PC</td>
      <td>0.02</td>
    </tr>
    <tr>
      <th>4</th>
      <td>007: Quantum of Solace</td>
      <td>PS2</td>
      <td>0.43</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>7950</th>
      <td>pro evolution soccer 2011</td>
      <td>PSP</td>
      <td>0.80</td>
    </tr>
    <tr>
      <th>7951</th>
      <td>pro evolution soccer 2011</td>
      <td>Wii</td>
      <td>0.22</td>
    </tr>
    <tr>
      <th>7952</th>
      <td>pro evolution soccer 2011</td>
      <td>X360</td>
      <td>0.60</td>
    </tr>
    <tr>
      <th>7953</th>
      <td>uDraw Studio: Instant Artist</td>
      <td>Wii</td>
      <td>0.17</td>
    </tr>
    <tr>
      <th>7954</th>
      <td>uDraw Studio: Instant Artist</td>
      <td>X360</td>
      <td>0.02</td>
    </tr>
  </tbody>
</table>
<p>7955 rows × 3 columns</p>
</div>




```python
sales_stats_by_platform = sales_by_platform.groupby('platform')[['total_sales']].describe()
sales_stats_by_platform
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

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="8" halign="left">total_sales</th>
    </tr>
    <tr>
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
      <th>platform</th>
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
      <th>2600</th>
      <td>17.0</td>
      <td>1.830000</td>
      <td>1.849277</td>
      <td>0.46</td>
      <td>0.6200</td>
      <td>1.35</td>
      <td>2.2000</td>
      <td>7.81</td>
    </tr>
    <tr>
      <th>3DS</th>
      <td>145.0</td>
      <td>0.351448</td>
      <td>0.786522</td>
      <td>0.01</td>
      <td>0.0700</td>
      <td>0.13</td>
      <td>0.3000</td>
      <td>7.55</td>
    </tr>
    <tr>
      <th>DC</th>
      <td>9.0</td>
      <td>0.330000</td>
      <td>0.556866</td>
      <td>0.09</td>
      <td>0.1100</td>
      <td>0.14</td>
      <td>0.2000</td>
      <td>1.81</td>
    </tr>
    <tr>
      <th>DS</th>
      <td>546.0</td>
      <td>0.362839</td>
      <td>0.684329</td>
      <td>0.01</td>
      <td>0.0825</td>
      <td>0.16</td>
      <td>0.4000</td>
      <td>10.30</td>
    </tr>
    <tr>
      <th>GB</th>
      <td>19.0</td>
      <td>3.301579</td>
      <td>6.678880</td>
      <td>0.07</td>
      <td>0.9950</td>
      <td>1.61</td>
      <td>2.1550</td>
      <td>30.26</td>
    </tr>
    <tr>
      <th>GBA</th>
      <td>230.0</td>
      <td>0.384391</td>
      <td>0.715663</td>
      <td>0.01</td>
      <td>0.0500</td>
      <td>0.16</td>
      <td>0.4200</td>
      <td>5.47</td>
    </tr>
    <tr>
      <th>GC</th>
      <td>427.0</td>
      <td>0.242904</td>
      <td>0.349343</td>
      <td>0.01</td>
      <td>0.0600</td>
      <td>0.14</td>
      <td>0.2900</td>
      <td>4.61</td>
    </tr>
    <tr>
      <th>GEN</th>
      <td>8.0</td>
      <td>1.645000</td>
      <td>1.390139</td>
      <td>0.08</td>
      <td>0.8775</td>
      <td>1.38</td>
      <td>2.2050</td>
      <td>4.33</td>
    </tr>
    <tr>
      <th>N64</th>
      <td>98.0</td>
      <td>0.689898</td>
      <td>1.449600</td>
      <td>0.02</td>
      <td>0.2000</td>
      <td>0.34</td>
      <td>0.6400</td>
      <td>11.90</td>
    </tr>
    <tr>
      <th>NES</th>
      <td>27.0</td>
      <td>4.008519</td>
      <td>7.935774</td>
      <td>0.07</td>
      <td>1.1100</td>
      <td>1.67</td>
      <td>3.5350</td>
      <td>40.24</td>
    </tr>
    <tr>
      <th>NG</th>
      <td>3.0</td>
      <td>0.110000</td>
      <td>0.078102</td>
      <td>0.06</td>
      <td>0.0650</td>
      <td>0.07</td>
      <td>0.1350</td>
      <td>0.20</td>
    </tr>
    <tr>
      <th>PC</th>
      <td>510.0</td>
      <td>0.278863</td>
      <td>0.659024</td>
      <td>0.01</td>
      <td>0.0200</td>
      <td>0.06</td>
      <td>0.2200</td>
      <td>8.01</td>
    </tr>
    <tr>
      <th>PS</th>
      <td>203.0</td>
      <td>0.952512</td>
      <td>1.180916</td>
      <td>0.02</td>
      <td>0.2300</td>
      <td>0.52</td>
      <td>1.1150</td>
      <td>6.03</td>
    </tr>
    <tr>
      <th>PS2</th>
      <td>1047.0</td>
      <td>0.766781</td>
      <td>1.319511</td>
      <td>0.00</td>
      <td>0.1600</td>
      <td>0.38</td>
      <td>0.7950</td>
      <td>20.81</td>
    </tr>
    <tr>
      <th>PS3</th>
      <td>1054.0</td>
      <td>0.748008</td>
      <td>1.440290</td>
      <td>0.01</td>
      <td>0.1300</td>
      <td>0.32</td>
      <td>0.8100</td>
      <td>21.05</td>
    </tr>
    <tr>
      <th>PS4</th>
      <td>321.0</td>
      <td>0.873769</td>
      <td>1.703264</td>
      <td>0.01</td>
      <td>0.0700</td>
      <td>0.26</td>
      <td>0.8200</td>
      <td>14.63</td>
    </tr>
    <tr>
      <th>PSP</th>
      <td>394.0</td>
      <td>0.341726</td>
      <td>0.617554</td>
      <td>0.01</td>
      <td>0.0700</td>
      <td>0.17</td>
      <td>0.3800</td>
      <td>7.68</td>
    </tr>
    <tr>
      <th>PSV</th>
      <td>205.0</td>
      <td>0.150927</td>
      <td>0.200077</td>
      <td>0.01</td>
      <td>0.0500</td>
      <td>0.09</td>
      <td>0.1700</td>
      <td>1.96</td>
    </tr>
    <tr>
      <th>SAT</th>
      <td>37.0</td>
      <td>0.210811</td>
      <td>0.149283</td>
      <td>0.03</td>
      <td>0.0800</td>
      <td>0.17</td>
      <td>0.3100</td>
      <td>0.55</td>
    </tr>
    <tr>
      <th>SNES</th>
      <td>34.0</td>
      <td>2.068824</td>
      <td>3.744020</td>
      <td>0.06</td>
      <td>0.4000</td>
      <td>0.99</td>
      <td>1.9975</td>
      <td>20.62</td>
    </tr>
    <tr>
      <th>WS</th>
      <td>2.0</td>
      <td>0.380000</td>
      <td>0.183848</td>
      <td>0.25</td>
      <td>0.3150</td>
      <td>0.38</td>
      <td>0.4450</td>
      <td>0.51</td>
    </tr>
    <tr>
      <th>Wii</th>
      <td>687.0</td>
      <td>0.509243</td>
      <td>0.918239</td>
      <td>0.01</td>
      <td>0.1000</td>
      <td>0.23</td>
      <td>0.5400</td>
      <td>10.12</td>
    </tr>
    <tr>
      <th>WiiU</th>
      <td>100.0</td>
      <td>0.317400</td>
      <td>0.550061</td>
      <td>0.01</td>
      <td>0.0575</td>
      <td>0.15</td>
      <td>0.4100</td>
      <td>4.87</td>
    </tr>
    <tr>
      <th>X360</th>
      <td>1014.0</td>
      <td>0.784152</td>
      <td>1.495789</td>
      <td>0.01</td>
      <td>0.1300</td>
      <td>0.31</td>
      <td>0.8000</td>
      <td>16.27</td>
    </tr>
    <tr>
      <th>XB</th>
      <td>594.0</td>
      <td>0.330606</td>
      <td>0.583517</td>
      <td>0.01</td>
      <td>0.0700</td>
      <td>0.15</td>
      <td>0.3775</td>
      <td>8.48</td>
    </tr>
    <tr>
      <th>XOne</th>
      <td>224.0</td>
      <td>0.603080</td>
      <td>1.006972</td>
      <td>0.01</td>
      <td>0.0575</td>
      <td>0.22</td>
      <td>0.6450</td>
      <td>7.39</td>
    </tr>
  </tbody>
</table>
</div>




```python
import seaborn as sns
import matplotlib.pyplot as plt


plt.figure(figsize=(12, 6))
sns.barplot(data=sales_by_platform, x='platform', y='total_sales', ci=None)
plt.title('Comparación de ventas por plataforma')
plt.xlabel('Plataforma')
plt.ylabel('Ventas totales')
plt.xticks(rotation=45)
plt.show()
```


    
![png](output_32_0.png)
    



```python
sales_pivot = sales_by_platform.pivot(index='name', columns='platform', values='total_sales')


sales_correlation = sales_pivot.corr()

sales_correlation
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
      <th>platform</th>
      <th>2600</th>
      <th>3DS</th>
      <th>DC</th>
      <th>DS</th>
      <th>GB</th>
      <th>GBA</th>
      <th>GC</th>
      <th>GEN</th>
      <th>N64</th>
      <th>NES</th>
      <th>...</th>
      <th>PSP</th>
      <th>PSV</th>
      <th>SAT</th>
      <th>SNES</th>
      <th>WS</th>
      <th>Wii</th>
      <th>WiiU</th>
      <th>X360</th>
      <th>XB</th>
      <th>XOne</th>
    </tr>
    <tr>
      <th>platform</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
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
      <th>2600</th>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-1.000000</td>
      <td>-0.143890</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3DS</th>
      <td>NaN</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>0.280268</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.457871</td>
      <td>0.578526</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.729235</td>
      <td>0.927479</td>
      <td>0.427384</td>
      <td>NaN</td>
      <td>0.492727</td>
    </tr>
    <tr>
      <th>DC</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>DS</th>
      <td>NaN</td>
      <td>0.280268</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>0.287382</td>
      <td>0.239476</td>
      <td>NaN</td>
      <td>0.999937</td>
      <td>0.972487</td>
      <td>...</td>
      <td>0.449933</td>
      <td>0.104825</td>
      <td>0.897802</td>
      <td>0.961980</td>
      <td>NaN</td>
      <td>0.776191</td>
      <td>0.383158</td>
      <td>0.309638</td>
      <td>0.027768</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>GB</th>
      <td>NaN</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.930596</td>
      <td>0.089232</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>GBA</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.287382</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>0.511064</td>
      <td>NaN</td>
      <td>0.669087</td>
      <td>1.000000</td>
      <td>...</td>
      <td>0.352344</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.908046</td>
      <td>NaN</td>
      <td>0.586132</td>
      <td>NaN</td>
      <td>-0.284316</td>
      <td>0.181050</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>GC</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.239476</td>
      <td>NaN</td>
      <td>0.511064</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>-0.301905</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.644407</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.672640</td>
      <td>1.000000</td>
      <td>0.239332</td>
      <td>0.541214</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>GEN</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.326726</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.121617</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>N64</th>
      <td>-1.000000</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>0.999937</td>
      <td>0.930596</td>
      <td>0.669087</td>
      <td>-0.301905</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.678302</td>
      <td>NaN</td>
      <td>-1.000000</td>
      <td>1.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>NES</th>
      <td>-0.143890</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.972487</td>
      <td>0.089232</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>...</td>
      <td>-1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.999953</td>
      <td>1.0</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>NG</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>PC</th>
      <td>NaN</td>
      <td>0.215492</td>
      <td>NaN</td>
      <td>-0.007459</td>
      <td>NaN</td>
      <td>-0.276358</td>
      <td>-0.074774</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>-0.228754</td>
      <td>0.332027</td>
      <td>-1.000000</td>
      <td>-1.000000</td>
      <td>NaN</td>
      <td>0.131156</td>
      <td>0.128753</td>
      <td>0.395925</td>
      <td>0.050747</td>
      <td>0.201787</td>
    </tr>
    <tr>
      <th>PS</th>
      <td>0.032752</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>0.059348</td>
      <td>-0.933342</td>
      <td>0.697663</td>
      <td>-0.314657</td>
      <td>1.000000</td>
      <td>0.530553</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.112008</td>
      <td>NaN</td>
      <td>-0.019238</td>
      <td>-0.281933</td>
      <td>NaN</td>
      <td>0.939293</td>
      <td>NaN</td>
      <td>0.939265</td>
      <td>-0.503338</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>PS2</th>
      <td>NaN</td>
      <td>0.685997</td>
      <td>0.942208</td>
      <td>0.039537</td>
      <td>NaN</td>
      <td>0.231957</td>
      <td>0.666429</td>
      <td>NaN</td>
      <td>0.041024</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.423086</td>
      <td>0.999954</td>
      <td>NaN</td>
      <td>0.941683</td>
      <td>NaN</td>
      <td>0.593535</td>
      <td>1.000000</td>
      <td>0.204210</td>
      <td>0.717236</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>PS3</th>
      <td>NaN</td>
      <td>0.246374</td>
      <td>NaN</td>
      <td>0.217853</td>
      <td>NaN</td>
      <td>-0.097057</td>
      <td>0.190398</td>
      <td>0.274313</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.459507</td>
      <td>0.622732</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.170035</td>
      <td>0.261212</td>
      <td>0.942593</td>
      <td>0.544855</td>
      <td>0.592735</td>
    </tr>
    <tr>
      <th>PS4</th>
      <td>NaN</td>
      <td>0.345204</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.222086</td>
      <td>0.715295</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.170320</td>
      <td>0.173120</td>
      <td>0.541798</td>
      <td>NaN</td>
      <td>0.956158</td>
    </tr>
    <tr>
      <th>PSP</th>
      <td>NaN</td>
      <td>0.457871</td>
      <td>NaN</td>
      <td>0.449933</td>
      <td>NaN</td>
      <td>0.352344</td>
      <td>0.644407</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-1.000000</td>
      <td>...</td>
      <td>1.000000</td>
      <td>0.241577</td>
      <td>NaN</td>
      <td>-1.000000</td>
      <td>NaN</td>
      <td>0.529157</td>
      <td>NaN</td>
      <td>0.451950</td>
      <td>0.395721</td>
      <td>-0.239366</td>
    </tr>
    <tr>
      <th>PSV</th>
      <td>NaN</td>
      <td>0.578526</td>
      <td>NaN</td>
      <td>0.104825</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.241577</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.327110</td>
      <td>0.342092</td>
      <td>0.854008</td>
      <td>NaN</td>
      <td>0.902941</td>
    </tr>
    <tr>
      <th>SAT</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>-1.000000</td>
      <td>0.897802</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>0.336557</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>SNES</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.961980</td>
      <td>1.000000</td>
      <td>0.908046</td>
      <td>NaN</td>
      <td>0.326726</td>
      <td>NaN</td>
      <td>0.999953</td>
      <td>...</td>
      <td>-1.000000</td>
      <td>NaN</td>
      <td>0.336557</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>WS</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Wii</th>
      <td>NaN</td>
      <td>0.729235</td>
      <td>NaN</td>
      <td>0.776191</td>
      <td>NaN</td>
      <td>0.586132</td>
      <td>0.672640</td>
      <td>NaN</td>
      <td>-0.678302</td>
      <td>1.000000</td>
      <td>...</td>
      <td>0.529157</td>
      <td>-0.327110</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>0.516911</td>
      <td>0.320886</td>
      <td>-0.019953</td>
      <td>0.007950</td>
    </tr>
    <tr>
      <th>WiiU</th>
      <td>NaN</td>
      <td>0.927479</td>
      <td>NaN</td>
      <td>0.383158</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>0.342092</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.516911</td>
      <td>1.000000</td>
      <td>0.309744</td>
      <td>NaN</td>
      <td>0.182288</td>
    </tr>
    <tr>
      <th>X360</th>
      <td>NaN</td>
      <td>0.427384</td>
      <td>NaN</td>
      <td>0.309638</td>
      <td>NaN</td>
      <td>-0.284316</td>
      <td>0.239332</td>
      <td>0.121617</td>
      <td>-1.000000</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.451950</td>
      <td>0.854008</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.320886</td>
      <td>0.309744</td>
      <td>1.000000</td>
      <td>0.063258</td>
      <td>0.566644</td>
    </tr>
    <tr>
      <th>XB</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>0.027768</td>
      <td>NaN</td>
      <td>0.181050</td>
      <td>0.541214</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>...</td>
      <td>0.395721</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.019953</td>
      <td>NaN</td>
      <td>0.063258</td>
      <td>1.000000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>XOne</th>
      <td>NaN</td>
      <td>0.492727</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>-0.239366</td>
      <td>0.902941</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.007950</td>
      <td>0.182288</td>
      <td>0.566644</td>
      <td>NaN</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
<p>26 rows × 26 columns</p>
</div>




```python
ventas_por_genero = df.groupby('genre')['total_sales'].sum().sort_values(ascending=False)


plt.figure(figsize=(10, 6))
ventas_por_genero.plot(kind='bar', color='skyblue')
plt.title('Ventas por género de juegos')
plt.xlabel('Género')
plt.ylabel('Ventas totales (en millones)')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()


generos_mas_rentables = ventas_por_genero.head(3)
generos_menos_rentables = ventas_por_genero.tail(3)

print("Géneros más rentables:")
print(generos_mas_rentables)

print("\nGéneros menos rentables:")
print(generos_menos_rentables)
```


    
![png](output_34_0.png)
    


    Géneros más rentables:
    genre
    Action     1744.17
    Sports     1331.27
    Shooter    1052.45
    Name: total_sales, dtype: float64
    
    Géneros menos rentables:
    genre
    Puzzle       242.57
    Adventure    237.59
    Strategy     174.23
    Name: total_sales, dtype: float64



```python
top_platforms_na = df.groupby('platform')['na_sales'].sum().nlargest(5)
top_platforms_eu = df.groupby('platform')['eu_sales'].sum().nlargest(5)
top_platforms_jp = df.groupby('platform')['jp_sales'].sum().nlargest(5)

print("Top 5 Plataformas en América del Norte:")
print(top_platforms_na)

print("\nTop 5 Plataformas en Europa:")
print(top_platforms_eu)

print("\nTop 5 Plataformas en Japón:")
print(top_platforms_jp)
```

    Top 5 Plataformas en América del Norte:
    platform
    X360    602.47
    PS2     583.84
    Wii     496.90
    PS3     393.49
    DS      382.40
    Name: na_sales, dtype: float64
    
    Top 5 Plataformas en Europa:
    platform
    PS2     339.29
    PS3     330.29
    X360    270.76
    Wii     262.21
    PS      213.61
    Name: eu_sales, dtype: float64
    
    Top 5 Plataformas en Japón:
    platform
    DS      175.57
    PS      139.82
    PS2     139.20
    SNES    116.55
    3DS     100.67
    Name: jp_sales, dtype: float64



```python
# En América del Norte, las cinco principales plataformas son X360, PS2, Wii, PS3 y DS, con X360 liderando en ventas con 602.47 millones de dólares en ventas.

# En Europa, las cinco principales plataformas son PS2, PS3, X360, Wii y PS, con PS2 como líder en ventas con 339.29 millones de dólares.

# En Japón, las cinco principales plataformas son DS, PS, PS2, SNES y 3DS, con DS liderando en ventas con 175.57 millones de dólares.

# Esto muestra una variación significativa en las preferencias de las plataformas entre las regiones.
```


```python
top_genres_na = df.groupby('genre')['na_sales'].sum().nlargest(5)
top_genres_eu = df.groupby('genre')['eu_sales'].sum().nlargest(5)
top_genres_jp = df.groupby('genre')['jp_sales'].sum().nlargest(5)

print("\nTop 5 Géneros en América del Norte:")
print(top_genres_na)

print("\nTop 5 Géneros en Europa:")
print(top_genres_eu)

print("\nTop 5 Géneros en Japón:")
print(top_genres_jp)
```

    
    Top 5 Géneros en América del Norte:
    genre
    Action      879.01
    Sports      684.43
    Shooter     592.24
    Platform    445.50
    Misc        407.27
    Name: na_sales, dtype: float64
    
    Top 5 Géneros en Europa:
    genre
    Action     519.13
    Sports     376.79
    Shooter    317.34
    Racing     236.51
    Misc       212.74
    Name: eu_sales, dtype: float64
    
    Top 5 Géneros en Japón:
    genre
    Role-Playing    355.41
    Action          161.43
    Sports          135.54
    Platform        130.83
    Misc            108.11
    Name: jp_sales, dtype: float64



```python
# En América del Norte, los géneros más populares son Action, Sports, Shooter, Platform y Misc, con Action liderando en ventas con 879.01 millones de dólares.

# En Europa, los géneros principales son parecidos a los de América del Norte, pero con Racing en lugar de Platform en el cuarto lugar. Action sigue siendo el género líder en ventas con 519.13 millones de dólares.

# En Japón, es totalmente diferente, con Role-Playing como el género líder en ventas seguido de cerca por Action y Sports. 

# Estas diferencias muestran cómo las preferencias de género pueden estar influenciadas por factores culturales y sociales en cada región.
```


```python
avg_sales_by_rating_na = df.groupby('rating')['na_sales'].mean().sort_values(ascending=False)


avg_sales_by_rating_eu = df.groupby('rating')['eu_sales'].mean().sort_values(ascending=False)


avg_sales_by_rating_jp = df.groupby('rating')['jp_sales'].mean().sort_values(ascending=False)

print("Ventas Promedio por Clasificación de ESRB en América del Norte:")
print(avg_sales_by_rating_na)

print("\nVentas Promedio por Clasificación de ESRB en Europa:")
print(avg_sales_by_rating_eu)

print("\nVentas Promedio por Clasificación de ESRB en Japón:")
print(avg_sales_by_rating_jp)
```

    Ventas Promedio por Clasificación de ESRB en América del Norte:
    rating
    AO      1.260000
    K-A     0.853333
    M       0.478874
    E       0.324058
    T       0.256586
    E10+    0.248817
    EC      0.191250
    nan     0.183633
    RP      0.000000
    Name: na_sales, dtype: float64
    
    Ventas Promedio por Clasificación de ESRB en Europa:
    rating
    AO      0.610000
    M       0.309642
    E       0.178008
    T       0.144218
    E10+    0.132761
    nan     0.090723
    K-A     0.090000
    RP      0.026667
    EC      0.013750
    Name: eu_sales, dtype: float64
    
    Ventas Promedio por Clasificación de ESRB en Japón:
    rating
    K-A     0.486667
    nan     0.124440
    T       0.051131
    E       0.049652
    M       0.041100
    E10+    0.028310
    AO      0.000000
    EC      0.000000
    RP      0.000000
    Name: jp_sales, dtype: float64



```python
fig, axes = plt.subplots(3, 1, figsize=(10, 15))

avg_sales_by_rating_na.plot(kind='bar', ax=axes[0], color='skyblue')
axes[0].set_title('Ventas Promedio por Clasificación de ESRB en América del Norte')
axes[0].set_ylabel('Ventas Promedio')
axes[0].set_xlabel('Clasificación de ESRB')

avg_sales_by_rating_eu.plot(kind='bar', ax=axes[1], color='lightgreen')
axes[1].set_title('Ventas Promedio por Clasificación de ESRB en Europa')
axes[1].set_ylabel('Ventas Promedio')
axes[1].set_xlabel('Clasificación de ESRB')

avg_sales_by_rating_jp.plot(kind='bar', ax=axes[2], color='salmon')
axes[2].set_title('Ventas Promedio por Clasificación de ESRB en Japón')
axes[2].set_ylabel('Ventas Promedio')
axes[2].set_xlabel('Clasificación de ESRB')

plt.tight_layout()
plt.show()
```


    
![png](output_40_0.png)
    


<div class="alert alert-block alert-success">
<b>Comentario del revisor:</b> <a class="tocSkip"></a>

Muy buen trabajo con el análisis exploratorio de los datos. Desarrollaste gráficas de box-plots para analizar ventas de las plataformas que más venden, scatter plots para ver la relación entre las score de usuarios y de los criticos respecto a las ventas, gráficas para identificar los juegos más populares en las distintas plataformas, gráficas de barras para analizar los géneros de juegos más populares y agregaste la conclusión y la interpretación de cada uno de estos resultados.   

</div>


```python
# parece que las clasificaciones de ESRB pueden tener cierto impacto en las ventas en regiones individuales, especialmente en América del Norte y Europa, donde los juegos dirigidos a audiencias adultas tienden a tener un mejor rendimiento. Sin embargo, en Japón, las preferencias de los jugadores pueden estar menos influenciadas por estas clasificaciones.
```


```python
import scipy.stats as stats

xbox_one_scores = df[df['platform'] == 'XOne']['user_score'].dropna()
pc_scores = df[df['platform'] == 'PC']['user_score'].dropna()

t_statistic, p_value = stats.ttest_ind(xbox_one_scores, pc_scores, equal_var=False)
alpha = 0.05

if p_value < alpha:
    print("Rechazamos la hipótesis nula: Las calificaciones promedio de usuario para Xbox One y PC son diferentes.")
else:
    print("No podemos rechazar la hipótesis nula: No hay suficiente evidencia para decir que las calificaciones promedio de usuario para Xbox One y PC son diferentes.")
```

    Rechazamos la hipótesis nula: Las calificaciones promedio de usuario para Xbox One y PC son diferentes.



<div class="alert alert-block alert-danger">
<b>Comentario Revisor</b> <a class="tocSkip"></a>

Te recomiendo que dentro de la función de stats.ttest_ind adiciones el elemento "equal_var = False" dado que para estos datos no podemos asegurar que las varianzas son iguales entre plataformas.
</div>


```python
import scipy.stats as stats


action_scores = df[df['genre'] == 'Action']['user_score'].dropna()
sports_scores = df[df['genre'] == 'Sports']['user_score'].dropna()

levene_statistic, levene_p_value = stats.levene(action_scores, sports_scores)

alpha = 0.05

if levene_p_value > alpha:
    equal_var = True
    print("No podemos rechazar la hipótesis nula: Las varianzas son iguales.")
else:
    equal_var = False
    print("Rechazamos la hipótesis nula: Las varianzas no son iguales.")

t_statistic, p_value = stats.ttest_ind(action_scores, sports_scores, equal_var=equal_var)

alpha = 0.05

if p_value < alpha:
    print("Rechazamos la hipótesis nula: Las calificaciones promedio de usuario para los géneros de Acción y Deportes son diferentes.")
else:
    print("No podemos rechazar la hipótesis nula: No hay suficiente evidencia para decir que las calificaciones promedio de usuario para los géneros de Acción y Deportes son diferentes.")
```

    Rechazamos la hipótesis nula: Las varianzas no son iguales.
    No podemos rechazar la hipótesis nula: No hay suficiente evidencia para decir que las calificaciones promedio de usuario para los géneros de Acción y Deportes son diferentes.


 <div class="alert alert-block alert-warning">
<b>Comentario revisor</b> <a class="tocSkip"></a>

Para estra pruebas te recomiendo hacer una prueba de  Levene  para mostrar si las varianzas son iguales y agregarlo dentro de la función. Actualmente lo colocar como equal_var=False. Para esto, primero debes calcular las varianzas para cada uno de las plataformas y en un segundo tiempo debes de hacer uso de la siguiente función: 
    
    levene(xbox_one_data['user_score'], pc_data['user_score'])
    
Adoptaremos un nivel de significancia de 0.05; si el valor p resultante es mayor a 0.05, no podemos rechazar la hipótesis nula, y si es menor a 0.05, rechazamos la hipótesis nula, indicando que las varianzas no son iguales. 
    
Solamente recuerda que la prueba de levene no es sustituto a la prueba de st.ttest_ind, más bien es complemento para saber que colocar dentro del elemento "equal_var". En este caso como rechazamos la hipótesis de varianzas iguales debemos de colocar False. Es por eso que para terminar la prueba debes de realizar la prueba de st.ttest_ind considernado el resultado de la prueba realizada de levene    
</div>


```python
# Hipótesis nula : Las calificaciones promedio de usuario para Xbox One y PC son iguales.
# Hipótesis alternativa : Las calificaciones promedio de usuario para Xbox One y PC son diferentes.
```


```python
# Hipótesis nula: Las calificaciones promedio de usuario para los géneros de Acción y Deportes son iguales.
# Hipótesis alternativa : Las calificaciones promedio de usuario para los géneros de Acción y Deportes son diferentes.
```


```python
# Criterio para probar las hipótesis:
# Utilicé un nivel alfa de 0.05, lo que significa que si el valor p resultante de la prueba es menor que 0.05, rechazamos la hipótesis nula y concluimos que hay suficiente evidencia para respaldar la hipótesis alternativa. Si el valor p es mayor que 0.05, no podemos rechazar la hipótesis nula y no hay suficiente evidencia para respaldar la hipótesis alternativa.

# En el caso de la hipótesis sobre las plataformas Xbox One y PC, como el valor p fue menor que 0.05, rechazamos la hipótesis nula y concluimos que las calificaciones promedio de usuario para estas dos plataformas son diferentes. Mientras que para la hipótesis sobre los géneros de Acción y Deportes, como el valor p fue mayor que 0.05, no rechazamos la hipótesis nula y no podemos concluir que las calificaciones promedio de usuario para estos dos géneros son diferentes.
```


```python
# En resumen, hemos explorado muchas técnicas estadísticas para comprender mejor el mercado de videojuegos. 

# Desde la identificación de las plataformas líderes en diferentes regiones hasta el análisis de los géneros más rentables y 
# la influencia de las clasificaciones de ESRB en las ventas, hemos utilizado datos detallados para obtener información valiosa. A través de la visualización de datos, la comparación de tendencias y la realización de pruebas de hipótesis, hemos obtenido una comprensión más profunda de cómo diferentes factores impactan en el éxito y la popularidad de los videojuegos en todo el mundo.

# El potencial de tener esta información es muy grande. Los análisis que hice, nos permiten identificar patrones, tendencias y áreas de oportunidad en la industria de los videojuegos. 
# Esta información puede ser utilizada por empresas para tomar decisiones estratégicas, como la planificación de lanzamientos de juegos, la asignación de recursos de marketing y la identificación de mercados objetivo. 
#Además, los hallazgos pueden servir como base para investigaciones más profundas y análisis predictivos, ayudando a prever futuras tendencias y adaptarse rápidamente a los cambios en el mercado.

# En última instancia, tener acceso a esta información detallada nos permite no solo comprender mejor la dinámica del mercado de videojuegos, sino también aprovechar al máximo las oportunidades que ofrece. Desde desarrolladores y editores hasta inversores y consumidores, el análisis de datos en esta industria es una herramienta invaluable para tomar decisiones informadas y avanzar hacia el éxito.







```

<div class="alert alert-block alert-warning">
<b>Comentario revisor</b> <a class="tocSkip"></a>

En general creo que hiciste un muy buen trabajo con el proyecto, pudiste limpiar y trabajar las bases de datos de beuna manera. Además, el análisis explorario de datos fue completo al mostrar resultados relevantes que pueden ser de mucha utilidad para la toma de decisiones y desarrollaste las pruebas de hipótesis de una buena manera. No obstante, recuerda que siempre podemos mejorar y te menciono algunos puntos que debes considerar:

* Verificar que cuando llenamos variables con valores nulos los estamos comletando con "Unknown' 

*  Considerar eliminar registros atipicos que puedan sesgar nuestros resultados. 
    
*  Considerar desarrollar un análisis para comprobar los supuestos de la prueba de hipótesis (varianzas iguales)
    
</div>
