
# Proyecto Integrador: Predictor de demanda para redes eléctricas

**Curso de Especialización en IA y Big Data - IES San Andrés - Curso 2025-26**

## 1. Contexto del Proyecto

La transición energética depende de la capacidad de predecir la demanda eléctrica para optimizar el uso de fuentes renovables. Tu misión en este proyecto será construir un **pipeline de datos híbrido** que recoja información de la Red Eléctrica de España (REE), datos meteorológicos históricos y factores socio-económicos para entrenar un modelo capaz de predecir el consumo eléctrico nacional.

## 2. Objetivos Técnicos

- **Sistemas de Big Data:** configurar una arquitectura de nube híbrida (AWS + Local) gestionando la seguridad y el flujo de datos.
- **Big Data Aplicado:** aplicar la metodología **CRISP-DM** para transformar datos brutos en un modelo predictivo funcional.


## 3. Requisitos de las fuentes de datos

El proyecto debe integrar obligatoriamente tres fuentes:

1. **API ESIOS (Red Eléctrica):** en la [API de Red Eléctrica Nacional](https://www.ree.es/es/datos/apidatos) podrás obtener los datos de demanda real (granularidad horaria).
2. **Histórico climático:** desde la página [datosclima.es](https://datosclima.es/Aemet2013/DescargaDatos.html) podrás obtener históricos en formato **Excel** de los datos publicados por la AEMET desde el año 2013 hasta la actualidad con información sobre temperatura, viento y precipitación.
3. **Fuente de contexto (A elección):** debes buscar e integrar una tercera fuente de datos a tu proyecto, algunas sugerencias de fuentes son:
   1. Datos de calendarios y festivos, ya que el consumo eléctrico cae drásticamente los fines de semana y festivos.
   2. Precios del mercado eléctrico: en la misma API de ESIOS puedes obtener el histórico de precios. Esto te puede ayudar para predecir, no solo la demanda, sino también si el precio subirá cuando la demanda sea alta y la generación de renovable sea baja.
   3. Datos históricos de contaminación atmosférica, hay una correlación indirecta ya que el uso de calefacciones y del tráfico aumenta tanto el consumo energético como la contaminación.


## 4. Fases del proyecto (Metodología CRISP-DM)

En este proyecto seguirás la **metodología CRISP-DM** tal como hemos visto en clase. Con objeto de abarcar diferentes tecnologías vistas en el curso, trabajarás en un entorno híbrido donde la capa bronce se almacenará en un Data Lake en Amazon AWS y las capas plata y oro las gestionarás en local.

Debes seguir todas las fases especificadas en CRISP-DM, aunque las más relevantes para los módulos de Big Data son las tres primeras fases (comprensión de negocio, comprensión de los datos y preparación de los datos), así como la última (despliegue).

Algunos consejos respecto a estas fases:

### Fase I: Comprensión del negocio

Asegúrate de entender bien lo que quieres hacer, cuál es el objetivo final y qué métrica o resultado vas a tener en cuenta para considerarlo un éxito o un fracaso.

### Fase II: Comprensión de los datos

Estudia bien los datos con los que vas a trabajar, determina cuáles te van a ser útiles y cuáles no, identifica las relaciones entre los diferentes datos y, en definitiva, entiende con qué vas a trabajar.


### Fase III: Preparación de los datos

En esta fase es cuando te pondrás ya manos a la obra. Vamos a trabajar utilizandola arquitectura medallón, así que tienes varios pasos:

#### Capa bronce

La capa bronce la implementaremos en Amazon AWS, la idea es que:

- Crees un bucket s3 para alojar los datos
- Desarrolles un **AWS Lambda** en Python que consuma la API de ESIOS y deposite el JSON original en este bucket
- Cargues en este bucket también los datos del clima (manualmente o automatizándolo con un script en Python), así como la tercera fuente de datos que hayas escogido.

#### Capa plata

Esta capa ya la implementaremos en local en nuestro equipo. Sería interesante, aunque no obligatorio, implementar un entorno HSFS para alojar los datos con contenedores.
 Algunas cosas a tener en cuenta:

- **Conexión local-cloud**: utiliza la librería `boto3` para recoger los datos de AWS
- **Almacenamiento**: sería interesante, aunque no obligatorio, que despliegues un entorno HDFS co Docker para alojar los datos de esta capa y de la capa oro.
- **Limpieza y normalización**: a medida que vayas leyendo los datos realiza todas las operaciones de limpieza, normalización y estandarización de los datos.
- **Formato**: no es necesario decir que en esta capa los datos se deben guardar en un formato adecuado, como puede ser Parquet.


#### Capa oro

Una vez que tenemos los datos listos, nos queda la fase de **combinación de fuente** y de **generación de nuevas características**, tras lo cual los almacenaremos en la capa oro.


### Fases IV y V: Modelado y Evaluación

Estas fases se salen del ámbito de los módulos de Big Data, por lo que las omitirás en tu proyecto.



### Fase VI: Despliegue

Aunque no realices las fases anteriores, sí deberás realizar algún tipo de despliegue. Como no hay predicciones el despliegue consistirá en crear un **Dashboard interactivo** con los datos ya limpios.

El contenido exacto de este dashboard os lo diré más adelante.


## 5. Entrega

En este proyecto deberás entregar:

1. **Memoria del proyecto:** documento PDF siguiendo las fases de CRISP-DM.
2. **Código fuente:** repositorio (GitHub/GitLab) con los scripts de AWS Lambda, los notebooks de procesamiento local y el código del Dashboard.
3. **Diccionario de datos:** documentación de las columnas finales de la capa *Gold*.
4. Eventualmente , se podrá realizar una **defensa en clase** del proyecto.



## 6. Criterios de Evaluación

**Pendiente**