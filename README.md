---
title: "TRABAJO FINAL"
author: "Los pescaditos; Flor de Maria Concha, Mirka Prieto, Alessandra Rossell, Astrid Rosales"
date: "2023-06-30"
output:
  prettydoc::html_pretty:
    theme: hpstr
    toc: yes
  html_document: default
  tufte::tufte_html: default
---
```{r}
getwd()
```

### **Pregunta de investigación:**

¿Qué factores tienen incidencia en el salario promedio alrededor del mundo en 2021?

### **Objetivo general:**

-Identificar los principales factores que inciden en el ingreso salarial promedio.


-Evaluar la magnitud de la influencia de cada factor en el ingreso salarial promedio.


-Analizar posibles interacciones y relaciones entre los factores identificados.


-Proporcionar información relevante para diseñar políticas y estrategias orientadas a reducir la brecha salarial.



```{r,echo=FALSE, out.width="40%",fig.align="center"}
knitr::include_graphics("mundomap.jpg") 
```

### **Factores:**


*- Tasa de alfabetización*


*- Migración neta*


*- Esperanza de vida*


*- Tasa de desempleo*


*- Crecimiento poblacional*


*- Crecimiento del PBI*


*- Educación secundaria*


*- Educación terciaria*


### **Hipótesis**
 
 H: Todas las variables independientes seleccionadas tienen impacto en el promedio salarial.

### **Importancia del caso:**

*Las diferencias de inclusión laboral y de brecha de género entre hombres y mujeres están siendo un reto a nivel mundial. A pesar de que la fuerza de trabajo de la mujer ha aumentado en las últimas décadas, sigue estando 27 puntos porcentuales inferior a la de los hombres (OIT). La persistencia de las brechas de género en el mercado laboral representa una violación de los derechos económicos de las mujeres, que han sido reconocidos internacionalmente a través de compromisos en materia de derechos humanos e instrumentos específicos de derechos de la mujer (Convención sobre la eliminación de todas las formas de discriminación contra la mujer).*

*Las razones por las cuales este problema sigue perpetuándose se pueden explicar en base a distintos factores, por ejemplo, en primer lugar el acceso a la educación . A pesar de que el rendimiento de las mujeres son más altos para las mujeres solo en el caso de los percentiles 50 y 75 (por ejemplo, 2% para las mujeres y 1% para los hombres en ambos grupos), es decir, entre los individuos de mayor ingreso.* 

*Otro factor, la residencia urbana del trabajador ejerce una influencia positiva sobre el ingreso medio, siendo el efecto similar para hombres y mujeres: por ejemplo, una mujer urbana gana un 44% más en comparación con una mujer con las mismas características pero que reside en el área rural, en el caso de los hombres urbanos, estos ganan un 64% más. El efecto de la educación disminuye a medida que  nos movemos desde el percentil 10 al percentil 90.*  

## **METODOLOGÍA Y DATOS**
```{r,echo=FALSE, out.width="40%",fig.align="center"}
knitr::include_graphics("limpr.jpg") 
```

## **ANÁLISIS EXPLORATORIO:**


*El análisis factorial exploratorio es una técnica estadística que se utiliza para identificar patrones y relaciones entre variables en un conjunto de datos. Su objetivo es reducir la complejidad de los datos al identificar las variables más importantes y agruparlas en factores latentes.* Esta técnica nos ha permitido identificar las variables que están más correlacionadas entre sí, lo que nos ayuda a entender mejor las relaciones entre ellas. Al agrupar estas variables en factores latentes, podemos reducir la cantidad de información que necesitamos procesar y obtener una visión más clara y concisa de los datos.

*Sin embargo, este análisis no nos da conclusiones. Por tanto, elegimos continuar con el siguiente modelo, para tener aproximaciones.*

## **MODELO DE REGRESIÓN LINEAL MÚLTIPLE:**


*El modelo de regresión lineal múltiple es una técnica estadística utilizada para analizar la relación entre una variable dependiente y dos o más variables independientes. En este modelo, se trata de ajustar una línea recta que mejor se ajuste a los datos, con el objetivo de predecir el valor de la variable dependiente en función de los valores de las variables independientes. En este caso, se está utilizando el modelo de regresión lineal múltiple para analizar si las variables independientes, que incluyen migración, tasa de alfabetización, PBI, crecimiento de la población, acceso a la electricidad, esperanza de vida, desempleo, educación secundaria, educación terciaria, empleo de mujeres y tasa de migración, son significativas en la variable dependiente, que en este caso es el salario.*

El objetivo de este análisis es determinar si existe una relación significativa entre las variables independientes y el salario, y si es así, identificar la fuerza y dirección de esta relación.

## **Fuentes** 

Fuentes que utilizamos para la construcción de la base de datos

- Las bases de datos para las variables independientes provienen de diversos módulos de la data del Banco Mundial.

- La base de datos de la variable dependiente Promedio Salarial de un país, en adelante Promedio Salarial, ha sido proporcionado por el Banco Mundial.

## **Limpieza de la base de datos:**

- Se ha decidido trabajar sólo con los datos del año 2021 debido a que ese es el período más reciente con datos prácticamente  completos para todas las variables.

- Para 2021, se tenía disponible el salario promedio de 126 países. Sin embargo, al combinarlo con otros módulos disponibles  disponibles para el mismo año, se redujo a 101 casos completos.

