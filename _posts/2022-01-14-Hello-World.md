---
layout: post
title: Segundo trabajo Técnicas de aprendizaje estadístico (TAE)
---

# Planteamiento del problema.

Se busca construir un modelo de regresión que ayude a predecir el número de vehículos que se registrarán
diariamente en el Registro Único Nacional de Tránsito (RUNT) para el 2018. Para esto se tienen los datos
hisotóricos de registros de autos desde el 01/01/2012 hasta el 31/12/2017.

# Datos

![_config.yml]({{ site.baseurl }}/images/img1.PNG)


Los datos principales constan de las columnas Fecha y Unidades, adicionalmente se les agregó las columnas
dia_semana (nombre del día de la semana correspondiente a la fecha) y mes (nombre del mes correspondiente a la fecha). esto con ayuda de Excel.Otras variables serán consideradas para ayudar a explicar el
comportamiento de los datos, estás variables serán derivadas de la variable fecha.

Veamos como se comportan las unidades registradas para cada una de las variables consideradas hata ahora.


## Unidades registradas por día del año

![_config.yml]({{ site.baseurl }}/images/img2.PNG)

Se pueden ver unos picos que representan una gran cantidad de autos registrados a finales y comienzo de
mes, sí parece haber una tendencia relacioanda con el tiempo.

## Unidades registradas por mes

![_config.yml]({{ site.baseurl }}/images/img3.PNG)

Al parecer no hay diferencias significativas de unidades registradas por mes para cada año ,pero se ve que
en el mes de Diciembre se obtienen los valores más altos y la variabilidad más alta.

## Unidades registradas por día del mes

![_config.yml]({{ site.baseurl }}/images/img4.PNG)

Se puede ver no hay diferencia entre las unidades registradas para los días de los meses para cada uno de los
años, sinembargo se ve que en los últimos días de los meses se alcanzan los valores más altos.

## Unidades registradas por semana

![_config.yml]({{ site.baseurl }}/images/img5.PNG)

Se puede ver que los fines de semana son los días que menos autos se registran, eso puede deberse a que le
Domingo es un día de descanso y que los sábados muchas personas trabajan hasta tempranas horas de la
tarde. A partir de esto se crea una variable llamada finde (Fin de semana) que pudiera ayudar a aexplciar
el comportamiento de los registros de las unidades.


## Unidades registradas en semana y en fin de semana

![_config.yml]({{ site.baseurl }}/images/img6.PNG)

## Modelo de regresión

Con las variables anteriormente definidas se buscará crear un modelo de regresión que pueda explicar y
posteriormente predecir las unidades de autos que se registran.

Para encontrar el mejor modelo de regresión se utiliza la regresión Stepwise, la cual nos permite escoger
las mejores variables capaces de explicar el comportamiento de las unidades de autos registrados. El mejor
modelo con el conjunto de variables indicado es escogido con el criterio AIC.

• Primero se intentará predecir y explicar las unidades registradas que corresponden a los años 2012
hasta 2016

• Segundo se intentará predecir las unidades registradas que corresponden al año 2017 para ver como
predice el modelo

• Tercero se intentará predecir las unidades registradas para los días comprendidos entre el 01/01/2018
y el 30/06/2018.

Para esto se dividen los datos en dos grupos, datos desde los años 2012 hasta el 2016 (registros_1216) y los
datos que corresponden al año 2017 (registros_17), para intentar predecir los datos del primer semestre de
2018 se utilizarán todos los datos.

registros_1216 <- registros[1:1827,]
registros_17 <- registros[1828:2192,]

## Regresión Stepwise

### Paso 1. Se crea un modelo de regresión lineal sin variables

![_config.yml]({{ site.baseurl }}/images/img7.PNG)

El modelo vacío (sólo con el intercepto), tiene una desviación estandar de σ = 552.2. Como no tiene variables
explicativas no se calcula el R2

### Paso 2. Se crea un modelo de regresión lineal con todas las variables que se puedan considerar

En este caso todas las variables son indicadoras puesto que los datos carecen de variables numéricas.
![_config.yml]({{ site.baseurl }}/images/img8.PNG)

La desviación estandar del modelo con todas las variables es de σ = 259.30, y un R2 = 0.83, los que significa
que las covariables del modelo explican un 83% de la variabilidad de las unidades de autos registradas, y con
un R2

Ajustado = 0.78 que está muy cerca del R2
(5%), lo que apoya la veracidad de lo concluído con el R2

### Paso 3. Regresión Stepwise

La regresión Stepwise o paso a paso genera el mejor modelo con las variables más significativas usando la
regresión hacía atrás (o Backward) y la regresión hacía adelante (o Forward). Escoge el mejor modelo con
el criterio AIC

![_config.yml]({{ site.baseurl }}/images/img9.PNG)

![_config.yml]({{ site.baseurl }}/images/img10.PNG)

## El modelo final obtenido es:

![_config.yml]({{ site.baseurl }}/images/img11.PNG)


La desviación estandar del modelo con todas las variables es de σ = 259.30, y un R2 = 0.83, los que significa
que las covariables del modelo explican un 83% de la variabilidad de las unidades de autos registradas, y con
un R2

Ajustado = 0.78. Son los mismos resultados obtenidos que cuando utilizamos todas las variables, con la
diferencia que este modelo no tiene encuenta la variable finde, la cual no aportaba información significativa
para explicar las unidades registradas.

## Supuestos del modelo


![_config.yml]({{ site.baseurl }}/images/img12.PNG)

## Estimación de los datos


![_config.yml]({{ site.baseurl }}/images/img13.PNG)

Vemos que entre los datos existen valores negativos, lo cual no tienen ninguna interpretación pues la variable
Unidad es una cantidad entera que no puede ser negativa, por lo tanto para un mejor ajuste se opta por
cambiar los valores negativos a cero. En el otro gráfico podemos ver que hay cierta relación entre los valores
estimados y las Unidades reales de la base de datos que contiene las unidades registradas desde el 2012 hasta
el 2016.

El MSE es de: 52070.35.


## Estimación de los datos con ajuste en los datos negativos

![_config.yml]({{ site.baseurl }}/images/img14.PNG)

El MSE es de: 48900.54, los que significa que el error cuadrático medio se reduce 3169.81 unidades cuadradas
con respecto al MSE anterior de los datos estimados que contenían los negativos.

## Predicción para 2017

Aquí se corrige de una vez el problema de los datos estimados negativos, haciéndolos igual a cero.

![_config.yml]({{ site.baseurl }}/images/img15.PNG)

Los datos no parecen seguir una linea recta de 45° con respecto al eje X, al parecer las estimaciones subestiman
los valores reales en su mayoría. Sinembargo fue le mejor modelo hallado.

![_config.yml]({{ site.baseurl }}/images/img16.PNG)

El MSE de los errores calculados para la base de datos de unidades registradas para el 2017 es de: 140145.4.
Casi el doble que el MSE para los datos con los que se hicieron el modelo.














