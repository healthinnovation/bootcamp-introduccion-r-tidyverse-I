# Sesión 04

## Exploración competencial 

### Uso de filter()

#### ¿Para que sirve?

- Ayuda a crear un subconjunto de datos con todas las filas que cumplan tus condiciones.
Pueden incluirse varias condiciones dentro de un filtro.

- Funciones y operadores útiles:
  
  - De comparación: `==`, `<`, `>`, `<=`, `>=`, `!=`, `%in%`, `is.na`, `!is.na`
  
  - De lógica: `&`, `|`, `xor`, `!`, `any()`, `all()`
  

```r
library(tidyverse)
#> ── Attaching packages ─────────────────── tidyverse 1.3.1 ──
#> ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
#> ✓ tibble  3.1.6     ✓ dplyr   1.0.8
#> ✓ tidyr   1.2.0     ✓ stringr 1.4.0
#> ✓ readr   2.1.2     ✓ forcats 0.5.1
#> ── Conflicts ────────────────────── tidyverse_conflicts() ──
#> x dplyr::filter() masks stats::filter()
#> x dplyr::lag()    masks stats::lag()
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

#### Ejemplo

Esta data muestra información de la [NOAA](https://www.nhc.noaa.gov/data/#hurdat) acerca de tormentas desde 1975 hasta el 2020.


```r
storms %>% 
  count(status, category)
#> # A tibble: 8 × 3
#>   status              category     n
#>   <chr>               <ord>    <int>
#> 1 hurricane           1         1933
#> 2 hurricane           2          749
#> 3 hurricane           3          434
#> 4 hurricane           4          411
#> 5 hurricane           5           86
#> 6 tropical depression -1        2898
#> 7 tropical storm      0         5347
#> 8 tropical storm      1            1
```

Si quisieramos solo trabajar con los huracanes de categoría 5, tendríamos que hacer lo siguiente con la función `filter()`:


```r
storms %>% 
  filter(status == "hurricane",
         category == 5)
#> # A tibble: 86 × 13
#>    name   year month   day  hour   lat  long status category
#>    <chr> <dbl> <dbl> <int> <dbl> <dbl> <dbl> <chr>  <ord>   
#>  1 Anita  1977     9     2     0  24.6 -96.2 hurri… 5       
#>  2 Anita  1977     9     2     6  24.2 -97.1 hurri… 5       
#>  3 David  1979     8    30     6  16   -64.2 hurri… 5       
#>  4 David  1979     8    30    12  16.3 -65.2 hurri… 5       
#>  5 David  1979     8    30    18  16.6 -66.2 hurri… 5       
#>  6 David  1979     8    31     0  16.8 -67.3 hurri… 5       
#>  7 David  1979     8    31     6  17   -68.3 hurri… 5       
#>  8 David  1979     8    31    12  17.2 -69.1 hurri… 5       
#>  9 David  1979     8    31    18  17.9 -69.7 hurri… 5       
#> 10 Gilb…  1988     9    13    18  19.4 -82.5 hurri… 5       
#> # … with 76 more rows, and 4 more variables: wind <int>,
#> #   pressure <int>, tropicalstorm_force_diameter <int>,
#> #   hurricane_force_diameter <int>
```

## Uso de select()

- Esta función permite seleccionar las variables de interés.

- Puede ser útil previo a un análisis de datos o solo si se desea tener una data menos larga.

- Para usarlo se puede nombrar a las variables dentro de la función `select()` y/o usar el comando : para indcar hasta

<img src='https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_04/img/select_01.png' width='100%'/>

<img src='https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_04/img/select_02.png' width='100%'/>

El uso de las funciones con **pipe** (`%>%`) permite anidarlas una tras otra. Además, si las columnas están una a lado de otra, podemos usar : para seleccionar varios al mismo tiempo.



```r
storms %>% 
  filter(status == "hurricane",
         category == 5) %>% 
  select(name, year, month, day, hour, wind)
#> # A tibble: 86 × 6
#>    name     year month   day  hour  wind
#>    <chr>   <dbl> <dbl> <int> <dbl> <int>
#>  1 Anita    1977     9     2     0   140
#>  2 Anita    1977     9     2     6   150
#>  3 David    1979     8    30     6   140
#>  4 David    1979     8    30    12   145
#>  5 David    1979     8    30    18   150
#>  6 David    1979     8    31     0   145
#>  7 David    1979     8    31     6   145
#>  8 David    1979     8    31    12   145
#>  9 David    1979     8    31    18   150
#> 10 Gilbert  1988     9    13    18   140
#> # … with 76 more rows
```


```r
storms %>% 
  filter(status == "hurricane",
         category == 5) %>% 
  select(name:hour, wind)
