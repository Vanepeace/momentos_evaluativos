# **Segmentación de clientes aplicado al análisis de reducción de tasas de natalidad en Colombia** 
## Seminario de Analítica y Ciencia de Datos

## **Generalidades**

### **1. Objetivo:**
Pre-procesar un conjunto de datos extraidos del DANE **(nombrado: nac2022.csv )** con las  estadísticas asociadas a los nacimientos en Colombia para el año 2022. Este, corresponde a una 
muestra del total de datos seleccionados en el planteamiento del presente proyecto (5 años) y serviran de base para explorar los modelos de regresión y clasificación
a implementar. 

### **2. Anotaciones importantes sobre el conjunto de datos**
Se tiene una base de datos con 39 columnas y 573.625 filas con datos demograficos, sociales, geograficos y educativos asociados a los nacimientos de individuos en el territorio
Colombiano, esta información se encuentra codificada de la siguiente manera: 

****
    
| Campo | Descripción | Ejemplo |
| :--- | :--- |:--- |
| COD_DPTO | Departamento de Nacimiento  | 17=Caldas |
| COD_MUNIC | Municipio de Nacimiento  | 15= Boyaca |
| AREANAC | Área del Nacimiento  | 3 = Rural disperso |
| SIT_PARTO | Sitio de la Parto  | 1= Institución de salud |
| OTRO_SIT | Otro sitio, ¿cuál?  | 2 = Domicilio |
| SEXO | Sexo del nacido vivo  | 1= Masculino |
| PESO_NAC | Peso del nacido vivo, al nacer | 1 = Menos de 1.000 |
| TALLA_NAC | Talla del nacido vivo, al nacer  | 1 = Menos de 20 |
| ANO | Año de la ocurrencia  | 2022 |
| MES | Mes de la ocurrencia  | 03 = Marzo |
| ATEN_PAR | El parto fue atendido por  | 1 = Médico |
| T_GES | Tiempo de gestación del nacido vivo  | 2 = De 22 a 27 |
| T_GES_AGRU_CIE | Tiempo de gestación del nacido vivo ajustado a la agrupación sugerida por la CIE (T_GES_AGRU_CIE)  | 3 = De 28 a 36|
| NUMCONSUL | Número de consultas prenatales que tuvo la madre del nacido vivo  | 00= Ninguna |
| TIPO_PARTO | Tipo de parto de este nacimiento  | 2 = Cesárea |
| MUL_PARTO | Multiplicidad del embarazo  | 3 = Triple |
| APGAR1 | Prueba APGAR al minuto del nacido vivo  | 01 - 10 = Al minuto |
| APGAR2 | Prueba APGAR a los cinco minutos del nacido vivo  | 01 - 10 = A los cinco minutos |
| IDHEMOCLAS | Hemoclasificación del nacido vivo: Grupo Sanguíneo  | 1 = A |
| IDFACTORRH | Hemoclasificación del nacido vivo: Factor RH | 1 = Positivo |
| IDPERTET | De acuerdo con la cultura, pueblo o rasgos físicos, el nacido vivo es reconocido por sus padres como  | 1 = Indígena |
| EDAD_MADRE | Edad de la madre a la fecha del parto | 2 = De 15-19 Años |
| EST_CIVM | Estado conyugal de la madre  | 4 = Está viuda |
| NIV_EDUM | Ultimo nivel de estudio que aprobó la madre  | 2 = Básica primaria |
| ULTCURMAD | Ultimo año o grado aprobado de la madre  | 99 = Sin información |
| CODPRES | País de residencia habitual de la madre en el extranjero  | Colombia |
| CODPTORE | Departamento de residencia habitual de la madre | 05 =	Antioquia |
| CODMUNRE | Municipio de residencia habitual de la madre  | 1 = Cabecera municipal |
| AREA_RES | Área de residencia habitual de la madre  | 2 = Centro poblado |
| N_HIJOSV | Número de hijos nacidos vivos que ha tenido la madre, incluido el presente  | 3 = 3 hijos |
| FECHA_NACM | Fecha de nacimiento del anterior hijo nacido vivo  | 99 = Sin información |
| N_EMB | Número de embarazos, incluido el presente  | 99 = Sin información |
| SEG_SOCIAL | Régimen de seguridad social en salud de la madre | 2 = Subsidiado |
| IDCLASADMI | Entidad Administradora en Salud a la que pertenece la madre  | 1 = Entidad promotora de salud |
| EDAD_PADRE | Edad del padre en años cumplidos a la fecha del nacimiento de este hijo  | 999 = Sin información |
| NIV_EDUP | Nivel educativo del padre, ultimo año de estudio que aprobó el padre | 5 = Media técnica |
| ULTCURPAD | Ultimo año o grado aprobado del padre  | 99 = Sin información |
| PROFESION | Profesión de quien certifica el nacimiento  | 2 = Enfermero(a) |
| TIPOFORMULARIO | Fuente del Certificado  | 1 = Certificado RUAF-ND |

   
****
    
