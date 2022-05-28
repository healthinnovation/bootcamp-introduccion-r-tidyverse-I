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

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_02/img/function_example.png" width="85%" style="display: block; margin: auto;" />

### Buscando ayuda sobre las funciones

La mejor forma de averiguar esta información es utilizar ? seguido del nombre de la función. Al hacer esto, se abrirá el manual de ayuda en el panel inferior derecho de RStudio que proporcionará una descripción de la función, uso, argumentos, detalles y ejemplos:

  - `?sd`
  - `help(sd)`
  - <img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_02/img/help_function.png" width=140px">

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_02/img/help_page.png" width="85%" style="display: block; margin: auto;" />

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

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_02/img/paquetes_hexa.png" width="85%" style="display: block; margin: auto;" />


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


### Bases de datos a utilizar 

Usaremos una base de datos proporcionado por [Gan et al. (2018)](https://www.nature.com/articles/s41598-018-27482-2) en su estudio:

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_02/img/levofloxacin_trial.png" width="100%">

Dicho estudio es un ensayo clínico aleatorizado (ECA) de 400 participantes en el que se compara 2 tipos de tratamientos para erradicar la infección por Helicobácter Pylori.

- **Grupo A de tratamiento**: Esomeprazol, amoxicilina, bismuto coloidal con pectina y levofloxacina 500mg una vez al día.

- **Grupo B de tratamiento**: Levofloxacina 200mg dos veces al día, durante un periodo de 14 días.

<table align="center">
 <tr align="center">
  <th><b>Randomized group</b></th>
  <th><b>n</b></th>
 </tr>
 <tr align="center">
  <th>group A</th>
  <th>200</th>
 </tr>
 <tr align="center">
  <th>group B</th>
  <th>200</th>
 </tr>

</table>

### Importación de datos I


|     Función        | Archivos 
---------------------|------------------
`readxl::read_excel()` | <img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_02/img/excel_logo.png" width="50px">
`readr::read_csv()`    | <img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_02/img/csv_logo.png" width="50px">
`haven::read_dta()`    | <img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_02/img/stata_logo.png" width="50px">
`haven::read_sav()`    | <img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_02/img/spss_logo.png" width="50px">


Vamos a importar el archivo excel que tiene una extensión `.xlsx` y se encuentra dentro de la carpeta data.

**Recuerda:** _Al importar el archivo debemos asignarlo a un objeto, para poder guardar la información. En este caso llamaremos a este objeto como `trial_data`._


```
#> ── Attaching packages ───────────
#> ✔ ggplot2 3.3.6     ✔ dplyr   1.0.9
#> ✔ tidyr   1.2.0     ✔ stringr 1.4.0
#> ✔ readr   2.1.2     ✔ forcats 0.5.1
#> ✔ purrr   0.3.4
#> ── Conflicts ────────────────────
#> ✖ dplyr::filter() masks stats::filter()
#> ✖ dplyr::lag()    masks stats::lag()
```


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

### Importación de datos II

En algunos casos estaremos frente a base de datos que contengan cierta información en sus primeras filas que no sean relevantes como datos a considerar para el análisis. La mayor cantidad de veces tienen un propósito meramente informativo. Ejemplo:

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/sesion_02/img/researchdata2_preview.png" width='100%'/>


#### Situación 

En estas situaciones tenemos 2 alternativas:

 **a)** Editar el archivo en cuestión y eliminar las filas que no sean relevantes. 
 
 **b)** Durante la importación indicar que se omitan las primeras filas o filtrarlas una vez se haya importado.

Siempre será una mejor opción manejar los cambios desde el código, ya que se esa manera mantenemos los archivos originales y además podemos tener un registro de los cambios realizados.

Para hacer esto usaremos el argumento skip dentro de la función `readxl::read_excel()`, que indicará la cantidad de filas que deseamos omitir en la importación.


#### Problema 

Si intentamos importar la data sin especificar ningún argumento, veremos como se registran informaciones que no requerimos, y solo se encuentran en los datos a manera de información.


```r
trial_data2 <- readxl::read_excel("_data/researchdata2.xlsx")
#> New names:
#> • `` -> `...1`
#> • `` -> `...3`
#> • `` -> `...4`
#> • `` -> `...5`
#> • `` -> `...6`
#> • `` -> `...7`
#> • `` -> `...8`
#> • `` -> `...9`
#> • `` -> `...10`
trial_data2
#> # A tibble: 403 × 10
#>    ...1       `Data de ejemp…` ...3  ...4  ...5  ...6  ...7 
#>    <chr>      <chr>            <chr> <chr> <chr> <chr> <chr>
#>  1 <NA>       <NA>             <NA>  <NA>  <NA>  <NA>  <NA> 
#>  2 <NA>       <NA>             <NA>  <NA>  <NA>  <NA>  <NA> 
#>  3 Patient n… Baseline 13C-UBT Rand… Foll… adve… adve… Adve…
#>  4 1          Positive         grou… Nega… No    NA    NA   
#>  5 2          Positive         grou… Nega… Yes   Fati… Mild 
#>  6 3          Positive         grou… Nega… No    NA    NA   
#>  7 4          Positive         grou… Posi… Yes   Abdo… Mild 
#>  8 5          Positive         grou… Nega… Yes   Drow… Mild 
#>  9 6          Positive         grou… Nega… No    NA    NA   
#> 10 7          Positive         grou… Nega… No    NA    NA   
#> # … with 393 more rows, and 3 more variables: ...8 <chr>,
#> #   ...9 <chr>, ...10 <chr>
```

#### Solución 

Ya que en este caso la base de datos llamada researchdata2.xlsx empieza a mostrar datos relevantes a partir de la fila 4, requeriremos omitir o saltar (skip) 3 filas, se la siguiente manera:


```r
trial_data2 <- readxl::read_excel(
  "_data/researchdata2.xlsx",
  skip = 3
  )

trial_data2
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
