# Sesión 02

### ¿Qué es una función?

Las funciones son módulos de código autónomo que realizan una tarea específica y generalmente, toman algún tipo de estructura de datos (vector, dataframes, etc.), lo procesan y devuelven un resultado.

El uso general de una función es el nombre de la función seguida de paréntesis

```
function_name(input)
```
Los inputs se denominan argumentos e incluyen:
 
 - El objeto físico (cualquier estructura de datos) en el que la función lleva a cabo una tarea.
 
 - Especificaciones que alteran la forma en que opera la función

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2002/img/function_example.png" width="85%" style="display: block; margin: auto;" />

### Buscando ayuda sobre las funciones

La mejor forma de averiguar esta información es utilizar ? seguido del nombre de la función. Al hacer esto, se abrirá el manual de ayuda en el panel inferior derecho de RStudio que proporcionará una descripción de la función, uso, argumentos, detalles y ejemplos:

  - `?sd`
  - `help(sd)`
  - <img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2002/img/help_function.png" width=140px">

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2002/img/help_page.png" width="85%" style="display: block; margin: auto;" />

Alternativamente, si está familiarizado con la función pero solo necesita recordar los nombres de los argumentos, puede usar:



```r
args(sd)
```

```
## function (x, na.rm = FALSE) 
## NULL
```

### Ejemplo de una función

Se tiene el número 3.15181930, pero solo necesitamos dos decimales. Para ello, utilizaremos la función round() que redondea los números de acuerdo a la cantidad de decimales que asignemos. En este caso, solo necesitaremos 2.



```r
round(3.15181930, digits = 2)
#> [1] 3.15
```

Como se puede observar, se ha utilizado el argumento digits para regular la cantidad de decimales.

**Nota: Si proporcionamos los argumentos en el mismo orden en el que han sido definidos, no es necesario nombrarlos**


```r
round(3.15181930, 2)
#> [1] 3.15
```

### ¿Data.frame?

- Estructura de datos 2D

- Admite datos con diferente tipo de variable (lo opuesto a matrices)

- Similar a Microsoft Excel

**Se crean con la función:**

```
data.frame(
  Var1 = elementos1,
  Var2 = elementos2
)
```


```r
var1 <- c("Peru", "Argentina", "Bolivia")
var2 <- rep("aceptado",3)
var3 <- seq(1000,1200,100)
df <- data.frame(var1, var2, var3)
df
#>        var1     var2 var3
#> 1      Peru aceptado 1000
#> 2 Argentina aceptado 1100
#> 3   Bolivia aceptado 1200
```



```r
df <- data.frame(
  var1 = c("Peru", "Argentina", "Bolivia"),
  var2 = rep("aceptado",3),
  var3 = seq(1000,1200,100)
)
df
#>        var1     var2 var3
#> 1      Peru aceptado 1000
#> 2 Argentina aceptado 1100
#> 3   Bolivia aceptado 1200
```

### ¿Tibble?

 - Son la versión mejorada del data.frame
 - Disponible en el paquete tibble y por lo tanto en el tidyverse.

**Se crean con la función:**

```
# Instalación
install.packages("tibble")
# Llavado o activación de paquete
library(tibble)
tibble(
  Var1 = elementos1,
  Var2 = elementos2
)
```

```r
library(tibble)
tibble(
  var1 = c("Peru", "Argentina", "Bolivia"),
  var2 = rep("aceptado",3),
  var3 = seq(1000,1200,100)
)
#> # A tibble: 3 × 3
#>   var1      var2      var3
#>   <chr>     <chr>    <dbl>
#> 1 Peru      aceptado  1000
#> 2 Argentina aceptado  1100
#> 3 Bolivia   aceptado  1200
```


### data.frame() v.s. tibble()

Ambas funciones tienen sus versiones `as.*` o `as_*` que permite transformar algo en lo que se desea. En este caso se estaría usando as.data.frame para convertir algo a data.frame y as_tibble para ese mismo objetivo.


```r
class(iris)
#> [1] "data.frame"
```


```r
# data.frame
head(iris) # Muestra las 6 primeras filas del data.frame
#>   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
#> 1          5.1         3.5          1.4         0.2  setosa
#> 2          4.9         3.0          1.4         0.2  setosa
#> 3          4.7         3.2          1.3         0.2  setosa
#> 4          4.6         3.1          1.5         0.2  setosa
#> 5          5.0         3.6          1.4         0.2  setosa
#> 6          5.4         3.9          1.7         0.4  setosa
```


```r
# tibble
as_tibble(iris)
#> # A tibble: 150 × 5
#>    Sepal.Length Sepal.Width Petal.Length Petal.Width Species
#>           <dbl>       <dbl>        <dbl>       <dbl> <fct>  
#>  1          5.1         3.5          1.4         0.2 setosa 
#>  2          4.9         3            1.4         0.2 setosa 
#>  3          4.7         3.2          1.3         0.2 setosa 
#>  4          4.6         3.1          1.5         0.2 setosa 
#>  5          5           3.6          1.4         0.2 setosa 
#>  6          5.4         3.9          1.7         0.4 setosa 
#>  7          4.6         3.4          1.4         0.3 setosa 
#>  8          5           3.4          1.5         0.2 setosa 
#>  9          4.4         2.9          1.4         0.2 setosa 
#> 10          4.9         3.1          1.5         0.1 setosa 
#> # … with 140 more rows
```

### ¿Qué es un paquete?

Los paquetes son colecciones de funciones, datos y código compilado de R en un formato bien definido, creados para agregar una funcionalidad específica.

Hay un conjunto de paquetes estándar (o base) que se consideran parte del código fuente de R y están disponibles automáticamente como parte de su instalación de R.

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2002/img/paquetes_hexa.png" width="85%" style="display: block; margin: auto;" />


### Instalación de paquetes desde CRAN

La forma de instalar un paquete dependerá de dónde se encuentre. Entonces, para los paquetes disponibles públicamente, esto significa a qué repositorio pertenece. La forma más común es usar el repositorio CRAN, luego solo necesita el nombre del paquete y usa el siguiente comando:


```r
install.packages("paquete")
```

Después de ejecutar esto, recibirá algunos mensajes en la pantalla. Dependerán del sistema operativo que esté utilizando, las dependencias y si el paquete se instaló correctamente.

### Instalación de paquetes vía remotes

Cada repositorio tiene su propia forma de instalar un paquete a partir de ellos, por lo que en el caso de que utilice regularmente paquetes de diferentes fuentes, este comportamiento puede ser un poco frustrante. Una forma más eficiente es probablemente usar el paquete `remotes` para simplificar este proceso.


```r
install.packages("remotes")
```

Después de haber instalado `remotes` podemos utilizar algunas de sus funciones para la instalación de paquetes:
  
  - `remotes::install_bioc()` desde Bioconductor
  
  - `remotes::install_github()` desde GitHub
  
  - `remotes::install_version()` para instalar una versión específica de CRAN. 


### Importación de datos

|     Función        | Archivos 
---------------------|------------------
`readxl::read_excel()` | <img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2002/img/excel_logo.png" width="50px">
`readr::read_csv()`    | <img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2002/img/csv_logo.png" width="50px">
`haven::read_dta()`    | <img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2002/img/stata_logo.png" width="50px">
`haven::read_sav()`    | <img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2002/img/spss_logo.png" width="50px">