- Para algunas bases de datos como Migración neta y Tasa de alfabetización se ha hecho el rename de los nombres de varios países de inglés a español con el comando *data[data$Pais=="Nombre original del pais",'Pais']= "Nombre en español del país"*  ya que al momento de descargar la base de datos, esta estaba en inglés.

- Para la limpieza de columnas se han utilizado los comandos *data[,c(2)]=NULL* y *data[,c(2:50)]=NULL*

- Para cambiar el nombre de las columnas se ha utilizado el comando *names(data)[1]<- 'Pais'*

- Para eliminar filas se ha utilizado el comando *data <- filter(data, row_number() != 1)* debido a que en los diversos módulos del Banco Mundial, dentro de la columna países estaban incluídos diferentes organismos como "Union Europea", "Países que forman parte de la OCDE", entre otros que si bien incluyen a países de diversos bloques económicos, se decidió que no eran necesarios para el análisis. 

- Los diferentes módulos de las bases de datos del Banco Mundial fueron unidas con la base de datos de Promedio Salarial usando el comando de *merge* de la siguiente forma *datafinal=merge(data1,data2)*

- Debido a que en algunos países se presentaban valores perdidos, el comando *merge* los fue eliminando de la Base de datos final por lo que sólo nos quedamos con 101 países. 


## **JUSTIFICACIÓN DE LAS VARIABLES INDEPENDIENTES**


**DESEMPLEO:**


Esta variable tiene relevancia, ya que bajo distintos análisis económicos, el nivel de desempleo puede tener un impacto en los promedios salariales y viceversa ya que existen distintos factores que influyen por ejemplo, en primer lugar la oferta y demanda de trabajo.  Cuando hay un alto nivel de desempleo, los empleadores pueden tener más poder de negociación para establecer salarios más bajos, ya que los trabajadores están dispuestos a aceptar empleos a cualquier precio para asegurar un ingreso. Esto puede conducir a una disminución en los promedios salariales. En segundo lugar, el crecimiento económico, ya que durante períodos de fuerte crecimiento económico, es posible que haya una mayor demanda de trabajadores, lo que puede generar una disminución del desempleo y un aumento en los promedios salariales. Esto se debe a que los empleadores pueden competir por trabajadores calificados, lo que les lleva a ofrecer salarios más altos para atraer y retener talento.En tercer lugar, las políticas  gubernamentales, como el establecimiento de un salario mínimo o la implementación de políticas de protección laboral, pueden influir en los promedios salariales y en el desempleo. Por ejemplo, si se establece un salario mínimo alto, esto puede aumentar los costos laborales para los empleadores y potencialmente resultar en una disminución en la contratación o un aumento del desempleo. Por último, la productividad laboral: La productividad laboral, es decir, la cantidad de producción generada por cada trabajador, también puede influir en los promedios salariales y en el desempleo. Cuando los trabajadores son más productivos, es más probable que los empleadores estén dispuestos a pagar salarios más altos. Por otro lado, si la productividad laboral disminuye, esto puede tener un efecto negativo en los salarios y aumentar el desempleo.


**ESPERANZA DE VIDA:**


La variable "esperanza de vida" y la variación de promedios salariales en el mundo también están relacionadas, aunque es importante tener en cuenta que existen múltiples factores que pueden influir en cada una de estas variables. Por ejemplo esta se refiere al acceso a servicios de salud, condiciones de vida, estilos de vida y salud. A partir de estos factores se puede establecer una relación con el acceso a oportunidades laborales y , por tanto a mejores o peores condiciones de salarios. En primer lugar, el acceso a servicios de salud: Los salarios pueden influir en la esperanza de vida a través del acceso a servicios de salud de calidad. Los ingresos más altos permiten a las personas acceder a una atención médica adecuada, incluyendo visitas regulares al médico, medicamentos, tratamientos y cirugías necesarias. El acceso a servicios de salud de calidad puede ayudar a prevenir enfermedades, diagnosticarlas tempranamente y brindar tratamientos efectivos, lo que puede aumentar la esperanza de vida. En segundo lugar, las condiciones de vida: Los salarios más altos suelen estar asociados con mejores condiciones de vida, como viviendas de mejor calidad, acceso a agua potable, saneamiento básico, alimentación adecuada y entornos más seguros. Estas condiciones favorables pueden contribuir a una mejor salud y, por lo tanto, a una mayor esperanza de vida. En tercer lugar, el estilo de vida y salud, ya que los salarios también pueden influir en el estilo de vida de las personas. Un mayor ingreso puede permitir el acceso a opciones más saludables, como una alimentación balanceada, actividad física regular y tiempo para el descanso. Estas elecciones de estilo de vida saludables pueden tener un impacto positivo en la salud y contribuir a una mayor esperanza de vida.


**EDUCACIÓN SECUNDARIA:**


