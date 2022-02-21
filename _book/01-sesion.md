# Sesión 01

### ¿Qué es Ciencia de Datos?

La Ciencia de Datos es una fusión entre múltiples disciplinas, incluyendo matematicas, estadistica, informatica, y tecnologia de la información. 

La Ciencia de Datos permite extraer información relevante de los datos.

<img src="https://raw.githubusercontent.com/healthinnovation/curso-introduccion-r-tidyverse/main/Sesi%C3%B3n%2001/img/ciencia_datos_1.png" width="60%" style="display: block; margin: auto;" />


### ¿Por qué usar R para Ciencia de Datos?

R cuenta con las herramientas necesarias (entorno, librerías, y funciones) para desarrollar proyectos de Ciencia de Datos.


<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2001/img/ciencia_datos_2.png" width="90%" style="display: block; margin: auto;" />

### Reconocimiento Rstudio

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2001/img/01_IDE_Rdtudio_v1.png" width="85%" style="display: block; margin: auto;" />


<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2001/img/01_IDE_Rdtudio_v2.png" width="85%" style="display: block; margin: auto;" />

### Mover paneles 

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2001/img/03_panel_v1.png" width="85%" style="display: block; margin: auto;" />

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2001/img/03_panel_v2.png" width="85%" style="display: block; margin: auto;" />


### Personalización de Rstudio

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2001/img/04_config_global_v1.png" width="85%" style="display: block; margin: auto;" />

**Modificaciones sobre la interfaz de Rstudio:**

 - Aumentar el zoom o utilizar el atajo: Ctrl y +
 
 - Cambiar tipo de letra puede hacer un tanto más agradable la codificación. La letra Fira
 
 - Code es bastante recomendable, pero se requiere instalar.
 
 - El tema también puede ayudar en que la codificación sea más agradable. El paquete rsthemes, contiene muchos temas extras.

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2001/img/04_config_global_v2.png" width="85%" style="display: block; margin: auto;" />


### ¿Por qué utilizar proyectos?

 - Es más fácil poder compartir los proyectos y estos se encuentran listos para que otras personas puedan colaborar contigo.
 
 - Cada proyecto se encuentra aislado. Los códigos en un proyecto no afectarán a ningún otro. Puedes tener muchos proyectos abiertos y los códigos del proyecto 1 no afectarán al proyecto 2.
 
 - Muy útil para facilitar la importación de data.
 
 - Mejora tanto la reproducibilidad como la colaboración.
 
### Creación de proyectos 

**PASOS:**

1. Seleccionamos “Project (None)” o “File” y luego, new project.

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2001/img/creacion_proyectos_1.png" width="85%" style="display: block; margin: auto;" />

2. “New Directory” se utiliza para indicar dónde voy a almacenar mis archivos y para que R cree una nueva carpeta para mi proyecto, mientras que “Existing Directory” se utiliza si ya tengo una carpeta en la cual voy a almacenar mis archivos. Seleccionamos “New Directory”.

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2001/img/creacion_proyectos_3.png" width="85%" style="display: block; margin: auto;" />

3. Aparecerán más opciones y seleccionamos nuevamente “New Project”

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2001/img/creacion_proyectos_4.png" width="85%" style="display: block; margin: auto;" />


3. En caso de haber seleccionado “Existing Directory” aparecerá esto y buscamos el nombre de la carpeta que utilizaremos.

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2001/img/creacion_proyectos_5.png" width="85%" style="display: block; margin: auto;" />


4. En “Directory name” ponemos el nombre de la carpeta que contendrá el archivo del proyecto, mientras que en “Create project as subdirectory of” seleccionamos dónde está la carpeta en la que trabajaremos.

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2001/img/creacion_proyectos_6.png" width="85%" style="display: block; margin: auto;" />


5. Resumen

<img src="https://healthinnovation.github.io/curso-introduccion-r-tidyverse/Sesi%C3%B3n%2001/img/creacion_proyectos_6.gif" width="85%" style="display: block; margin: auto;" />



### Vectores atómicos 

- Los vectores contienen información homogénea o siempre de un solo tipo de datos.
  
- Un vector puede contener 1 solo elemento o n-elementos.

- Existen hasta 6 tipos de datos que puede contener un vector:
    - Logical: `TRUE`, `FALSE`
    - Integer: `1, 5, 7` 
    - Double: `3.15, 10, 12.86`
    - Character: `"Marcos", "Laptop"`.
    - Complex: `3 + 2i`


**Ejemplos:**


```r
v_numeric <- 5
v_numeric
#> [1] 5
```


```r
v_numeric <- c(5, 10, 15)
v_numeric
#> [1]  5 10 15
```


```r
typeof(v_numeric)
#> [1] "double"
```


```r
v_character <- c("Laptop", "Rstudio", "4.2")
v_character
#> [1] "Laptop"  "Rstudio" "4.2"
```

Los vectores solo pueden tener un solo tipo de información a la vez, así que si dentro de un vector se ingresa un elemento tipo numeric, este inmediatamente será transformado a character.


```r
v_character <- c("Laptop", "Rstudio", 4.2)
v_character
#> [1] "Laptop"  "Rstudio" "4.2"
```


```r
typeof(v_character)
#> [1] "character"
```

Ahora crearemos 2 vectores llamados nombres y edades.



```r
nombres <- c("Luis", "Mateo", "Carlos", "Eduardo")
edades <- c(28, 30, 40, 35)
```

A partir de esto, podemos construir algo con lo que probablemente estemos más familiarizados.


```r
data.frame(nombres, 
           edades)
#>   nombres edades
#> 1    Luis     28
#> 2   Mateo     30
#> 3  Carlos     40
#> 4 Eduardo     35
```