#> # A tibble: 86 × 6
#>    name     year month   day  hour  wind
#>    <chr>   <dbl> <dbl> <int> <dbl> <int>
#>  1 Anita    1977     9     2     0   140
#>  2 Anita    1977     9     2     6   150
#>  3 David    1979     8    30     6   140
#>  4 David    1979     8    30    12   145
#>  5 David    1979     8    30    18   150
#>  6 David    1979     8    31     0   145
#>  7 David    1979     8    31     6   145
#>  8 David    1979     8    31    12   145
#>  9 David    1979     8    31    18   150
#> 10 Gilbert  1988     9    13    18   140
#> # … with 76 more rows
```

## Mutate II

<img src='https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_04/img/mutate_ilustration.png' width='100%'/>

Esta función del paquete `dplyr` nos permite agregar o modificar las variables actuales en un conjunto de datos (dataframe). Tal y como ya lo vimos en la [sesión 03](https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_03/#6), esta función puede hacer cambios sobre una o múltiples variables existentes, así como crear varias a la vez serparándolas con una coma ([Y. Wendy Huynh,2019](https://bookdown.org/yih_huynh/Guide-to-R-Book/mutate.html)).


```r
data %>% 
  mutate(
    var1 = old_var*2,
    var2 = old_var*3,
    var3 = var1*var2
  )
```

## Mutate II: Uso de across()

Haremos la prueba con la base storm. Usando la función `across()` para aplicar una función a múltiples variables a la vez. En esta ocasión transformaremos en factores a las variables status y category de tormentas.


```r
storms %>% 
  select(name:pressure) %>% 
  mutate(
    status = as.factor(status),
    category = as.factor(category)
  ) %>% 
  glimpse()
#> Rows: 11,859
#> Columns: 11
#> $ name     <chr> "Amy", "Amy", "Amy", "Amy", "Amy", "Amy",…
#> $ year     <dbl> 1975, 1975, 1975, 1975, 1975, 1975, 1975,…
#> $ month    <dbl> 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6,…
#> $ day      <int> 27, 27, 27, 27, 28, 28, 28, 28, 29, 29, 2…
#> $ hour     <dbl> 0, 6, 12, 18, 0, 6, 12, 18, 0, 6, 12, 18,…
#> $ lat      <dbl> 27.5, 28.5, 29.5, 30.5, 31.5, 32.4, 33.3,…
#> $ long     <dbl> -79.0, -79.0, -79.0, -79.0, -78.8, -78.7,…
#> $ status   <fct> tropical depression, tropical depression,…
#> $ category <ord> -1, -1, -1, -1, -1, -1, -1, -1, 0, 0, 0, …
#> $ wind     <int> 25, 25, 25, 25, 25, 25, 25, 30, 35, 40, 4…
#> $ pressure <int> 1013, 1013, 1013, 1013, 1012, 1012, 1011,…
```


```r
storms %>% 
  select(name:pressure) %>% 
  mutate(
    across(c(status, category), as.factor)
  ) %>% 
  glimpse()
#> Rows: 11,859
#> Columns: 11
#> $ name     <chr> "Amy", "Amy", "Amy", "Amy", "Amy", "Amy",…
#> $ year     <dbl> 1975, 1975, 1975, 1975, 1975, 1975, 1975,…
#> $ month    <dbl> 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6,…
#> $ day      <int> 27, 27, 27, 27, 28, 28, 28, 28, 29, 29, 2…
#> $ hour     <dbl> 0, 6, 12, 18, 0, 6, 12, 18, 0, 6, 12, 18,…
#> $ lat      <dbl> 27.5, 28.5, 29.5, 30.5, 31.5, 32.4, 33.3,…
#> $ long     <dbl> -79.0, -79.0, -79.0, -79.0, -78.8, -78.7,…
#> $ status   <fct> tropical depression, tropical depression,…
#> $ category <ord> -1, -1, -1, -1, -1, -1, -1, -1, 0, 0, 0, …
#> $ wind     <int> 25, 25, 25, 25, 25, 25, 25, 30, 35, 40, 4…
#> $ pressure <int> 1013, 1013, 1013, 1013, 1012, 1012, 1011,…
```


## Mutate II: lubridate

Muchas veces durante el pre-procesamiento de datos tenemos que enfrentarnos a manejo de fechas (crear, transformar, etc.). Para estos fines podemos usar **las funciones del paquete** `lubridate`.

Para tener una mejor apreciación de la variable de fecha que crearemos, usaremos `relocate()` para reposicionar a la variable creada.


```r
storms %>%
  select(name:pressure) %>%
  mutate(
    date = lubridate::make_date(year, month, day)
  ) %>%
  relocate(date, .before = year)
