# Sesión 03

### Función Glimpse 

Mediante la función:


```r
glimpse()
```

#### ¿Para que sirve?

- Versión transpuesta de print

- Ayuda a visualizar la mayor cantidad de datos de muchas columnas.

- Muestra el nombre de la variable junto con una designación de tipo de variable.

*__Observación:__*

- Recordar importar el paquete tidyverse:


```r
library(tidyverse)
#> ── Attaching packages ─────────────────── tidyverse 1.3.1 ──
#> ✔ ggplot2 3.3.6     ✔ purrr   0.3.4
#> ✔ tibble  3.1.7     ✔ dplyr   1.0.9
#> ✔ tidyr   1.2.0     ✔ stringr 1.4.0
#> ✔ readr   2.1.2     ✔ forcats 0.5.1
#> ── Conflicts ────────────────────── tidyverse_conflicts() ──
#> ✖ dplyr::filter() masks stats::filter()
#> ✖ dplyr::lag()    masks stats::lag()
library(dplyr)
```

- Para el ejemplo se recomienda installar el siguiente paquete:


```r
install.packages("nycflights13")
```

#### Ejemplo 

Así habitualmente observamos la data:


```r
nycflights13::flights
#> # A tibble: 336,776 × 19
#>     year month   day dep_time sched_dep_time dep_delay
#>    <int> <int> <int>    <int>          <int>     <dbl>
#>  1  2013     1     1      517            515         2
#>  2  2013     1     1      533            529         4
#>  3  2013     1     1      542            540         2
#>  4  2013     1     1      544            545        -1
#>  5  2013     1     1      554            600        -6
#>  6  2013     1     1      554            558        -4
#>  7  2013     1     1      555            600        -5
#>  8  2013     1     1      557            600        -3
#>  9  2013     1     1      557            600        -3
#> 10  2013     1     1      558            600        -2
#> # … with 336,766 more rows, and 13 more variables:
#> #   arr_time <int>, sched_arr_time <int>, arr_delay <dbl>,
#> #   carrier <chr>, flight <int>, tailnum <chr>,
#> #   origin <chr>, dest <chr>, air_time <dbl>,
#> #   distance <dbl>, hour <dbl>, minute <dbl>,
#> #   time_hour <dttm>
```

Con `glimpse()`, podrás tener un vistazo rápido de la estructura de los datos:


```r
glimpse(nycflights13::flights)
#> Rows: 336,776
#> Columns: 19
#> $ year           <int> 2013, 2013, 2013, 2013, 2013, 2013,…
#> $ month          <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
#> $ day            <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
#> $ dep_time       <int> 517, 533, 542, 544, 554, 554, 555, …
#> $ sched_dep_time <int> 515, 529, 540, 545, 600, 558, 600, …
#> $ dep_delay      <dbl> 2, 4, 2, -1, -6, -4, -5, -3, -3, -2…
#> $ arr_time       <int> 830, 850, 923, 1004, 812, 740, 913,…
#> $ sched_arr_time <int> 819, 830, 850, 1022, 837, 728, 854,…
#> $ arr_delay      <dbl> 11, 20, 33, -18, -25, 12, 19, -14, …
#> $ carrier        <chr> "UA", "UA", "AA", "B6", "DL", "UA",…
#> $ flight         <int> 1545, 1714, 1141, 725, 461, 1696, 5…
#> $ tailnum        <chr> "N14228", "N24211", "N619AA", "N804…
#> $ origin         <chr> "EWR", "LGA", "JFK", "JFK", "LGA", …
#> $ dest           <chr> "IAH", "IAH", "MIA", "BQN", "ATL", …
#> $ air_time       <dbl> 227, 227, 160, 183, 116, 150, 158, …
#> $ distance       <dbl> 1400, 1416, 1089, 1576, 762, 719, 1…
#> $ hour           <dbl> 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6,…
#> $ minute         <dbl> 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, …
#> $ time_hour      <dttm> 2013-01-01 05:00:00, 2013-01-01 05…
```