La variable “Educación Secundaria”, es importante porque impacta en los salarios de las personas, ya que puede limitar las opciones de carrera y los ingresos potenciales de una persona. Sin embargo, esto también puede variar según el país y el mercado laboral en el que se encuentre laborando. En primer lugar, tener una secundaria completa, genera mayor empleabilidad, pues es un requisito mínimo para muchos trabajos, lo que significa que las personas que han completado la educación secundaria tienen más oportunidades de empleo. Esto puede aumentar sus posibilidades de conseguir un trabajo remunerado al menos con el sueldo básico. En segundo lugar, mejora las habilidades pues proporciona a los estudiantes habilidades y conocimientos en áreas como matemáticas, ciencias, lenguaje y comunicación. Estas habilidades son valiosas en muchos trabajos y pueden ayudar a los empleados a ser más productivos y eficientes. Por último, el crecimiento profesional, debido a que puede ser un puente para continuar con la educación superior y el desarrollo profesional. Los trabajos que requieren educación superior suelen pagar más, y las personas con educación secundaria pueden estar mejor preparadas para seguir estudiando y avanzando una carrera. Esta variable mide el promedio de hombres y mujeres que tuvieron educación secundaria.


**EDUCACIÓN TERCIARIA:**


La variable “Educación Terciaria”, es importante porque tiene un impacto más significativo en el ingreso salarial promedio que tener solo educación secundaria. Esto se debe a que la educación terciaria proporciona habilidades y conocimientos especializados que son altamente valorados en el mercado laboral y que pueden resultar en trabajos mejor remunerados. En primer lugar, permite una mayor especialización, pues los estudiantes pueden especializarse en áreas específicas de estudio, lo que puede hacerlos más valiosos para los empleadores en campos específicos. Por ejemplo, en áreas como la medicina, la ingeniería o la tecnología, entre otros. En segundo lugar, el desarrollo de habilidades avanzadas debido a que proporciona habilidades avanzadas en áreas como el pensamiento crítico, la resolución de problemas y la toma de decisiones. Estas habilidades son altamente valoradas por los empleadores y pueden llevar a trabajos mejor remunerados en una variedad de campos. Asimismo, suelen tener más oportunidades de carrera y de ascenso profesional que aquellos con sólo educación secundaria. En tercer lugar, mayores oportunidades de carrera, ya que esto puede abrir puertas a una amplia gama de oportunidades de carrera que no están disponibles para aquellos con educación secundaria. Por ejemplo, los trabajos en áreas como la investigación científica o la gestión empresarial, entre otros. Asimismo, ofrecen salarios más altos que los trabajos que solo requieren educación secundaria. Esta variable mide el promedio de hombres y mujeres que tuvieron educación terciaria.


**EMPLEO DE MUJERES:**


La variable “Empleo de mujeres”, es importante porque refleja el grado de participación de las mujeres en la fuerza laboral y su capacidad para contribuir al crecimiento económico y al desarrollo de un país. Sin embargo, es importante considerar, que no necesariamente refleja la igualdad salarial, pues a mayor cantidad de mujeres empleadas, es menor el salario que la empresa invierte en ellas. En primero lugar, la equidad de género, es un tema importante debido a que las mujeres a menudo enfrentan discriminación salarial y de oportunidades en el lugar de trabajo, lo que puede afectar negativamente sus ingresos a lo largo del tiempo. Abogar por el empleo de las mujeres y apoyar la igualdad de oportunidades puede ayudar a reducir esta brecha salarial. En segundo lugar, la mejora de la economía pues tiene un impacto positivo en la economía en general. Las mujeres representan una gran parte de la fuerza laboral y su contribución es importante para el crecimiento económico lo cual permite mejorar la estabilidad económica de una empresa, y su impacto en la sociedad. En tercer lugar, la diversidad y perspectivas únicas pues al tener diferentes experiencias y habilidades, pueden contribuir de una mejor forma en el manejo de las funciones de una empresa y, por tanto, ayudaría en su crecimiento. Al contratar y promover el empleo de las mujeres, las empresas pueden beneficiarse de esta diversidad y mejorar su desempeño y rentabilidad a largo plazo. Esta variable mide el promedio de mujeres que son contratadas en las empresas.


**MIGRACIÓN NETA**


Es relevante estudiar la variable “migración” y su posible relación con el promedio salarial de un país debido a que los migrantes tienen efectos en la economía de su país de origen así como de país al cuál migran (por ejemplo, con las transacciones producidas por las remesas) así como poseen impacto en la dinámica del mercado laboral.
Según el OIM (2021), para el año 2020, la cifra de migrantes a nivel mundial se había incrementado en  281 millones, una cifra elevada en comparación a años anteriores por lo que la migración es un tema relevante en el día a día en los países receptores. Estudiar esta variable es importante debido a que, dependiendo del contexto social, económico, cultural y político, la migración puede ser entendida como un problema o una oportunidad para mostrar el liderazgo político de un país receptor; un buen ejemplo para explicar esto es lo presentado por Wivel y Howard (2021), donde señalan que la migración puede ser enmarcada como un problema o un deber moral, dependiendo el contexto político, por ejemplo, políticas como Merkel enmarcaron la migración como una oportunidad de demostrar que Alemania, en conjunto con los países europeos, podían lidiar con esta crisis a través de políticas, en contraste, políticos como Donald Trump, enmarcaron a la migración como un problema que ocasionaba que “los verdaderos norteamericanos” se viesen desplazados por los migrantes ya que la migración retaba a aspectos como la seguridad y el bienestar financiero de todos los americanos por lo que era un “deber” detenerla; es así que al ser la migración un tema vigente y enmarcado de forma diferenciada en el debate público, se convierte en una intersante variable para el estudio. Según organismos como la CEPAL, la migración acarrea costos pero tambien beneficios economicos por lo que, al ser el promedio salarial una variable que está fuertemente relacionada con la economía de un páis, en el presente trabajo también se busca conocer si la migración tiene relación e impacto en el promedio salarial de un país.



