# Projecto_Final_Bootcamp_Ironhack

En este repositorio se encuentra la información y desarrollo del projecto final de bootcamp que he realizado en Ironhack

## Objetivo del projecto

El principal objetivo de este proyecto es conocer dentro del mapa político nacional que existe en la actualidad ( Mayo del 2019) que partido político se ajusta en mayor medida a la mentalidad de la persona que rellene una encuesta final.
Con este modelo se busca verificar la identidad que tiene cada persona con la perspectiva social que se tienen sobre ellos, pues muchas veces los partidos políticos afirman tener un cierto planteamiento político e identificarse en un ámbito que luego no es respaldado por la sociedad. Es por ello, que en este proyecto no se ha analizado la percepción que los partidos quieren trasmitir sino donde se ubican según opina la población española 

## Preparación del proyecto

### Obtención del modelo predictivo

Para realizar este proyecto se ha utilizado los microdatos del  macrobarometro preelectoral que realizó el Centro de Investigaciones Sociológicas (CIS) en Marzo del 2019.
El cual consta de 16.194 encuestas realizadas en el ámbito nacional, a población con derecho a voto en elecciones generales y residente en España de ambos sexos y que sean mayores de  18 años.

http://www.cis.es/cis/opencm/ES/1_encuestas/estudios/ver.jsp?estudio=14447&cuestionario=17380&muestra=24134 (última visita el 7-VI-2019)

En el apartado de "*Fichero_de_datos*" se encuentra un fichero ZIP donde se puede encontrar la información mas importante para comenzar a realizar el análisis.

Aunque estos datos estén pensados para abrir principalmente con programas como SPSS, se pueden abrir también con otros lenguajes de programación como son R o Python.

El **primer archivo** que se tiene que visualizar es el documento llamado *DA3232*, el cual, es un texto plano en el que se indican las respuestas de las encuestas, es importante señalar **cada fila representa un caso**, asiste algún texto en el que varias filas pueden ser un único encuestado pero es raro verlo en la actualidad

El **segundo archivo** es el que tiene el título de *ES3232*, en el cual se encuentra el libro de códigos, este libro es importante pues en el primer apartado te indican donde terminan los valores de las columnas: 
               
    Lista/ESTU 1-4 CUES 5-9 CCAA 10-11 PROV 12-13 MUN 14-16 TAMUNI 17 CAPITAL 18 DISTR 19-20 SECCION 21-23
    ENTREV 24-27 P0A 28 P1 29 P2 30 P3 31 P4 32 P501 33 P502 34 P503 35 P601 36-37 P602 38-39 P603 40-41
    P701 42-43 P702 44-45 P703 46-47 P801 48 P802 49 P803 50 P804 51 P805 52 P806 53 P807 54 P808 55
    P809 56 P810 57 P811 58 P812 59 P813 60 P814 61 P815 62 P816 63 P9 64 P9A 65 P9B01 66-67 P9B02 68-69
    P10 70-71 P10A 72-73 P1101 74-75 P1102 76-77 P1103 78-79 P1104 80-81 P1105 82-83 P1106 84-85
    P12 86-87 P1301 88-89 P1302 90-91 P1303 92-93 P1304 94-95 P1305 96-97 P1306 98-99 P1307 100-101
    P1308 102-103 P1309 104-105 P1310 106-107 P1311 108-109 P1312 110-111 P1313 112-113 P1314 114-115
    P1315 116-117 P1316 118-119 P1317 120-121 P1318 122-123 P1319 124-125 P1320 126-127 P14 128-129
    P15 130-131 P16 132-133 P17 134-135 P18 136 P18A 137-138 P19 139-140 P2001 141-142 P2002 143-144
    P2003 145-146 P2004 147-148 P2005 149-150 P2006 151-152 P2007 153-154 P2008 155-156 P2009 157-158
    P2010 159-160 P2011 161-162 P2012 163-164 P2013 165-166 P2014 167-168 P2015 169-170 P2016 171-172
    P2017 173-174 P2018 175-176 P2019 177-178 P2020 179-180 P21 181-182 P21A 183-184 P22 185 P23 186-187
    P24 188 P24A 189-190 P25 191 P25A 192-193 P26 194 P27 195 P28 196 P29 197 P30 198 P30A 199 P31 200
    E101 201-202 E102 203-204 E103 205-206 E2 207-209 E3 210 C1 211 C1A 212-213 PESO 214-220(5)
    P9BCOMR 221-224 P10R 225-226 P10AR 227-228 VOTOSIMG 229-230 P18AR 231-232 RECUERDO 233-234 P9BCOM 235-238
    P14R 239-240 P15R 241-242 P16R 243-244 ESTUDIOS 245 PESOCCAA 246-252(5)
El libro de códigos también te indica que etiqueta tienen los valores y el nombre completo de las variables