Generalmente la vista de `glimpse()` es suficientemente ordenada para poder observar la estructura de la data sin problemas. Pero también se puede usar el argumento `width` para poder especificar ello.

```
glimpse(nycflights13::flights, width = 90)
```

### Operador Pipe %>% 

Útil para concatenar múltiples operaciones en `dplyr`.

Atajo de Teclado:
<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_03/img/atajo_pipe.svg" width="100%"/>

En algunas ocasiones cuando se desea aplicar una función de forma anidada puede resultar ilegible o difícil de comprender, aquí un ejemplo.


```r
tabla(formato(coeficiente(data)))
```


El operador `%>%` nos permite escribir de una secuencia de operaciones de izquierda a derecha :

```r
coeficiente(data) %>% formato() %>% tabla()
```

Esta forma de programar hace que los códigos sean más legibles por muchos usarios y más si
empleamos la siguiente estructura.


```r
coeficiente(data) %>% 
  formato() %>% 
  tabla()
```

### Función mutate()

Con `mutate()` podemos realizar modificaciones en las variables. Por ej. sumar variables, o modificarlas de alguna manera (transformar a porcentaje, multiplicarlas por alguna constante, etc.). Estas modificaciones pueden realizarse:
 
 - Creando una nueva variable a partir de otras ya existentes.
 
 - Modificar una variable existente en la misma variable.


#### Ejemplo: 


```r
library(tidyverse)
df %>% 
  mutate(
    New_var = var*2
  )
```

*__Explicación:__*

*En una data llamada df se estaría aplicando la función mutate creando una variable llamada New_var a partir de otra variable llamada var que está siendo multiplicada por 2.*


## Uso práctico de mutate()

### Reconocimiento de Base de datos 

