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

















