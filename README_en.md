# traslados_INM

Project analyzing the official records of the Mexican National Immigration Institute [INM]'s internal transfers from 2017 through the first half of 2024.

Here, we created source files for @jdanielgoh's interactive data visualization and our corresponding report, [The Effects of Immigrant Dispersion Policies in Mexico](https://tirandocodigo.mx/traslados-migracion/). 

By observing trends in the INM's internal transfers, we are able to gain a better understanding of a key mechanism for US border externalization in Mexican territory. We also observe the construction of megaproject-level infrastructure facilitating civil/military collaboration to contain immigrants in transit. 

## The data

The data which make up our main database documenting INM transfers were obtained through an information request in 2024. They cover 2017-2023 and the first half of 2024. For each trip (row), authorities registered the origin and destination, how many people were aboard, and their sexes, nationalities and if they were adults or minors. 

- Cleaning the data was complicated due to important inconsistencies between the way different INM regional offices documented their data, which sometimes also vary from year to year. Our systematization of these inconsistencies and the rules we followed to resolve them in the data cleaning can be found [here](https://docs.google.com/spreadsheets/d/17OCfRHTOGVZ7WL_YxtLJe7dqQxjmPX-1wGMM3uXzsgY/edit?usp=sharing). 

- In order to evaluate how well a given transfer route aligned with historical transit migration routes in Mexico, it was first necessary to generate an accurate map of such routes in QGIS. The generated routes, both as lines and with a buffer of 5km, are available in the `datos/referencias` folder, the final map can be viewed in the `docs` folder, and the process was meticulously documented in the data dictionary, which is also available in the `docs` folder in English and Spanish as well as at the end of our report.

- To check if the transfers were ending up in municipalities with detention infrastructre, we consulted the following [report](https://www.cndh.org.mx/sites/default/files/documentos/2024-02/INFORME%20ESPECIAL%20ESTANCIAS%20MIGRATORIAS.pdf) from Mexico's National Human Rights Commission. Beginning on page 164, it includes a list of such installations throughout the country, along with their opening dates. This information was then systematized into a table, which is linked in `datos/referencias`. 

- In order to evaluate the direction of each transfer, we hand-created a dictionary referring to the map of routes generated. This can be found in `datos/referencias`. 

- To assign geometry for our final interactive map, we used geographic data from Mexico’s National Institute of Statistics and Geography [INEGI](https://www.inegi.org.mx/app/ageeml/), for example the "municipios" table, which assigns a unique code (CVEGEO) to each municipality and its corresponding state. This file is included in `datos/referencias` as a .zip, **it must be expanded in order to function properly.**

- Coordinate Reference System (CRS): `EPSG:4326` (WGS 84).

- Our work was collaborative; I (@lilianafrankel) wrote in close consult with @jdanielgoh y @santiagonh, whose specific contributions are tagged in each relevant section, although their influence and commentary influence the work as a whole. Sierra Wells and Kathleen Escoto also helped check our code. 

## Requirements

- Python 3.13.5 
- Packages listed in `requirements.txt`

Recommended configuration (with a virtual environment):

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Next, open Jupyter with `jupyter notebook` and run the notebooks in order (01, 02, 03).

Remember the need to unzip the .zip "municipios" in `datos/referencias`

Note: if `geopandas` installation fails, consult [here](https://geopandas.org/en/stable/getting_started/install.html)

## Instructions

Notebooks should be run in the order they are tagged (01, 02, 03).  

## Structure

traslados_INM

- `README.md`                  ← same document in Spanish

- `LICENSE`                    ← code license

- `LICENSE-DATA`               ← data license

- `requirements.txt`           ← packages required to execute the project

- `.gitignore`                 ← execute the code with no extra files

- `notebooks/`                 ← Jupyter notebooks - should be run in order (01, 02, 03)

- `01_limpieza_traslados_INM.ipynb`

- `02_analisis_traslados_INM.ipynb`

- `03_calculos_figuras_traslados_INM.ipynb`

- `datos/`

- `originales/`            ← original files as received from INM

- `procesados/`            

- `etiquetados/`       ← the original files, plus an index and major inconsistencies highlighted in yellow

- `datos_limpios_concatenados.parquet`       ← the original data compiled into a single table

- `datos_analizados_condep.csv`         ← analyzed data (total)

- `datos_analizados_solomx.csv`         ← analyzed data (just internal transfers)

- `datos_analizados_solodep.csv`        ← analyzed data (just deportations)

- `referencias/`           ← files needed to run the code

- `rutas/`             ← line files representing historical transit migration routes in Mexico, generated in QGIS

- `rutas_buff/`        ← the same files, now with a 5km buffer

- `rutas_buff_shp/` ← the geographic data

- `rutas_buff_mun/` ← the municipalities crossed by each buffered route as .csv's

- `rutas_buff_mun_master.csv` ← master table of all municipalities crossed by buffered routes in one .csv

- `áreas_geoestadísticas_municipales.csv`     ← geographic data for all municipalities in Mexico. Source: [INEGI](https://www.inegi.org.mx/app/ageeml/)

- `municipios.zip`        ← .shp files for every municipality in Mexico, **must be unzipped to work** Source: [INEGI](https://www.inegi.org.mx/app/ageeml/)

- `EMs.csv`            ← table of INM's detention centers, along with their municipalities and opening dates 

- `diccionario_sentidos.parquet` ← dictionary of INM transfer routes and their directions, compiled manually with reference to the historical route map generated 

- `docs/`

- `mapa_rutas.png`         ← historical route map

- `data_dict_en.pdf`       ← English data dictionary

- `dicc_datos_esp.pdf`     ← Spanish data dictionary

- `para_figuras/`              ← files necessary to generate report figures in Flourish

- `para_mapa_interactivo/` ← files necessary to generate our interactive visualizations


## License

- **Data, figures and documentation:** [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.es)
- **Code:** [MIT](https://choosealicense.com/licenses/mit/)

More details in the files `LICENSE` (code) and `LICENSE-DATA` (data).

## AI disclosure

Claude (Anthropic) was used as a reference when generating code and organizing the repository. The project data was never directly shared with or processed by AI. All writing, analysis, and interpretation are fully our responsability.  

## Contact

Write me: lilianafrankel@proton.me 