Para esta ejemplificación usaremos la base de datos del ECA sobre la [erradicación de la infección por Helicobácter Pylori](https://www.nature.com/articles/s41598-018-27482-2) explicado en la [sesión 02](https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_02/#14).



```r
trial_data <- readxl::read_excel("_data/researchdata.xlsx")
trial_data
#> # A tibble: 400 × 10
#>    `Patient number` `Baseline 13C-UBT` `Randomized group`
#>               <dbl> <chr>              <chr>             
#>  1                1 Positive           group B           
#>  2                2 Positive           group A           
#>  3                3 Positive           group B           
#>  4                4 Positive           group A           
#>  5                5 Positive           group A           
#>  6                6 Positive           group A           
#>  7                7 Positive           group B           
#>  8                8 Positive           group A           
#>  9                9 Positive           group A           
#> 10               10 Positive           group A           
#> # … with 390 more rows, and 7 more variables:
#> #   `Follow-up13C-UBT (4 weeks after therapy)` <chr>,
#> #   `adverse drug reactions` <chr>,
#> #   `adverse drug reactions  content` <chr>,
#> #   `Adverse drug reaction classified` <chr>,
#> #   `Complete the study` <chr>, `Uncompleted Reason` <chr>,
#> #   `per protocol analysis` <chr>
```


```r
glimpse(trial_data)
#> Rows: 400
#> Columns: 10
#> $ `Patient number`                           <dbl> 1, 2, 3…
#> $ `Baseline 13C-UBT`                         <chr> "Positi…
#> $ `Randomized group`                         <chr> "group …
#> $ `Follow-up13C-UBT (4 weeks after therapy)` <chr> "Negati…
#> $ `adverse drug reactions`                   <chr> "No", "…
#> $ `adverse drug reactions  content`          <chr> "NA", "…
#> $ `Adverse drug reaction classified`         <chr> "NA", "…
#> $ `Complete the study`                       <chr> "Yes", …
#> $ `Uncompleted Reason`                       <chr> "NA", "…
#> $ `per protocol analysis`                    <chr> "Yes", …
```

### Janitor 

En algunas ocasiones las base de datos contienen nombres de variables muy largas o que incluso pueden contener espacios o símbolos. Una forma sencilla de solucionar ello es mediante el uso de la función `clean_names()` del paquete `janitor`.

*Observación:*
- Para instalar el paquete janitor,empleamos la siguiente función:


```r
install.packages("janitor")
```


```r
trial_data <- trial_data %>% 
  janitor::clean_names() 
trial_data
#> # A tibble: 400 × 10
#>    patient_number baseline_13c_ubt randomized_group
#>             <dbl> <chr>            <chr>           
#>  1              1 Positive         group B         
#>  2              2 Positive         group A         
#>  3              3 Positive         group B         
#>  4              4 Positive         group A         
#>  5              5 Positive         group A         
#>  6              6 Positive         group A         
#>  7              7 Positive         group B         
#>  8              8 Positive         group A         
#>  9              9 Positive         group A         
#> 10             10 Positive         group A         
#> # … with 390 more rows, and 7 more variables:
#> #   follow_up13c_ubt_4_weeks_after_therapy <chr>,
#> #   adverse_drug_reactions <chr>,
#> #   adverse_drug_reactions_content <chr>,
#> #   adverse_drug_reaction_classified <chr>,
#> #   complete_the_study <chr>, uncompleted_reason <chr>,
#> #   per_protocol_analysis <chr>
```

### Rename 

A pesar de que `janitor::clean_names()` nos proporciona una gran solución para el formateo de nombres de variables que tienen espacios y/o símbolos, a veces podría ser necesario modificar específicamente el nombre de algunas variables. Para ello usaremos la función rename de la siguiente manera:


```r
trial_data <- trial_data %>% 
  rename(
    follow_4_weeks = follow_up13c_ubt_4_weeks_after_therapy
  )
trial_data
#> # A tibble: 400 × 10
#>    patient_number baseline_13c_ubt randomized_group
#>             <dbl> <chr>            <chr>           
#>  1              1 Positive         group B         
#>  2              2 Positive         group A         
#>  3              3 Positive         group B         
#>  4              4 Positive         group A         
#>  5              5 Positive         group A         
#>  6              6 Positive         group A         
#>  7              7 Positive         group B         
#>  8              8 Positive         group A         
#>  9              9 Positive         group A         
#> 10             10 Positive         group A         
#> # … with 390 more rows, and 7 more variables:
#> #   follow_4_weeks <chr>, adverse_drug_reactions <chr>,
#> #   adverse_drug_reactions_content <chr>,
#> #   adverse_drug_reaction_classified <chr>,
#> #   complete_the_study <chr>, uncompleted_reason <chr>,
#> #   per_protocol_analysis <chr>
```

### Mutate I 

Una de las primeras cosas que podemos hacer con `mutate` durante el primer contacto con la data que trabajemos es:

- Configurar variables `ID` como **texto** (`character`).

- Configurar variables como **factores**.

- Configurar respuestas `NA` en caso tengan alguna otra codificación.

1. Configurar la variable **ID**


```r
trial_data %>% 
  mutate(
    patient_number = as.character(patient_number)
  )
#> # A tibble: 400 × 10
#>    patient_number baseline_13c_ubt randomized_group
#>    <chr>          <chr>            <chr>           
#>  1 1              Positive         group B         
#>  2 2              Positive         group A         
#>  3 3              Positive         group B         
#>  4 4              Positive         group A         
#>  5 5              Positive         group A         
#>  6 6              Positive         group A         
#>  7 7              Positive         group B         
#>  8 8              Positive         group A         
#>  9 9              Positive         group A         
#> 10 10             Positive         group A         
#> # … with 390 more rows, and 7 more variables:
#> #   follow_4_weeks <chr>, adverse_drug_reactions <chr>,
#> #   adverse_drug_reactions_content <chr>,
#> #   adverse_drug_reaction_classified <chr>,
#> #   complete_the_study <chr>, uncompleted_reason <chr>,
#> #   per_protocol_analysis <chr>
```

### Mutate II

2. Configurar **factores**


```r
trial_data %>% 
  mutate(
    randomized_group = factor(randomized_group),
    complete_the_study = factor(complete_the_study)
  )
#> # A tibble: 400 × 10
#>    patient_number baseline_13c_ubt randomized_group
#>             <dbl> <chr>            <fct>           
#>  1              1 Positive         group B         
#>  2              2 Positive         group A         
#>  3              3 Positive         group B         
#>  4              4 Positive         group A         
#>  5              5 Positive         group A         
#>  6              6 Positive         group A         
#>  7              7 Positive         group B         
#>  8              8 Positive         group A         
#>  9              9 Positive         group A         
#> 10             10 Positive         group A         
#> # … with 390 more rows, and 7 more variables:
#> #   follow_4_weeks <chr>, adverse_drug_reactions <chr>,
#> #   adverse_drug_reactions_content <chr>,
#> #   adverse_drug_reaction_classified <chr>,
#> #   complete_the_study <fct>, uncompleted_reason <chr>,
#> #   per_protocol_analysis <chr>
```

3. Configurar respuestas `NA`

Para reemplazar respuestas dependiendo de una condición en particular se puede utilizar la función `case_when()` dentro de un `mutate()`.


```r
trial_data %>% 
  mutate(
    Var = case_when(
      Var == "Text" ~ "New_Text", 
      TRUE ~ Var
    )
  )
```

De esta manera en la variable `Var` se reemplazará todos los casos que registren el dato de **Text** por **New_Text**   .

### Uso de count 

La función count es bastante sencilla y poderosa a la vez. Permite obtener una tabla en formato tibble que representará las frecuencias (cantidades n) de una o múltiples variables en específico.


```r
trial_data %>% 
  count(adverse_drug_reactions)
#> # A tibble: 4 × 2
#>   adverse_drug_reactions     n
#>   <chr>                  <int>
#> 1 NA                        10
#> 2 No                       295
#> 3 Yes                       94
#> 4 <NA>                       1
```

La tabla generada muestra que cantidad de personas han tenido reacciones adversas a los medicamentos ya sea en el Grupo A o B. Sin embargo, también se aprecia que hay **2** respuestas que indican la presencia de datos vacíos: `NA` y `<NA>`. El primero está codificado directamente como texto (`character`) y sel segudo es un `NA` real, es decir que comunica la ausencia de un dato.

### Uso de mutate() y case_when()

#### Explicación previa del NA

Al importar las bases de datos dentro de R, la gran mayoría de funciones (como `read_excel()`) interpretarán los valors en blanco o celdas vacías como reales `NA`. Sin embargo si en las celdas se ha llenado explícitamente el texto `NA` o se ha usado alguna codificación diferente, el valor de `NA` no se introducirá automáticamente y habrá que indicarlo como tal (`case_when()`).

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_03/img/view_excel_na.png" width="100%"/>


```r
trial_data %>% 
  count(adverse_drug_reactions)
#> # A tibble: 4 × 2
#>   adverse_drug_reactions     n
#>   <chr>                  <int>
#> 1 NA                        10
#> 2 No                       295
#> 3 Yes                       94
#> 4 <NA>                       1
```


#### Uso de case_when()

La función `case_when()` tiene una aplicación directa y perfecta para estos fines, en el que recodificaremos el `NA` introducido como texto a un `NA` real que sea reconocido como tal. El mismo procedimiento se utilizaría si los valores faltantes o perdidos se hubieran codificado de otra forma (ej. **777** o **999**).


Recordar que con pipe (`%>%`) podemos anidar muchas funciones en un solo bloque:


```r
trial_data %>%
  mutate(
    adverse_drug_reactions = case_when(
      adverse_drug_reactions == "NA" ~ NA_character_,
      TRUE ~ adverse_drug_reactions
    )
  ) %>% 
  count()
```

El código `TRUE ~ adverse_drug_reactions` significa que **todos los demás casos** mantendrán el valor original que el de la variable.


```
#> # A tibble: 1 × 1
#>       n
#>   <int>
#> 1   400
```


#### Advertencia

La función case_when requiere respetar de forma estricta el tipo de vector utilizado. Es decir que si se le pide recodificar una variable a número, y dentro de esa variable continúan habiendo textos, habrá un problema de no-coerción. Es por ese motivo que en el anterior ejemplo se usa NA_character en vez de únicamente NA, ya que este elemento como tal en realidad es de tipo lógico.


```r
typeof(NA)
#> [1] "logical"
```


```r
typeof(NA_character_)
#> [1] "character"
```


```r
typeof(NA_real_)
#> [1] "double"
```

### Más sobre case_when()

Anteriormente vimos como usar la función `case_when` para recategorizar/recodificar variables en base a una condición de igualdad (`==`). Sin embargo, no es la única manera. También se puede recategorizar en base a múltiples condiciones, como `%in%` (comparar con múltiples valores a la vez), `>`, `>=`, `<` y `<=`, en conjunto con `&` y `|`.


Para ejemplificar esto haremos una recategorización de la base nycflights13::flights:


```r
nycflights13::flights %>% 
  count(year, month)
#> # A tibble: 12 × 3
#>     year month     n
#>    <int> <int> <int>
#>  1  2013     1 27004
#>  2  2013     2 24951
#>  3  2013     3 28834
#>  4  2013     4 28330
#>  5  2013     5 28796
#>  6  2013     6 28243
#>  7  2013     7 29425
#>  8  2013     8 29327
#>  9  2013     9 27574
#> 10  2013    10 28889
#> 11  2013    11 27268
#> 12  2013    12 28135
```

Consideraremos del mes 1 hasta el 6 como 2013-I y a partir del mes 7, como 2013-II.


```r
nycflights13::flights %>% 
  mutate(
    year = case_when(
      month %in% 1:6 ~ "2013-I",
      TRUE ~ "2013-II"
    )
  ) %>% 
  count(year)
#> # A tibble: 2 × 2
#>   year         n
#>   <chr>    <int>
#> 1 2013-I  166158
#> 2 2013-II 170618
```

Ya que la variable `month` es de tipo `integer` (**numérica**) tenemos más formas alternativas de conseguir exactamente el mismo resultado mostrado anteriormente.


En variables numéricas, podemos directamente usar `<=` en las condiciones.


```r
nycflights13::flights %>% 
  mutate(
    year = case_when(
      month <= 6 ~ "2013-I",
      month > 6 ~ "2013-II"
    )
  ) %>% 
  count(year)
#> # A tibble: 2 × 2
#>   year         n
#>   <chr>    <int>
#> 1 2013-I  166158
#> 2 2013-II 170618
```

O directamente usar `TRUE` ~ "Condicion, para *todos los demás casos*.


```r
nycflights13::flights %>% 
  mutate(
    year = case_when(
      month <= 6 ~ "2013-I",
      TRUE ~ "2013-II"
    )
  ) %>% 
  count(year)
#> # A tibble: 2 × 2
#>   year         n
#>   <chr>    <int>
#> 1 2013-I  166158
#> 2 2013-II 170618
```

### Más usos de count() y arrange()

Ya hemos visto que `count()` es sumamente útil. Además, basta con agregar más variables dentro de sus argumentos, para que estos automáticamente ingresen a generar una tabla de frecuencias. Sin embargo, a veces puede ser necesario ordenar esos resultados, para ello usaremos `arrange()`.


```r
trial_data <- trial_data %>% 
  mutate(
    follow_4_weeks = case_when(
      follow_4_weeks == "NA" ~ NA_character_,
      TRUE ~ follow_4_weeks
    ),
    adverse_drug_reactions = case_when(
      adverse_drug_reactions == "NA" ~ NA_character_,
      TRUE ~ adverse_drug_reactions
    )
  )
```


```r
trial_data %>% 
  count(randomized_group, 
        follow_4_weeks,
        adverse_drug_reactions)
```

La función `arrange()` permitirá ordenar un objeto en base a una o múltiples variables. En caso se ejecute sobre una variable numérica, se ordenará de menor a mayor por defecto, y en caso se ejecute sobre una variable texto (**character**) se ordenará de forma alfabética, tal y como ya lo hace `count()` por defecto.

Si se desea invertir el ordenamiento, se puede utilizar la función `desc()` dentro de `arrange()`.

```
trial_data %>%
  count(randomized_group,
        follow_4_weeks,
        adverse_drug_reactions) %>%
  arrange(randomized_group,
          desc(follow_4_weeks))
```


```
#> # A tibble: 13 × 4
#>    randomized_group follow_4_weeks adverse_drug_react…     n
#>    <chr>            <chr>          <chr>               <int>
#>  1 group A          Negative       No                    124
#>  2 group A          Negative       Yes                    31
#>  3 group A          Positive       No                     27
#>  4 group A          Positive       Yes                    14
#>  5 group A          <NA>           <NA>                    4
#>  6 group B          Negative       No                    114
#>  7 group B          Negative       Yes                    41
#>  8 group B          Negative       <NA>                    4
#>  9 group B          Positive       No                     25
#> 10 group B          Positive       Yes                     8
#> 11 group B          Positive       <NA>                    2
#> 12 group B          <NA>           No                      5
#> 13 group B          <NA>           <NA>                    1
```


### Uso de slice_max()

Anteriormente conocido como `top_n()`, la función `slice_max()`, permite seleccionar cuantos casos (filas) se específique en base a una variable numérica.


```r
trial_data %>%
  count(randomized_group,
        follow_4_weeks) %>%
  slice_max(order_by = n,
            n = 2)
#> # A tibble: 2 × 3
#>   randomized_group follow_4_weeks     n
#>   <chr>            <chr>          <int>
#> 1 group B          Negative         159
#> 2 group A          Negative         155
```


### Introducción a tidydata

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_03/img/tidydata_7.jpg" width='100%'/>

Tener datos ordenados (tidydata) significa tener una BD con estructuras adecuadas, donde cada registro representa una fila, cada variable representa una columna y cada celda contiene una simple medida ([Hadley Wickham,2014](https://www.jstatsoft.org/article/view/v059i10)).

<img src='https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_03/img/tidydata_1.jpg' width='100%'/>

### Uso de pivot_longer() y pivot_wider()

Para este ejemplo usaremos una base de datos que contiene casos de personas fallecidas a causa del coranovirus a nivel de país, este dataset está alojada en el siguiente repositorio de GitHub ([click aquí](https://github.com/CSSEGISandData/COVID-19)).

<img src='https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_03/img/github_covid_1.png' width='100%' />

La función `read_csv` del paquete readr (se carga automáticamente cuando se realiza `library(tidyverse)`), permite importar archivos `csv` (data) incluso cuando el archivo está en una web.


```r
covid19 <- read_csv("https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_deaths_global.csv")
#> Rows: 285 Columns: 868
#> ── Column specification ────────────────────────────────────
#> Delimiter: ","
#> chr   (2): Province/State, Country/Region
#> dbl (866): Lat, Long, 1/22/20, 1/23/20, 1/24/20, 1/25/20...
#> 
#> ℹ Use `spec()` to retrieve the full column specification for this data.
#> ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
covid19
#> # A tibble: 285 × 868
#>    `Province/State`  `Country/Region`   Lat   Long `1/22/20`
#>    <chr>             <chr>            <dbl>  <dbl>     <dbl>
#>  1 <NA>              Afghanistan       33.9  67.7          0
#>  2 <NA>              Albania           41.2  20.2          0
#>  3 <NA>              Algeria           28.0   1.66         0
#>  4 <NA>              Andorra           42.5   1.52         0
#>  5 <NA>              Angola           -11.2  17.9          0
#>  6 <NA>              Antarctica       -71.9  23.3          0
#>  7 <NA>              Antigua and Bar…  17.1 -61.8          0
#>  8 <NA>              Argentina        -38.4 -63.6          0
#>  9 <NA>              Armenia           40.1  45.0          0
#> 10 Australian Capit… Australia        -35.5 149.           0
#> # … with 275 more rows, and 863 more variables:
#> #   `1/23/20` <dbl>, `1/24/20` <dbl>, `1/25/20` <dbl>,
#> #   `1/26/20` <dbl>, `1/27/20` <dbl>, `1/28/20` <dbl>,
#> #   `1/29/20` <dbl>, `1/30/20` <dbl>, `1/31/20` <dbl>,
#> #   `2/1/20` <dbl>, `2/2/20` <dbl>, `2/3/20` <dbl>,
#> #   `2/4/20` <dbl>, `2/5/20` <dbl>, `2/6/20` <dbl>,
#> #   `2/7/20` <dbl>, `2/8/20` <dbl>, `2/9/20` <dbl>, …
```

#### ¿Pivot?

<img src='https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_03/img/pivot_longer_wider.png' width='100%'/>

Tenemos un conjunto de datos donde cada una de las fechas de fallecimiento por Covid-19 se encuentran almacenadas como columnas.

Sin embargo, esta forma de organizar la información podría generar dificultades al momento de pre-procesar la información o realizar algún tipo de análisis. Tener todas las fechas y casos de muerte por COVID-19 en 2 columnas (fecha y fallecidos), podría ayudar a este proceso.

#### Pivotear

Así, dependiendo de el formato inicial de los datos, tendremos que pivotear hacia la derecha (wider) o hacia abajo (longer).

<img src='https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_03/img/tidyr-pivot_wider_longer.gif' width='100%'/>

### Uso de pivot_longer()

La función `pivot_longer` permitirá pasar todas las fechas que están a lo largo de las columnas a 2: fecha y fallecidos.


```r
covid19_tidy <- covid19 %>%
  select(-c(Lat:Long)) %>%
  pivot_longer(
    cols = -c(`Province/State`:`Country/Region`),
    names_to = "fecha",
    values_to = "fallecidos"
  )
```

### Uso de pivot_wider()

De forma análoga, la función `pivot_wider()` hará exactamente lo contrario, pasar de una data que se encuentre ordenada (**tidy data**), a una data ancha. Para esta función se tendrá que indicar los argumentos: `names_from` y `values_from`.


```r
covid19_tidy %>%
  pivot_wider(
    names_from = "fecha",
    values_from = "fallecidos"
  )
#> # A tibble: 285 × 866
#>    `Province/State`     `Country/Region` `1/22/20` `1/23/20`
#>    <chr>                <chr>                <dbl>     <dbl>
#>  1 <NA>                 Afghanistan              0         0
#>  2 <NA>                 Albania                  0         0
#>  3 <NA>                 Algeria                  0         0
#>  4 <NA>                 Andorra                  0         0
#>  5 <NA>                 Angola                   0         0
#>  6 <NA>                 Antarctica               0         0
#>  7 <NA>                 Antigua and Bar…         0         0
#>  8 <NA>                 Argentina                0         0
#>  9 <NA>                 Armenia                  0         0
#> 10 Australian Capital … Australia                0         0
#> # … with 275 more rows, and 862 more variables:
#> #   `1/24/20` <dbl>, `1/25/20` <dbl>, `1/26/20` <dbl>,
#> #   `1/27/20` <dbl>, `1/28/20` <dbl>, `1/29/20` <dbl>,
#> #   `1/30/20` <dbl>, `1/31/20` <dbl>, `2/1/20` <dbl>,
#> #   `2/2/20` <dbl>, `2/3/20` <dbl>, `2/4/20` <dbl>,
#> #   `2/5/20` <dbl>, `2/6/20` <dbl>, `2/7/20` <dbl>,
#> #   `2/8/20` <dbl>, `2/9/20` <dbl>, `2/10/20` <dbl>, …
```