Url origen datos: **[nac2022](https://microdatos.dane.gov.co/index.php/catalog/807/data-dictionary/F32?file_name=nac2022)**

### **3. Variable predictora, dependiente o de respuesta para el modelo de regresión**

Como resultado de un análisis visual de los datos que suministra el DANE se selecciona la variable **`MUL_PART`** como la predictora o de respuesta. Ya que suministra información de la cantidad de individuos nacidos al momento del parto, es decir, proporciona la **cantidad de nacimientos**, valor fundamental para el analisis de la tasa de natalidad.  

## **Preprocesamiento de datos**

Antes de comenzar  porfavor acceda al siguiente Script implementado enn **Google Colaboratory**:  **[Nacimientos](https://colab.research.google.com/drive/1_Gw7abhVSN5p9U0YD9DjXrDvbxyvMhVw?usp=sharing)**, allí  podrá evidenciar todo el tratamiento realizado a los datos. 
Para su entendimiento visualice y ejecute el `Script` de la siguiente manera y en el siguiente orden, identificando los siguientes titulos o encabezados: 

 ### 1. Librerias y configuraciones previas
En este bloque de código podrá encontrar las librerias que se han implementado a lo largo del `Script` para: cargar los datos, tratamiento de datos, gráficos, operaciones
matematicas y estadísticas, preparación de datos para generación de modelos, configuración de warnings o alertas. Porfavor corra este bloque de código utilizando las teclas 
`Ctrl`+`Enter`. 

 ### 2. Funciones externas para gráficar
En este bloque de código podrá identificar diferentes funciones para generar ciertos tipos de gráficos con mayor practicidad a lo largo del Script según sea la necesidad. 
Porfavor corra este bloque de código utilizando las teclas `Ctrl`+`Enter`. 

 ### 3. Carga del conjunto de datos desde Google Drive
En este apartado podrá identificar lineas de código que le permitiran acceder, descargar y abrir la base de datos a analizar desde una ubicación de Google Drive determinada. 
Porfavor corra este bloque de código utilizando las teclas `Ctrl`+`Enter` y siga los pasos indicados en el cuadro de dialogo que se despliequega en la parte superior izquierda de su pantalla, aceptando los permisos solicitados. De manera gráfica podrá visualizar lo siguiente: 

![image](https://github.com/Sebastianvc16/momentos_evaluativos/assets/165964833/5465bb76-4197-47f0-a69f-29b03ff76c3a)


De esta manera, quedará cargado el archivo `.csv`, disponible para su manipulación en pasos posteriores con el nombre `**nac**`. Puede guiarse de manera gráfica por las siguientes 

 ### 3.1 Cargar el conjunto de datos en un DataFrame
Al correr este bloque de código podrá generar un DataFrame donde podrpa visualizar las variables que componen el conjunto de datos llamado `nac2022.csv`, de la siguiente manera (Recuerde correr esta línea de codigo con las teclas `Ctrl`+`Enter`): 

![image](https://github.com/Sebastianvc16/momentos_evaluativos/assets/165964833/542f286c-fba3-4c6c-9db0-ba090c5d1dad)

### 4. Identificar datos del Dataframe 
A continuación, corra los bloques de código **4.1** y **4.2**, cómo resultado podrá visualizar con mayor detalle las columas del DataSet y su tipo (`int64`, `object`, `float64`).  

## En materia ...

### 5. Limpieza de datos 
#### Este apartado se compone de 5 bloques de código, se deben ejecutar en orden y de manera individual. Ejecutan las siguientes acciones: 

   * **5.1** En este bloque de código se eliminan las columnas que no aportan información relevante para el análisis del proyecto planteado. Al correr este bloque podrá identificar un Dataframe con 13 columnas de tipo númerico.
   * **5.2** Se genera un nuevo dataFrame llamado **`nac_1`** que contenga las columnas eliminadas y conserve los valores númericos, es decir sin descodificar (Recuerde que los valores se encuentran códificados de acuerdo a lo indicado en tabla del item **(2): Anotaciones importantes del conjunto de datos**. Esto, para evitar errores a la hora de preparar y visualizar datos para los modelos a realizar (regresión y Clasificación).
     ***NOTA***: En este mismo bloque, se reemplazarán los valores considerados *outliers* = 99 y 999, por valores tipo `NaN`.
     
   * **5.3** Al correr este bloque de código contabilizará los valores considerados `NaN` del item **5.2**.
     
   *  **5.4** Se imputan los valores `NaN` identificados previamente, por la media de la columna donde se encuentran dichos valores.
     
   *  **5.5** Se verifica que ya no se tienen valores `NaN` en el Dataframe

**NOTA:** Porfavor recuerde que para correr cada bloque de código puede utilizar las teclas `Ctrl`+`Enter`. 
     
### 6. Descodificación de variables sobre el dataFrame Original

Previamente se identificó que al traducir los códigos númericos de cada una de las columnas del conjunto de datos inicial **Ver item (2): Anotaciones importantes del conjunto de datos**, muchos de los registros eran de tipo categorico. Por tal motivo, en este bloque de código se utiliza el metodo de **maping** y la función  `Replace` para reemplazar los valores númericos por su correspondiente variable categorica, a esto le llamamos *descodificar* y así visualizar su comportamiento para comenzar a evidenciar tendencias o datos importantes. 

### 7. Visualización de datos 
#### Este apartado se compone de 6 bloques de código, se deben ejecutar en orden y de manera individual. Estos, ejecutan las siguientes acciones: 

   *  **7.1 y 7.2** Al correr este bloque de código se generarán listas de variables categóricas y númericas, respectivamente. Requeridas como argumento para graficar de acuerdo a las funciones cargadas previamente de acuerdo al apartado **2. Funciones externas para gráficar** del apartado de **Preparación de datos**.
     
   *  **7.3** Al correr este bloque de código podrá visualizar a través de graficos de barra el como se distribuyen las variables categoricas en cada columna.

   *  **7.4** En este bloque de codigo se realiza un conteo de las variables categoricas por columna.Complementando la visualizacipon gráfica obtenida en el bloque *7.3*, con valores detallados para las cantidades de variables categoricas.
      
   * **7.5** Al correr este bloque de código podrá visualizar un gráfico tipo **BoxPlot** que tendrá como finalidad observar la distribución de los datos de la variable **nacimientos** y **departamento** en cuartiles. Sin embargo, podrá observar un comportanmiento particular de acuerdo a los tipos de datos que se tienen en el Dataframe `nac_1`, su distribucón, entre otros. Estas gráficas se generan  partir de la lista **numCols** generada en el bloque **`7.1`**. 
   
   **NOTA** : Es de aclarar que si bien, la variable MUL_PART, es nuestra variable de interés para predicción, vale la pena revisar como se comporta en contextos geograficos, de escolaridad entre otros. En este aparto se intenta explorar este comportamiento gráfico, no sería la unica combinación a probar. 
     
   *  **7.6** Al correr este bloque de código podrá visualizar un gráfico tipo **ScatterPlot** que le permitirá visualizar la dispersión de los datos en cada una de las columnas o variables. Este se genera  partir de la lista **numCols** generada en el bloque **`7.2`**

### 8. Preparación de datos para el modelo de regresión 

#### Este apartado se compone de 2 bloques de código con un análisis estadístico, se deben ejecutar en orden y de manera individual. Estos, realizan las siguientes acciones: 

*  **8.1** Al correr este bloque de código visualizará un gráfico de histograma generado a partir de la función **histplot** de la libreria Seaborn, allí podrá observar la frecuencia de nacimientos segpun su tipo (1,2,3,4). 

![image](https://github.com/Sebastianvc16/momentos_evaluativos/assets/165964833/017824b5-7b23-4b2c-837a-80ef7f118122)

*  **8.2** Al correr este bloque de código visualizará una matriz de correlación generada a partir de la función **heatmap** / **matrixcorr** de la libreria Seaborn. Allí podrá identificar en tonos oscuros las correlaciones fuertes entre variables del DataFrame **nac_1**

![image](https://github.com/Sebastianvc16/momentos_evaluativos/assets/165964833/c5dcd233-f074-4685-9728-d616371d7faf)
  

### 9. Preparación de datos para el modelo de Clusterización

En este bloque de código se generan 2 Graficos, generados a partir de las variables **MUL_PART** y **NIV_EDUM** (**Ver tabla en item (2): Anotaciones importantes del conjunto de datos**), para identificar el comportamiento de la cantidad de nacimientos en relación al nivel de escolaridad de la madre. Las instancias gráficas generadas son: 

*  **Dispersión** : Permite identificar la distribución de los datos clasificados. 
*  **Clasificación**: Utilizando el metodo KMeans, podrá observar 5 clusters discrimados por color, para cada uno podrá encontrar información importante en relación al nivel de escolaridad y el aumento o disminución de la cantidad de nacimientos.
![image](https://github.com/Sebastianvc16/momentos_evaluativos/assets/165964833/71ba4ed0-a292-48c7-bafd-516505994caf)  ![image](https://github.com/Sebastianvc16/momentos_evaluativos/assets/165964833/a7c81205-25c7-4853-b7cd-b9d6c948cd19) 


# **¡ MUCHAS GRACIAS !** 

## Si deseas contribuir a este proyecto, ¡eres bienvenido! Siéntete libre de realizar tus aportes !

   
**ELABORADO POR:** 

    * LYDA VANESSA LARGO QUINTERO
    * SEBASTIAN VALENCIA CADENA
