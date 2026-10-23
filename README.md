# traslados_INM

Proyecto para analizar los registros oficiales de traslados internos del Instituto Nacional de Migración (INM) en México desde 2017 hasta la primera mitad de 2024. 

Aquí se crearon los archivos base para la visualización realizada por @jdangoh y el informe ["La dispersión como una política migratoria de desgaste"](https://tirandocodigo.mx/traslados-migracion/). 

Al observar las tendencias en los traslados internos del INM, nos acercamos a un mecanismo clave para la externalización de la frontera estadounidense en territorio mexicano. También observamos la creación de una infraestructura nivel megaproyecto que facilita la colaboración entre dependencias civiles y fuerzas armadas para efectuar la contención de las personas migrantes.

## Los datos

Los datos que conforman la base principal de registros de traslados se obtuvieron mediante una solicitud de transparencia realizada al Instituto Nacional de Migración [INM] en 2024. Abarcan el periodo de 2017-2023 y la primera mitad de 2024. Para cada traslado, está registrado el origen y destino, el número total de personas a bordo, y sus sexos, nacionalidades y si eran menores o mayores de edad. 

- La limpieza de datos resultó ser una tarea compleja debido al registro de inconsistencias importantes entre las formas de registro utilizadas por cada Oficina de Representación del INM, las cuales también variaban entre los años registrados. La sistematización de estas inconsistencias y las reglas que se siguieron para homologarlas se encuentra en la siguiente [tabla](https://docs.google.com/spreadsheets/d/17OCfRHTOGVZ7WL_YxtLJe7dqQxjmPX-1wGMM3uXzsgY/edit?usp=sharing). 

- Para evaluar la correspondencia de cada traslado interno con las rutas migratorias históricas establecidas en México, fue necesario generar un mapa de rutas en QGIS. Las rutas generadas (solas y con buffer de 5 km) se encuentran en la carpeta `datos/referencias`, el mapa final en la carpeta `docs`, y el proceso se encuentra documentado con mayor detalle en el diccionario de datos, el cual también se encuentra en la carpeta `docs` en inglés y español.

- Para evaluar la correspondencia de cada municipio destino con el mapa de municipios en que se encuentra documentado alguna estancia provisional o estación migratoria del INM, se consultó el siguiente [informe](https://www.cndh.org.mx/sites/default/files/documentos/2024-02/INFORME%20ESPECIAL%20ESTANCIAS%20MIGRATORIAS.pdf) de la Comisión Nacional de Derechos Humanos, que en la página 164 empieza un recuento de dichas instalaciones en todo el país, junto con sus fechas de inicio de operaciones. Esta información fue sistematizada en una tabla, la cual está vinculada en `datos/referencias`. 

- Para evaluar el sentido de cada traslado registrado, se realizó a mano un diccionario de sentidos, con referencia al mapa de rutas generado. Este diccionario se encuentra en `datos/referencias`. 

- Para asignar la geometría para el mapa interactivo final, utilizamos los datos geográficos del [INEGI](https://www.inegi.org.mx/app/ageeml/), por ejemplo la tabla de municipios, el cual asigna cada municipio y su correspondiente entidad federativa un código único (CVEGEO). El archivo está incluido en la carpeta `datos/referencias` como un .zip, **tiene que expandirse para funcionar.**

- Sistema de referencia de coordenadas (CRS): `EPSG:4326` (WGS 84).

- El trabajo fue colaborativo; yo (@lilianafrankel) escribí en consulta cercana con @jdangoh y @santiagonh, cuyas contribuciones concretas son indicadas en las secciones a que pertenecen, aunque su influencia y comentarios permean todo el trabajo realizado. Sierra Wells y Kathleen Escoto también ayudaron a revisar el código. 

## Requisitos

- Python 3.13.5 
- Paquetes listados en `requirements.txt`

Configuración recomendada (con entorno virtual):

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Después, abre Jupyter con `jupyter notebook` y ejecuta los cuadernos en orden (01, 02, 03).

Nota: si la instalación de `geopandas` falla, consulta la guía oficial: https://geopandas.org/en/stable/getting_started/install.html

## Instrucciones para el uso 

Los cuadernos se pueden correr en el orden en que están etiquetados (01, 02, 03). Así se repite la limpieza, el análisis, y los cálculos realizados desde la base de datos recibida del INM. 

## Estructura del repositorio

traslados_INM

- `README.md`                  ← este documento

- `LICENSE`                    ← licencia del código

- `LICENSE-DATA`               ← licencia de los datos

- `requirements.txt`           ← paquetes requeridos para ejectuar el proyecto

- `.gitignore`                 ← archivo para ejecutar el código sin extras

- `notebooks/`                 ← cuadernos de Juypter, para ejecutar en orden (01, 02, 03)

- `01_limpieza_traslados_INM.ipynb`

- `02_analisis_traslados_INM.ipynb`

- `03_calculos_figuras_traslados_INM.ipynb`

- `datos/`

- `originales/`            ← los archivos recibidos del INM

- `procesados/`            

- `etiquetados/`       ← las mismas tablas, más una columna de índice, y con las inconsistencias destacadas

- `datos_limpios_concatenados.parquet`       ← los datos originales limpios en una sola tabla, aún sin análisis

- `datos_analizados_condep.csv`         ← los datos completos analizados

- `datos_analizados_solomx.csv`         ← los traslados internos analizados

- `datos_analizados_solodep.csv`        ← las deportaciones analizadas

- `referencias/`           ← archivos necesarios para que el código corra correctamente

- `rutas/`             ← archivos geoespaciales (líneas) que representan rutas migratorias históricas en México, generados en QGIS

- `rutas_buff/`        ← las mismas rutas con un buffer de 5 kilómetros

- `rutas_buff_shp/` ← datos geográficos

- `rutas_buff_mun/` ← los municipios que cada ruta con su buffer cruza en csv's

- `rutas_buff_mun_master.csv` ← tabla que enlista todos los municipios cruzados de todas las rutas

- `áreas_geoestadísticas_municipales.csv`     ← datos geográficos de todos los municipios de México. Fuente: [INEGI](https://www.inegi.org.mx/app/ageeml/)

- `municipios.zip`        ← archivos shp de todos los municipios de México, **tiene que descomprimirse para funcionar** Fuente: [INEGI](https://www.inegi.org.mx/app/ageeml/)

- `EMs.csv`            ← tabla de estaciones migratorias y estancias provisionales del INM, sus municipios, y fechas de inicio

- `diccionario_sentidos.parquet` ← tabla de rutas posibles con sus sentidos asignados manualmente con referencia al mapa

- `docs/`

- `mapa_rutas.png`         ← el mapa de rutas como imagen

- `data_dict_en.pdf`       ← el diccionario de datos en inglés

- `dicc_datos_esp.pdf`     ← el diccionario de datos en español

- `para_figuras/`              ← archivos necesarios para generar las gráficas del informe en Flourish

- `para_mapa_interactivo/` ← archivos necesarios para generar la visualización interactiva


## Licencia

- **Datos, figuras y documentación:** [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/deed.es)
- **Código:** [MIT](https://choosealicense.com/licenses/mit/)

Los detalles completos están en los archivos `LICENSE` (código) y `LICENSE-DATA` (datos).

## Uso de inteligencia artificial

Se utilizó Claude (Anthropic) como referencia durante la generación del código y la organización del repositorio. Los datos del proyecto nunca se compartieron directamente con la herramienta. Toda la redacción, el análisis y la interpretación de los resultados son de los autores, quienes asumen la responsabilidad del contenido final.

## Contacto

Con cualquier duda, escríbame: lilianafrankel@proton.me 