#> # A tibble: 11,859 × 12
#>    name  date        year month   day  hour   lat  long
#>    <chr> <date>     <dbl> <dbl> <int> <dbl> <dbl> <dbl>
#>  1 Amy   1975-06-27  1975     6    27     0  27.5 -79  
#>  2 Amy   1975-06-27  1975     6    27     6  28.5 -79  
#>  3 Amy   1975-06-27  1975     6    27    12  29.5 -79  
#>  4 Amy   1975-06-27  1975     6    27    18  30.5 -79  
#>  5 Amy   1975-06-28  1975     6    28     0  31.5 -78.8
#>  6 Amy   1975-06-28  1975     6    28     6  32.4 -78.7
#>  7 Amy   1975-06-28  1975     6    28    12  33.3 -78  
#>  8 Amy   1975-06-28  1975     6    28    18  34   -77  
#>  9 Amy   1975-06-29  1975     6    29     0  34.4 -75.8
#> 10 Amy   1975-06-29  1975     6    29     6  34   -74.8
#> # … with 11,849 more rows, and 4 more variables:
#> #   status <chr>, category <ord>, wind <int>,
#> #   pressure <int>
```

## Uso de group_by()

Esta función permite poder indicarle a R que las operaciones que hagamos en adelante, sean divididas y aplicadas por las agrupaciones que sea haya formado. Es decir, que se puede hacer la agrupación por una o múltiples variables.


```r
storms %>% 
  filter(year >= 2010) %>% 
  group_by(name)
#> # A tibble: 3,608 × 13
#> # Groups:   name [112]
#>    name   year month   day  hour   lat  long status category
#>    <chr> <dbl> <dbl> <int> <dbl> <dbl> <dbl> <chr>  <ord>   
#>  1 Alex   2010     6    25    18  16.4 -83.1 tropi… -1      
#>  2 Alex   2010     6    26     0  16.6 -83.9 tropi… -1      
#>  3 Alex   2010     6    26     6  16.7 -84.9 tropi… 0       
#>  4 Alex   2010     6    26    12  16.9 -86.1 tropi… 0       
#>  5 Alex   2010     6    26    18  17.2 -87.2 tropi… 0       
#>  6 Alex   2010     6    27     0  17.5 -88.2 tropi… 0       
#>  7 Alex   2010     6    27     6  18   -89.1 tropi… 0       
#>  8 Alex   2010     6    27    12  18.5 -90   tropi… 0       
#>  9 Alex   2010     6    27    18  18.9 -90.7 tropi… 0       
#> 10 Alex   2010     6    28     0  19.2 -91.1 tropi… 0       
#> # … with 3,598 more rows, and 4 more variables: wind <int>,
#> #   pressure <int>, tropicalstorm_force_diameter <int>,
#> #   hurricane_force_diameter <int>
```

La función `group_by()` solo configura como será el tratamiento de la data en adelante. No observará ningún cambio percepctible en los datos con excepción de:

```
# Groups:   name [112]
```

## Uso de summarise()

Esta función permite obtener algun resumen de los datos, como la media, desviación estándar, valores máximos, mínimos, calculos de prueba estadística, y la mayoría de funciones de esta naturaleza. El uso conjunto de `group_by()` y `summarise()` es una combinación perfecta.

<img src ="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_04/img/group_by_01.png" width='100%'/>



```r
mtcars %>%
  group_by(cyl) %>%
  summarise(
    avg = mean(mpg)
  )
#> # A tibble: 3 × 2
#>     cyl   avg
#>   <dbl> <dbl>
#> 1     4  26.7
#> 2     6  19.7
#> 3     8  15.1
```


## Uso de summarise()

Usaremos la misma [BD de COVID-19 que empleamos en la sesión 03](https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_03/#19).

Este dataset está alojada en el siguiente repositorio de GitHub ([click aquí](https://github.com/CSSEGISandData/COVID-19)).

<img src='https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_04/img/github_covid_1.png' width='100%'/>

Mediante la función `read_csv` podremos importar la data directamente desde **Github**.


```r
covid19 <- read_csv("https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_deaths_global.csv")
#> Rows: 284 Columns: 822
#> ── Column specification ────────────────────────────────────
#> Delimiter: ","
#> chr   (2): Province/State, Country/Region
#> dbl (820): Lat, Long, 1/22/20, 1/23/20, 1/24/20, 1/25/20...
#> 
#> ℹ Use `spec()` to retrieve the full column specification for this data.
#> ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
covid19
#> # A tibble: 284 × 822
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
#> # … with 274 more rows, and 817 more variables:
#> #   `1/23/20` <dbl>, `1/24/20` <dbl>, `1/25/20` <dbl>,
#> #   `1/26/20` <dbl>, `1/27/20` <dbl>, `1/28/20` <dbl>,
#> #   `1/29/20` <dbl>, `1/30/20` <dbl>, `1/31/20` <dbl>,
#> #   `2/1/20` <dbl>, `2/2/20` <dbl>, `2/3/20` <dbl>,
#> #   `2/4/20` <dbl>, `2/5/20` <dbl>, `2/6/20` <dbl>,
#> #   `2/7/20` <dbl>, `2/8/20` <dbl>, `2/9/20` <dbl>, …
```

## Uso de summarise()

Recordar que primero debemos pivotear la data para poder trabajar con ella. Obtendremos resúmenes de casos por muerte COVID-19 por países.


```r
covid19 %>%
  select(-c(Lat:Long)) %>%
  pivot_longer(
    cols = -c(`Province/State`:`Country/Region`),
    names_to = "fecha",
    values_to = "fallecidos"
  ) %>%
  group_by(`Country/Region`) %>%
  summarise(
    M = mean(fallecidos, na.rm = TRUE),
    DE = sd(fallecidos, na.rm = TRUE),
    Max = max(fallecidos, na.rm = TRUE),
    Min = min(fallecidos, na.rm = TRUE)
  ) %>%
  arrange(desc(M))