El **tercer archivo** que se tiene que visualizar y tener en cuenta es el cuestionario, en el cual se puede visualizar el orden exacto que han tenido las preguntas, y la codificación de las mismas.

### Creación del DataFrame ###

Una vez se ha tenido en cuenta estas peculiaridades que tiene la encuesta, leemos el archivo, pero como se ha señalado el texto no posee ningún caracter especial para separar las columnas sino que se tiene que realizar con un diccionario que se cree con los detalles que se indican en el archivo llamado *ES3232*, el cual gracias a la función en este caso creada ad hoc, **get_intervals**, la cual crea las columnas con el nombre.

### Limpieza del DataFrame###

Al tratarse de una encuesta todas las variables están codificadas, por lo que a no ser que exista un fallo en la codificación no se va a encontrar ningún valor nulo.
Sin embargo en este caso las respuestas que hayan sido NS o NC "*se pueden entender como nulos*" si en nuestro estudio los identificamos como información nula, es decir, que no aporta ninguna información a nuestra investigación.

El problema que existe es que la codificación de los NS/NC puede ser con 8 y 9 si la variable solamente tiene datos hasta el 7, la codificación de los NS y NC se hace con 8 y 9 pero si se superan estos valores la codificación se suele realizar con 99 para NS y 88 o 98 para los NC

En este caso se encuentran variables que nos interesan para la investigación con ambos valores por lo que se tienen que tener en cuenta a la hora de eliminar estos casos y no perder información.

### Colinealidad  de las variables, elección de modelo y entrenamiento.
 
Con el DataFrame limpio y las variables que nos interesaban recodificadas, se realiza un PCA para visualizar como se distribuyen las diferentes variables dentro de dos planos y ver si se puede realizar una buena separación de los datos.
También se realizan variables *dummies* de las variables categóricas y una matriz de correlación entre las distintas variables para conocer la colinealidad de las distintas variables.

Una vez refinado el DataFrame aplicamos diferentes modelos a los datos para determinar cual es el que tiene mayor precisión. Los modelos principales utilizados han sido los siguientes, en un principio se utilizaron alguno mas o con mas variables pero no eran tan significativos por lo que sólo se dejaron los que :

    1. Linear regresion 
    2. Logistic regresion 
    3. k-Neighbours k=3 
    4. k-Neighbours k=5 
    5. RandomForest 
    6. Gaussian Method
    7. SVC
    8. GradientBoostingClassifier
    
### Significación de las variables y refinamiento del modelo

Una vez obtenido los tres modelos que son óptimos, puesto que el segundo de ellos era el de regresión lineal, se realizó un análisis de las variables para conocer cuales son las que mas peso tienen en el modelo y cuales no son significativas puesto que no están ayudando en el modelo sino que incluso pueden crear el conocido como *ruido*

Vista la significación entre las variables se quitan aquellas que no aportan ningún valor al modelo, existen algunas veces que variables que pertenecen a una variable categórica y se han convertido en dummies no son significativas, pero al existir alguna de estas nuevas variables como significativa se ha pensado que era mejor dejarlas para que sea más facil el análisis.

Una vez realizado un gridsearch, con los tres modelos que mas representación se ha tenido, se comprueba que el mejor para este análisis es el ***RandomForest*** 

### Verificación con casos aleatorios

Una vez obtenido un modelo óptimo y entrenado; seleccionamos un caso de los datos que se han incluido en la parte test y se verifica con ellos la eficancia del modelo y cuales son los partidos políticos que mas se aproximan a sus ideas.
En este caso se puede verificar como si sólo se usa el "*predict*" obtenemos un valor que en un alto porcentaje se aproxima al dato que nos facilitó en la encuesta como el partido con el que se veía mas reflajado. 
Pero al utilizar el *predict_proba* se puede verificar como a lo mejor el partido seleccionado no se encuentra el primero en el 100% de las ocasiones pero si se encuentra entre los 3 primeros. 
Por lo que se puede ver como si nos quedamos con un único partido perdemos bastante información y no se aprecia el amplio espectro político que existe en el ámbito político nacional


## Nuevos casos

Uno de los principales objetivos que tiene este proyecto es que cualquier persona pueda visualizar a que partido político se parece mas según sus ideas, es por ello que para poder conocerlas las personas deben de contestar las preguntas que se les realizan en el siguiente enlace https://es.surveymonkey.com/r/encuesta_data (última visita el 7-VI-2019), en ella se realiza una pequeña encuesta (20 preguntas en total, aunque alguna pregunta se elimina después en el análisis se realizan para respetar en lo máximo las preguntas del macrobarometro y poder ayudar a la construcción y unión de las preguntas) 

El siguiente paso en el que se esta trabajando es que al terminar la encuesta se visualice el último gráfico que aparece en el pipeline el cual ayuda a comprender que partidos políticos son los más próximos a tu pensamiento