**POBLACIÓN TOTAL**


Se busca conocer la incidencia de la población total, entendida como "todos los residentes independientemente de su estatus legal o ciudadanía" (Banco Mundial) de un país.  Estudiar la relación entre el promedio salarial y la población total es importante para conocer más acerca de a economía de un país, el desarrollo económico, las políticas económicas entre otros ya que podría proporcionar informacion que aporte para explicar el promedio salarial de un país.  


**PBI:**


El PBI es ampliamente utilizado como una medida de la actividad económica de un país. Representa el valor total de todos los bienes y servicios producidos en un período determinado. Al ser una medida integral de la actividad económica, el crecimiento del PBI se considera una indicación general del rendimiento económico de un país.  Un mayor crecimiento económico, representado por un aumento en el PBI, generalmente se asocia con un aumento en la demanda de bienes y servicios (Cavallo & otros, 2021). Esto puede conducir a la creación de nuevos empleos y oportunidades laborales. A medida que se generan más empleos, existe la posibilidad de que la competencia por la mano de obra calificada aumente, lo que podría resultar en un aumento en los salarios.
Asimismo, el crecimiento o disminución del PBI es una preocupación central para los formuladores de políticas económicas. Los gobiernos y las instituciones internacionales suelen establecer objetivos de crecimiento económico y adoptar medidas para fomentar el desarrollo económico (Cavallo & otros, 2021). Estas políticas pueden incluir incentivos para la inversión, el fomento de la innovación y la mejora de la infraestructura. Un mayor crecimiento económico a través de estas políticas puede tener un impacto positivo en el ingreso salarial promedio.


**CRECIMIENTO DE LA POBLACIÓN:**


Un mayor crecimiento de la población implica un aumento en la cantidad de personas en edad de trabajar. Como menciona la OIT (2012), esto puede resultar en una mayor oferta de mano de obra en el mercado laboral. A medida que aumenta la oferta de trabajadores, la competencia por los empleos puede intensificarse, lo que puede ejercer presión sobre los salarios. En un contexto de mayor oferta de trabajadores en relación con la demanda de empleo, es posible que los empleadores tengan más opciones y puedan ofrecer salarios más bajos. 
Además, con una mayor cantidad de personas buscando empleo, la competencia por los puestos de trabajo puede volverse más intensa. Los empleadores pueden aprovechar esta situación para negociar salarios más bajos, ya que tienen una amplia selección de candidatos para elegir. Esto puede afectar negativamente el ingreso salarial promedio, ya que los trabajadores pueden estar dispuestos a aceptar salarios más bajos para asegurar un empleo.


**ACCESO A LA ELECTRICIDAD:**


Como señalan Modi & Figueroa, el acceso a la electricidad es fundamental para impulsar la productividad y la eficiencia en diferentes sectores económicos. La electricidad proporciona energía para la maquinaria, equipos y tecnología utilizados en la producción y prestación de servicios. Un mayor acceso a la electricidad puede facilitar la automatización de procesos, mejorando la eficiencia y permitiendo un aumento en la producción. A medida que aumenta la productividad y la eficiencia, es posible generar mayores ingresos, lo que puede tener un impacto positivo en el salario promedio.
El acceso a la electricidad está estrechamente vinculado al desarrollo económico de un país. Cuando más personas tienen acceso a la electricidad, se pueden desarrollar más actividades económicas y sectores industriales. Esto puede conducir a un crecimiento económico sostenido, con la creación de nuevos empleos y oportunidades laborales. A medida que la economía crece, es más probable que los salarios también aumenten, ya que hay una mayor demanda de trabajadores cualificados. Y es especialmente relevante en sectores clave como la industria, la agricultura y los servicios (Modi & Figueroa). Estos sectores pueden ser impulsados por la disponibilidad de energía eléctrica, lo que puede generar más empleos y aumentar los ingresos. Por ejemplo, en el sector agrícola, el acceso a la electricidad puede facilitar la irrigación, el procesamiento de alimentos y la conservación, lo que a su vez puede generar más empleo y aumentar los ingresos agrícolas.



## **PROCESO**


```{r message=FALSE, warning=FALSE}
library(rio)
DL = import("Bdfin.xlsx")
```

## **CAMBIO DE FORMATOS**

**VARIABLES INDEPENDIENTES**
```{r message=FALSE, warning=FALSE}
names(DL)
```

```{r message=FALSE, warning=FALSE}
DL$Migracion = as.numeric(DL$Migracion )
DL$Tasaalfabetizacion = as.numeric(DL$Tasaalfabetizacion)
DL$PBI = as.numeric(DL$PBI)
DL$Poblaciont = as.numeric(DL$Poblaciont)
DL$Esperanzavida = as.numeric(DL$Esperanzavida)
DL$Desempleo = as.numeric(DL$Desempleo)
DL$Educsecun = as.numeric(DL$Educsecun)
DL$Educaterciaria = as.numeric(DL$Educaterciaria)
DL$Crecimientopob = as.numeric(DL$Crecimientopob)
DL$Electricidad = as.numeric(DL$Electricidad)
```

```{r message=FALSE, warning=FALSE}
DL$TasaMigracion = DL$Migracion * 100000/DL$Poblaciont #Regla de tres simple
```

