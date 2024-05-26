# RickAndMortyAPI_PowerBI_Visualization
![Dashboard Principal](images/OIP.jpg)
*Descripción de la imagen del dashboard principal.*

Este repositorio contiene un proyecto que consulta datos de la API de Rick and Morty y los visualiza utilizando Power BI. El objetivo del proyecto es demostrar cómo extraer, transformar y visualizar datos de una API pública mediante herramientas de análisis de datos.

## Tecnologías Utilizadas
- **Python**: Para consultar y procesar los datos de la API de Rick and Morty.
- **Pandas**: Para manipulación y limpieza de datos.
- **Power BI**: Para crear visualizaciones interactivas y dashboards.

## Contenido del Repositorio
- `data_extraction.py`: Script en Python para obtener y procesar los datos de la API.
- `rickandmorty_data.csv`: Archivo CSV con los datos extraídos y procesados.
- `PowerBI_Dashboard.pbix`: Archivo de Power BI con las visualizaciones y el dashboard.

## Cómo Empezar
1. Clona este repositorio:
    ```sh
    git clone https://github.com/tuusuario/RickAndMortyAPI_PowerBI_Visualization.git
    cd RickAndMortyAPI_PowerBI_Visualization
    ```
2. Ejecuta `data_extraction.py` para obtener los datos de la API y guardarlos en un archivo CSV:
    ```sh
    python data_extraction.py
    ```
3. Abre `PowerBI_Dashboard.pbix` en Power BI para ver las visualizaciones interactivas.

## Visualizaciones en Power BI
Aquí hay una vista previa de las visualizaciones creadas en Power BI:

![Dashboard Principal](images/dashboard_main.png)
*Descripción de la imagen del dashboard principal.*

![Detalle de Personajes](images/character_details.png)
*Descripción de la imagen del detalle de personajes.*

## Ejemplo de Código
### `data_extraction.pynb`
```python
import requests
import pandas as pd

# URL base de la API de Rick and Morty
base_url = "https://rickandmortyapi.com/api"

# Función para obtener todos los personajes
def get_characters():
    characters = []
    url = f"{base_url}/character"
    while url:
        response = requests.get(url)
        data = response.json()
        characters.extend(data['results'])
        url = data['info']['next']
    return characters

# Obtener datos de los personajes
characters = get_characters()

# Convertir a DataFrame
df = pd.DataFrame(characters)

# Contar el número de episodios en los que aparece cada personaje
df['episode_count'] = df['episode'].apply(lambda x: len(x))

# Seleccionar las columnas 'name', 'gender' y 'episode_count'
new_df=df[['name','status','species','type','gender','origin_name','location_name','image','url','episode_count']]

# Exportar el DataFrame con las columnas seleccionadas a un archivo CSV
new_df.to_csv('dataset/rickandmorty_data.csv', index=False)
