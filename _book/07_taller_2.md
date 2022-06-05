# Taller II

## Introducción

Esta última parte del curso tiene por intención realizar un proceso de análisis de datos en base a los conceptos mostrados y explicados en las 3 últimas sesiones. Mediante una serie de instrucciones y la posibilidad de consultar pistas/ayudas referenciadas, se busca que el estudiante pueda aplicar conceptos y desarrolle las habilidades procedimentales para lograr dar solución a los problemas planteados.

## Instrucciones

Para este proyecto usaremos las base de datos disponibles a partir del estudio [Tomographic score (RAD-Covid Score) to assess the clinical severity of the novel coronavirus infection](https://www.bjid.org.br/en-tomographic-score-rad-covid-score-assess-articulo-S1413867021000684) de Guimarães y colaboradores. Las bases de datos en formato excel (`.xlsx`) se encuentran disponibles en el repositorio [figshare](https://figshare.com/articles/dataset/Clinical_data_and_radiological_severity_score_RAD-Covid_Score_of_chest_CT_scans_from_COVID-19_patients_/12675098).

<img src="img/clinical_data_rx_view.png" width="90%" style="display: block; margin: auto;" />

El repositorio contiene 3 conjuntos de datos:

- El primero (`CLIN LAB DATA RAD-Covid (1).xlsx`) presenta la información socio-demográfica, las comorbilidades, y el resultado de la hospitalización (recuperado/muerto) de los pacientes con COVID-19
- El segundo (`consensus RADIOLOGISTS CT AVAL. PATTERNS AND DISTRIBUTION OF LESIONS (1).xlsx`) contiene los patrones y distribuciones de las lesiones encontradas en las tomografías
- Y el tercero (`RAD-COVID SCORE AGREEMENT (1).xlsx`) contiene información sobre la severidad de los resultados de las tomografías.



1. En un nuevo proyecto de rstudio y en un archivo **Rmarkdown** (`.Rmd`), realizar la importación de 2 conjuntos de datos. La primera base a importar será la que contiene información socio-demográfica, comorbilidades y resultado de hospitalización; y la segunda base a importar será únicamente la de la segunda pestaña (`Radiologist 2`) de la base de datos que contiene la información sobre la severidad de la tomografía. 

> Recuerda que para no batallar con los nombres de las variables, podemos usar `janitor::clean_names()`

<details>
  <summary>Ayuda 1</summary>
  <p>Recordar que estamos trabajando con archivos `.xlsx`, la función `read_excel()` permite leer archivos con esta extensión</p>
</details>
<details>
  <summary>Ayuda 2</summary>
  <p>Considerar el argumento `sheet` de la función `read_excel()` para leer una pestaña en particular.</p>
</details>
2. Ambas bases de datos contienen información de los mismos pacientes. Es por ello que, en esta ocasión, será necesario que ambas bases de datos se encuentren unificadas para poder interactuar con toda la información.
<details>
  <summary>Ayuda 1</summary>
  <p>La familia de funciones `*_join()` sirve para unir registros de dos tablas por una columna en común (key).</p>
</details>
<details>
  <summary>Ayuda 2</summary>
  <p>La función `left_join()` une los registros de una tabla sobre otra tabla manteniendo todos los registros de la primera tabla.</p>
</details>
3. Se desea tener un dataframe que solo contenga la información del id del paciente (`patient`), de la severidad de los casos (`rad_covid_score`, `ct_date`), el resultado de la hospitalización de todos los pacientes (`result`), evolución (`death`), así  como los datos sociodemográficos (género[`gender`] y edad[`age`]).
<details>
  <summary>Ayuda 1</summary>
  <p>La función `select()` es usada para seleccionar las variables con las que deseamos trabajar.</p>
</details>
<details>
  <summary>Ayuda 2</summary>
  <p>Almacenar la base en nuevo objeto para poder realizar las operaciones posteriores.</p>
</details>
4. Se necesita tener un conjunto de datos que solo contenga la información de los pacientes de género femenino que sean menores de 50 años de edad y que tengan un caso de COVID-19 leve (<25%).
<details>
  <summary>Ayuda 1</summary>
  <p>La función `filter()` sirve para filtrar registros de acuerdo a ciertos criterios.</p>
</details>
<details>
  <summary>Ayuda 2</summary>
  <p>Se pueden hacer múltiples filtros dentro de la misma función utilizando los operadores lógicos correspondientes (**&**, **|**).</p>
</details>
5. La información sobre los resultados y muertes por paciente se encuentran completamente en mayúsculas. Si se desea generar tablas tipo reporte o luego elaborar gráficos en base a estas variables, sería mucho más ordenado que sus valores se encuentren en formato oración, es decir que si inicialmente se indica `POSITIVE FOR COVID`, debería indicarse como `Positive for covid`.
<details>
  <summary>Ayuda 1</summary>
  <p>La función `str_to_sentence()` de la librería stringr puede ser útil.</p>
</details>
6. Generar una tabla de reporte que informe sobre el tiempo promedio en horas o días que existe entre la fecha toma de radiología y la fecha de aparición de síntomas para aquellos que resultaron positivos en COVID-19 de acuerdo a su nivel de serveridad identificado por RX (RAD-Covid Score).
<details>
  <summary>Ayuda 1</summary>
  <p>Para diferenciar entre fechas, se puede aplicar una resta simple dentro de un `mutate()`</p>
</details>
<details>
  <summary>Ayuda 2</summary>
  <p>Cuando se requiere tener un resumen de datos, lo ideal es usar `group_by()` y `summarise()` </p>
</details>

> **¡Reto!**

7. Se desea visualizar la distribución de casos positivos y negativos por COVID (barplot) en cada quincena de los meses de marzo y abril del 2020.
<details>
  <summary>Ayuda 1</summary>
  <p>Las funciones `year()`, `month()` y `day()` permiten extraer información específica de una variable en formato fecha.</p>
</details>
<details>
  <summary>Ayuda 2</summary>
  <p>La función `case_when()` y `mutate()` permite categorizar una variable en base a una condición. </p>
</details>

¡Éxtitos en el taller!