**VARIABLE DEPENDIENTE**
```{r}
DL$Salario = as.numeric(DL$Salario)
str(DL$Salario)
```

```{r message=FALSE, warning=FALSE}
library(dplyr)
DG <- select(DL, -Pais, -Salario, -Poblaciont, -Migracion)
```
*se ha decidido crear una subdata DG porque no se utilizaran las variables Pais, (variable dependiente) Salario, Poblacion y Migracion.


## **ANÁLISIS FACTORIAL EXPLORATORIO**

*Se esta utilizando un analisis factorial explotario para resumir la informacion de nuestros grupos de variables a factores nuevos y obtener menor perdida de información. Asimismo nos permitira identificar que variables están mas correlacionadas.*

*Realizamos análisis factorial porque buscamos minimizar el riesgo de multicolinealidad, esto es, una alta correlación entre las variables independientes.* 


## **Calcular la matriz de correlación**

```{r message=FALSE, warning=FALSE}
library(polycor)
corMatrix=polycor::hetcor(DG)$correlations
corMatrix
```

```{r message=FALSE, warning=FALSE}
library(psych)
cor.plot(corMatrix,
 numbers=T, #Se muestren los numeros de las correlaciones
upper=F, #Que aparezca la segunda parte
main= "Matriz de correlaciones",#Titulo
show.legend=T)#Mostrar leyenda
```

Se identifican correlaciones:

**ALTAS**

- Electricidad y tasa de alfabetización (0.75)


- Esperanza de vida y tasa de alfabetización (0.71)


- El % de empleados que son mujeres y la tasa de alfabetización (0.69) 


- Electricidad y esperanza de vida (0.65)


- El % de empleados que son mujeres y esperanza de vida (0.70) 

**INTERMEDIAS**

- El % de empleados mujeres y electricidad (0.49)


- Educación secundaria y PBI (0.40)


- El % de empleados que son mujeres y esperanza de vida (0.40)


- Alfabetización y PBI (0.33)


- El ratio de mujeres por hombres en educación secundaria y tasa de alfabetización (0.31)


- Educacion secundaria y crecimiento poblacional (0.30)


- Educacion secundaria y tasa de alfabetizacion (0.31)


- Tasa de migracion y esperanza de vida (0.30)


- El % de empleadas que son mujeres y educacion secundaria (0.30)

**BAJAS**

Finalmente, se encontró una correlación muy baja e, incluso, nula entre el desempleo y la mayoría de variables, a excepción del PBI (0.19) y la tasa de alfabetización (0.13). Por esta razón, se decide excluir el desempleo.

Además se encontró que se correlacionaba negativamente, por lo cual preferimos excluirla del modelo factorial, pero conservarla en la regresión.


```{r}
DG1 <- select(DG, -Desempleo, -TasaMigracion, -Crecimientopob)
```

*Volvemos a correr la matriz de correlaciones excluyendo el desempleo.*
```{r}
corMatrix1=polycor::hetcor(DG1)$correlations
corMatrix1
```

```{r}
cortest.bartlett(corMatrix,n=nrow(DG1))$p.value>0.05 #Menor a 0.05 saldrá FALSE, mayor a 0.05 saldra TRUE
```

*- H0: la matriz de correlaciones es una matriz de identidad, o sea, las variables solo mantienen correlación consigo mismas.* 

*- H0: la matriz de correlaciones NO es una matriz de identidad.*

- Conclusión: no es una matriz de identidad, por lo que podemos continuar con el AFE.


## **Evaluar adecuación de la muestra**


```{r message=FALSE, warning=FALSE}
library(psych)
psych::KMO(DG1) 
```

El KMO es 0.73, lo que es un valor bueno, lo cual posibilita seguir con el analisis.


## **Estimar el número de factores**

```{r}
fa.parallel(corMatrix1, fm="pa", fa="fa", main = "Scree Plot")
```
El Scree Plot sugiere que el número de factores sea 2; sin embargo, el número de factores con eigen values por encima de 1 es 1.


```{r message=FALSE, warning=FALSE}
library(GPArotation)
factorial <- fa(DG1, nfactors= 2 ,rotate = "varimax", fm ="minres")
factorial
```


```{r}
fa.diagram(factorial)
```

El factor MR1 hace referencia a las condiciones de vida y el factor MR2 se refiere a oportunidades de crecimiento.

```{r}
print(factorial$loadings, cutoff = 0.35)
```

```{r}
sort(factorial$communality)
```

Variables se extrae la mayor cantidad de información: Alfabetización y, en segundo lugar, esperanza de vida.

```{r}
sort(factorial$complexity)
```

- En cuántos factores carga la variable; por ejemplo, empleo mujer y tasa de alfabetización cargan con coeficientes por encima de 0.368 y 0.546, respectivamente, en el segundo factor. 

```{r}
sort(factorial$uniquenesses)
```

Qué proporción de la varianza de la variable es varianza única.

```{r message=FALSE, warning=FALSE}
factorial_casos<-as.data.frame(factorial$scores)
head(factorial_casos)
summary(factorial_casos)
```

```{r message=FALSE, warning=FALSE}
DL$factor1<- factorial_casos$MR1
DL$factor2<- factorial_casos$MR2
```