#> # A tibble: 198 × 5
#>    `Country/Region`       M      DE    Max   Min
#>    <chr>              <dbl>   <dbl>  <dbl> <dbl>
#>  1 US               452333. 305740. 988899     0
#>  2 Brazil           325330. 243458. 662271     0
#>  3 India            236318. 193372. 521966     0
#>  4 Mexico           164019. 113885. 323944     0
#>  5 Peru             122894.  76116. 212654     0
#>  6 Russia           119528. 117685. 366209     0
#>  7 Italy             86270.  51331. 161766     0
#>  8 Colombia          66945.  52586. 139751     0
#>  9 Iran              66048.  48315. 140854     0
#> 10 Argentina         59771.  48107. 128344     0
#> # … with 188 more rows
```


```r
covid19_tidy <- covid19 %>%
  select(-c(Lat:Long)) %>%
  pivot_longer(
    cols = -c(`Province/State`:`Country/Region`),
    names_to = "fecha",
    values_to = "fallecidos"
  )
```

Guardaremos la data pivoteada en un objeto llamado **covid19_tidy**, para no extender demasiado el código. Además, veamos lo sencillo que es poder introducir un filter a los resultados obtenidos.


```r
covid19_tidy %>%
  group_by(`Country/Region`) %>%
  summarise(
    M = mean(fallecidos, na.rm = TRUE),
    DE = sd(fallecidos, na.rm = TRUE),
    Max = max(fallecidos, na.rm = TRUE),
    Min = min(fallecidos, na.rm = TRUE)
  ) %>%
  arrange(desc(M))
#> # A tibble: 198 × 5
#>    `Country/Region`       M      DE    Max   Min
#>    <chr>              <dbl>   <dbl>  <dbl> <dbl>
#>  1 US               452333. 305740. 988899     0
#>  2 Brazil           325330. 243458. 662271     0
#>  3 India            236318. 193372. 521966     0
#>  4 Mexico           164019. 113885. 323944     0
#>  5 Peru             122894.  76116. 212654     0
#>  6 Russia           119528. 117685. 366209     0
#>  7 Italy             86270.  51331. 161766     0
#>  8 Colombia          66945.  52586. 139751     0
#>  9 Iran              66048.  48315. 140854     0
#> 10 Argentina         59771.  48107. 128344     0
#> # … with 188 more rows
```


```r
covid19_tidy %>%
  mutate(
    fecha = lubridate::mdy(fecha)
  ) %>%
  filter(fecha > "2022-01-01") %>%
  group_by(`Country/Region`) %>%
  summarise(
    M = mean(fallecidos, na.rm = TRUE),
    DE = sd(fallecidos, na.rm = TRUE),
    Max = max(fallecidos, na.rm = TRUE),
    Min = min(fallecidos, na.rm = TRUE)
  ) %>% 
  arrange(desc(M))
#> # A tibble: 198 × 5
#>    `Country/Region`       M     DE    Max    Min
#>    <chr>              <dbl>  <dbl>  <dbl>  <dbl>
#>  1 US               926962. 52488. 988899 825097
#>  2 Brazil           643144. 15699. 662271 619401
#>  3 India            507215. 13648. 521966 481893
#>  4 Russia           339858. 19291. 366209 304284
#>  5 Mexico           314087.  8773. 323944 299544
#>  6 Peru             208730.  3545. 212654 202782
#>  7 Italy            151898.  7470. 161766 137646
#>  8 Indonesia        148924.  4669. 155903 144097
#>  9 Colombia         136612.  3492. 139751 130026
#> 10 Iran             136084.  3491. 140854 131680
#> # … with 188 more rows
```