```{r message=FALSE, warning=FALSE}
library(BBmisc)
DL$factor1 = normalize(DL$factor1, 
                                        method = "range", 
                                        margin=2, # by column
                                        range = c(0, 100))
DL$factor2 = normalize(DL$factor2, 
                                        method = "range", 
                                        margin=2, # by column
                                        range = c(0, 100))
```

## **MODELO DE REGRESIÓN LINEAL MÚLTIPLE**

*JUSTIFICACIÓN*

Se esta utilizando una regresión lineal múltiple para ver si las variables independientes (migración, tasa de alfabetización, PBI, crecimiento de la población, acceso a la electricidad, esperanza de vida, desempleo, educación secundaria, educación terciaria, empleo de mujeres, tasa de migración) son signficativos en la variable dependiente (salario).

**Variable dependiente:** SALARIO

**Variable independiente:** MR1, MR2, Tasa de Migración, Desempleo, Crecimiento poblacional

```{r message=FALSE, warning=FALSE}
DL$MR1=DL$"Factor1"
DL$MR2=DL$"Factor2"
```

```{r message=FALSE, warning=FALSE}
library(tidyverse)
```


```{r}
modelo1= lm(Salario ~ factor1 + factor2, DL)
summary(modelo1)
```

*Se propuso un primer modelo en el que solo se incluyó los factores extraídos por el EFA. Dicho modelo:*

**Dicho modelo:**
- Es significativo, con un p valor de 1.041e-09.

- Tiene un R cudrado de 0.3309, lo que significa que el 33% de la varianza de la variable dependiente es explicada por el modelo

- Se identificó efecto significativo del factor 1, este efecto es positivo.



```{r message=FALSE, warning=FALSE}
modelo2= lm(Salario ~ factor1 + TasaMigracion + Desempleo + Crecimientopob, DL)
summary(modelo2)  
```
Se propuso un segundo modelo en el que se incluyó además de los factores extraídos por el EFA, las variables Tasa de migración, Desempleo y crecimiento población. 

**Dicho modelo:**

- Es significativo, con un p valor de 5.838e-10

- Tiene un R cuadrado de 0.3716, lo que significa que el 39% de la varianza de la variable dependiente es explicada por el modelo

- Se identificó efecto significativo del factor 1, este efecto es positivo, y del crecimiento población con un efecto negativo: esto es, que a medida que mejoran las condiciones de vida, también mejora el salario promedio. Por otra parte, a medida que la población está en crecimiento disminuye el salario promedio.


```{r message=FALSE, warning=FALSE}
library(lm.beta)
modelo1$coefficients
```

## **MODELO 1**

### **SUPUESTOS:**

**LINEALIDAD**


*Los residuos deben tener una distribución normal.*


```{r message=FALSE, warning=FALSE}
library(ggfortify)
plot(modelo1,1)
autoplot(modelo1,1)
```

```{r}
cor.test(DL$Salario, DL$factor1)
cor.test(DL$Salario, DL$factor2) #no funciona
# (completar) No es lineal
```
DL$Salario and DL$factor1:*Si cumple con el supuesto de linealidad debido a que el p-value es 1.168e-10 (<0.05).*


DL$Salario and DL$factor2:
*No cumple con el supuesto de lienalidad debido a que el p-value es 0.4139 (>0.05).*



**NORMALIDAD DE RESIDUOS**

```{r}
plot(modelo1, 2)
```


**Normalidad**

```{r}
shapiro.test(modelo1$resid)
```

No hay normalidad de residuos debido a que el p-values es menor a 0.05.



**HOMOCEDASTICIDAD**

```{r}
plot(modelo1, 3)
```

*En el Gráfico la línea roja debe seguir una tendencia horizontal.* 


```{r message=FALSE, warning=FALSE}
library(lmtest)
bptest(modelo1)
```
*Homocedasticidad es que la varianza de los residuos es constante a lo largo del modelo.*

No hay heterocedasticidad, debido a que el p-values es 0.1149, mayor a 0.05.


**NO MULTICOLINEALIDAD**

```{r message=FALSE, warning=FALSE}
library(DescTools)
VIF(modelo1)
```

Valores > 5 indican presencia de multicolinealidad por lo que no hay multicolinealidad.

**INDEPENDENCIA DE RESIDUOS**
```{r message=FALSE, warning=FALSE}
#Default
library(car)
durbinWatsonTest(modelo1)
```
*Durbin Watson: Las hipótesis son:*
*- H0: Los residuos son independientes.*

*- H1: Los residuos no son independientes.*

Si cumplimos.


**Cumplimos el supuesto de homocedasticidad, no multicolinealidad e independencia de residuos.**



## **MODELO 2**

### **SUPUESTOS:**

*ANALIZANDO EL MODELO 2 SIN FACTOR 2:*

```{r message=FALSE, warning=FALSE}
library(lm.beta)
modelo2$coefficients
```

**LINEALIDAD**
```{r message=FALSE, warning=FALSE}
library(ggfortify)
plot(modelo2,1)
autoplot(modelo2,1)
```
```{r}
cor.test(DL$Salario, DL$factor1)
cor.test(DL$Salario, DL$TasaMigracion)
cor.test(DL$Salario, DL$Desempleo) #no funciona
cor.test(DL$Salario, DL$Crecimientopob)
```
**DL$Salario and DL$factor1:**
- P-value = 1.168e-10, si hay linealidad  

**DL$Salario and DL$TasaMigracion:**
- P-value = 0.03079, si hay linealidad

**DL$Salario and DL$Desempleo:**
- P-value = 0.4505, no hay linealidad

**DL$Salario and DL$Crecimientopob:**
- P-value = 3.057e-07, si hay linealidad


**NORMALIDAD** 
```{r}
shapiro.test(modelo2$resid)
```
*- H0: Es normal*

*- H1: No es normal*

- No hay normalidad de residuos.

**HOMOCEDASTICIDAD**

```{r}
plot(modelo2, 3)
```
```{r message=FALSE, warning=FALSE}
library(lmtest)
bptest(modelo2)
```
*- H0: El modelo es homocedástico*

*- H1: El modelo es heterocedástico*


No hay heterocedasticidad.

**NO MULTICOLENALIDAD**
```{r message=FALSE, warning=FALSE}
library(DescTools)
VIF(modelo2)
```
*Valores > 5 indican presencia de multicolinealidad.*
 No hay multicolinealidad 


**INDEPENDENCIA DE RESIDUOS**
```{r message=FALSE, warning=FALSE}
#Default
library(car)
durbinWatsonTest(modelo2)
```
*Durbin Watson: Las hipótesis son:*
*- H0: Los residuos son independientes*

*- H1: Los residuos no son independientes*

Si hay independencia de residuos.


**Se cumple con homocedasticidad, no multicolinealidad, si independencia de residuos.**


## **MODELO 3**


### **SUPUESTOS:**

Para este modelo se probarán con todas las variables 
```{r}
modelo3= lm(Salario ~ Migracion + Tasaalfabetizacion + PBI + Educaterciaria + Educsecun + Esperanzavida + Desempleo + Crecimientopob + Electricidad, DL)
summary(modelo3)
```
```{r message=FALSE, warning=FALSE}
library(lm.beta)
modelo3$coefficients
```

**LINEALIDAD**
```{r message=FALSE, warning=FALSE}
library(ggfortify)
plot(modelo3,1)
autoplot(modelo3,1)
```

**NORMALIDAD** 
```{r}
shapiro.test(modelo3$resid)
```
*- H0: Es normal*

*- H1: No es normal*

-No hay normalidad de residuos.

**HOMOCEDASTICIDAD**

```{r}
plot(modelo3, 3)
```
```{r message=FALSE, warning=FALSE}
library(lmtest)
bptest(modelo3)
```
*- H0: El modelo es homocedástico*

*- H1: El modelo es heterocedástico*

*Si el pvalor es menor a 0.05 entonces el modelo es heterocedástico.*
No hay heterocedasticidad.

**NO MULTICOLENALIDAD**
```{r message=FALSE, warning=FALSE}
library(DescTools)
VIF(modelo3)
```
*Valores > 5 indican presencia de multicolinealidad.*
No hay multicolinealidad


**INDEPENDENCIA DE RESIDUOS**
```{r message=FALSE, warning=FALSE}
#Default
library(car)
durbinWatsonTest(modelo3)
```
*Durbin Watson: Las hipótesis son:*
*- H0: Los residuos son independientes*

*- H1: Los residuos no son independientes*

Si hay independencia de residuos.

## **COMPARAMOS LOS MODELOS** 

```{r message=FALSE, warning=FALSE}
library(stargazer)
stargazer(modelo1, modelo2, modelo3, type = "text")
```
- El factor 1 es significativo para predecir el salario promedio.


- R cuadrado: es más alto en el modelo 3.



```{r}
anova(modelo1, modelo2, modelo3)
```

- El modelo 2 presenta mejoras significativas respecto al modelo 1, según la prueba ANOVA.

## **CONCLUSIONES**

El análisis de regresión lineal múltiple puede proporcionar información valiosa sobre la relación entre las variables independientes y la variable dependiente. En este caso, se ha encontrado que la tasa de alfabetización está positivamente relacionada con el salario promedio. Esto significa que los países con una alta tasa de alfabetización tienden a tener salarios más altos en promedio. Esta relación puede ser atribuida a una mayor capacitación y habilidades de la población. Los países con tasas de alfabetización más altas suelen tener poblaciones más educadas, lo que puede conducir a una fuerza laboral más capacitada y productiva. A su vez, esto puede aumentar la demanda de trabajadores calificados y hacer que los salarios sean más altos. Además, una mayor tasa de alfabetización también puede estar relacionada con una mayor capacidad para adaptarse a los cambios en el mercado laboral y en la economía en general. Esto puede permitir a los trabajadores mantenerse al día con las nuevas tecnologías y habilidades, lo que puede mejorar su productividad y, por lo tanto, aumentar sus salarios.

También se ha encontrado una relación positiva entre la esperanza de vida y el salario promedio. Esto sugiere que los países con una esperanza de vida más alta generalmente tienen salarios más altos en promedio. Asimismo, puede ser interpretada como un indicador del nivel de desarrollo socioeconómico de un país. Los países con una esperanza de vida más alta suelen tener sistemas de salud más efectivos, mejores condiciones de vida y un mayor acceso a oportunidades laborales. Esto puede conducir a una población más saludable y productiva, lo que a su vez puede aumentar la demanda de trabajadores calificados y hacer que los salarios sean más altos. Además, una mayor esperanza de vida también puede estar relacionada con una mayor estabilidad política y social. Los países con una esperanza de vida más alta tienden a tener sistemas políticos más estables y menos conflictivos, lo que puede crear un ambiente más favorable para la inversión y el crecimiento económico. Esto a su vez puede aumentar la demanda de trabajadores y hacer que los salarios sean más altos.

Por último, otra variable que se ha encontrado que está positivamente relacionada con el salario promedio es el acceso a la electricidad. Los países con mayor acceso a la electricidad tienden a tener salarios más altos en promedio. Esto se debe a que el acceso a la electricidad es fundamental para el funcionamiento de las industrias y empresas, lo que genera empleo y mejores remuneraciones. Además, el acceso a la electricidad también puede mejorar la calidad de vida de la población, al proporcionar iluminación, calefacción y refrigeración, así como acceso a tecnologías modernas y herramientas eléctricas. Además, el acceso a la electricidad también puede estar relacionado con una mayor inversión en infraestructura y tecnología. Los países con mayor acceso a la electricidad tienden a tener sistemas de energía más avanzados y eficientes, lo que puede mejorar la productividad y la competitividad de las empresas. Esto a su vez puede aumentar la demanda de trabajadores calificados y hacer que los salarios sean más altos.

Cabe destacar que después de analizar diversas alternativas de regresiones lineales utilizando las diversas variables que consideramos y explicamos previamente, decidimos quedarnos con la regresión lineal múltiple “Modelo 2”. 

Si bien nuestro modelo 3 frente a nuestro modelo 2 tiene un ligero valor superior respecto a la predicción que nos brinda el R ajustado, analizamos que la mayor cantidad de las variables, muchas de ellas por separado, no tienen ningún tipo de significancia; en cambio en nuestro modelo 2 utilizamos factores, previamente evaluados con un análisis factorial exploratorio, que ya albergan las variables que mayor aporte dan a nuestro modelo.  Así mismo,  nuestro modelo 2 nos muestra un P.valor superior, lo que determina mayor significancia de nuestro conjuntos de variables hechas factores.  

Por ende, el último modelo “Modelo 2” elegido nos ayuda a acercarnos más a las variables conjuntas que tienen mayor impacto explicativo de nuestra pregunta de investigación sobre cuáles son las causas de las diferencias salariales en el mundo

En resumen, variables como el PBI, el crecimiento de la población, el desempleo, la educación secundaria, la educación terciaria, el empleo de mujeres y la tasa de migración, también pueden tener un impacto significativo en el salario promedio. Por ejemplo, se ha encontrado que el PBI está positivamente relacionado con el salario promedio, lo que sugiere que los países con una economía más fuerte tienden a tener salarios más altos. Además, el empleo de mujeres también puede estar relacionado con salarios más altos, ya que esto puede aumentar la oferta de trabajadores y reducir la discriminación salarial. Por otro lado, se ha encontrado que el desempleo y la tasa de migración están negativamente relacionados con el salario promedio. Esto sugiere que los países con altas tasas de desempleo y migración tienden a tener salarios más bajos en promedio.
Este análisis estadístico nos ha permitido revelar, que múltiples factores pueden influir en el promedio de salario mundial. Estos hallazgos destacan la importancia de abordar estas variables en los esfuerzos por mejorar los niveles de salario a nivel global, y sugieren que invertir en educación, atención médica, desarrollo de infraestructura eléctrica, economía fuerte y reducción del desempleo y la migración puede tener un impacto positivo en los salarios de las personas en todo el mundo.



## **BIBLIOGRAFÍA**


Anders Wivel , Caroline Howard Grøn, Charismatic leadership in foreign policy, International Affairs, Volume 97, Issue 2, March 2021, Pages 365–383, https://doi.org/10.1093/ia/iiaa223 


Cavallo & otros (2021) Oportunidades para un mayor crecimiento sostenible tras la pandemia. BID.


Caribe, C. E. P. A. L. Y. E. (2019, 28 febrero). CEPAL: Impacto social, económico y cultural de la migración es notoriamente positivo para los países de origen y destino. https://www.cepal.org/es/comunicados/cepal-impacto-social-economico-cultural-la-migracion-es-notoriamente-positivo-paises


Empleos y Desarrollo. (s. f.). World Bank. https://www.bancomundial.org/es/topic/jobsanddevelopment/overview


Informe de la OIM sobre las migraciones en el mundo: Aumento del desplazamiento mundial pese a las restricciones a la movilidad por la COVID-19. (s. f.). International Organization for Migration. https://www.iom.int/es/news/informe-de-la-oim-sobre-las-migraciones-en-el-mundo-aumento-del-desplazamiento-mundial-pese-las-restricciones-la-movilidad-por-la-covid-19#:~:text=De%20acuerdo%20con%20el%20Informe,3%2C6%20%25%20de%20la%20poblaci%C3%B3n 


Modi, V. & Figueroa, H. Objetivo de Desarrollo Sostenible para la energía y la tecnología de la información y las comunicaciones. ONU.


World Health Organization: WHO. (2016, 19 mayo). La esperanza de vida ha aumentado en 5 años desde el año 2000, pero persisten las desigualdades sanitarias. Organización Mundial de la Salud. https://www.who.int/es/news/item/19-05-2016-life-expectancy-increased-by-5-years-since-2000-but-health-inequalities-persist


OIT (2012) A medida que crece la población, también aumentan las necesidades de competencias. 
