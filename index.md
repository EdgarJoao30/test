---
title: Principios de Estad?stica Aplicada con R
subtitle: Introducci?n a R
Project: 
author:
- name: Gabriel Carrasco Escobar
  affiliation: Universidad Peruana Cayetano Heredia
- name: Jorge Ruiz Cabrejos
  affiliation: Universidad Peruana Cayetano Heredia
Comment:
web: 
date: 08 de febrero del 2018
output: 
  html_document:
    toc: true
    toc_float: true
---

<p style="text-align: center;"> 
Rutinas y comandos complementarios del curso *Principios de Estad?stica Aplicada con R (PEAR)*

*Cualquier problema con este c?digo, porfavor contactar a gabriel.carrasco@upch.pe*
</p>

Los paquetes a ser utilizados en esta secci?n son:

```{r message = FALSE, warning = FALSE}
library(devtools)
library(rafalib)
library(downloader)
library(dplyr)
```


```{r include = FALSE}
wd <- "C:/Users/Jorge/Desktop/Universidad/Curso R - FASPA"
csv <- "Databases/femaleMiceWeights.csv"
dat <- read.csv(file.path(wd, csv))
```

## Introducci?n a R

La consola de RStudio es el ?rea de trabajo en donde se ejecutan operaciones, funciones y c?digos con R, desarrollado por R Development Core Team (2008).

Por ejemplo, podemos utilizarlo para llevar a cabo [operaciones aritm?ticas](#table_arith) como:

```{r}
10*10
```

```{r}
420/30
```
O crear vectores (secuencia ordenada de elementos de un mismo tipo):
```{r}
1:10
```

```{r}
c("Juan","Carlos","Gabriel")
```

### Objetos

Un objeto es una estructura que almacena las caracter?sticas y datos que se le asigne. Es asi que se dice que R es un lenguaje de programaci?n orientado a objetos. 

A continuaci?n, generamos un vector con n?meros enteros del 1 al 10

```{r}
1:10
```

Ahora, asignamos este vector a un objeto al cual llamaremos `x`

```{r}
x<-1:10
x
```
As?, el objeto `x` almacenar? este vector

### Funciones
Las funciones son operaciones o procedimientos desarrollados por la comunidad de R. Por ejemplo, la funci?n `rnorm` nos permite generar una muestra de n?meros racionales aleatorios con distribuci?n normal. 

Utilizando esta funci?n, asignaremos 10 n?meros generados aleatoriamente al objeto `y`

```{r}
y=rnorm(10)
y
```

Ahora, utilizando ambos objetos antes creados (`x` e `y`), utilizamos la funci?n `plot` para graficar los datos.

```{r}
plot(x,y)
```

A?adiendo `col = "color"` podemos modificar el color del gr?fico, especificando el color dentro del doble corchete. En el ejemplo a continuaci?n, colocamos el color `blueviolet`

*[Lista de colores disponibles en R](http://www.stat.columbia.edu/~tzheng/files/Rcolor.pdf)* por @tzheng_color

```{r}
plot(x,y, col= "blueviolet")
```

## Importando datos

```{r message = FALSE, warning = FALSE, include= FALSE}
rm(x,y)
```

```{r include = FALSE}
require(knitr)
require(kableExtra)
```


### Datasets <a id="femalemice"></a> 

R puede utilizar bases de datos externas (Excel, Stata, SPSS, etc.) Para importar esta informaci?n a la consola, primero debemos establecer nuestro directorio de trabajo. Aqui almacenaremos nuestras bases de datos, scripts y archivos a ser utilizados.

```{r eval = FALSE}
setwd("C:/Usuario/Estudiante/Escritorio/Estadistica")
```

A continuaci?n, cargaremos la base de datos `femaleMiceWeights.csv` de Love (2015) y lo almacenaremos dentro del objeto `dat`. Para lograrlo, se puede importar de tres formas distintas: 

1.- En la barra superior, entrando a File > Import Dataset y seleccionando el tipo de archivo a instalar
```{r echo = FALSE, out.width = "50%"}
include_graphics("https://puu.sh/z3OBb/a73789c1bc.png")
```

2.- Utilizando `read.csv`

```{r eval = FALSE}
dat <- read.csv("C:/Usuario/Estudiante/Escritorio/Estadistica/Databases/femaleMiceWeights.csv")
```

3.- Utilizando `file.choose()`
```{r eval = FALSE}
dat <- read.csv(file.choose())
```

### Download
Esta base de datos (`femaleMiceWeights.csv`) es de acceso libre y puede ser descargada directamente desde su repositorio con la funci?n `download`.
El archivo se descargara en el directorio de trabajo

```{r}
url <- "https://raw.githubusercontent.com/genomicsclass/dagdata/master/inst/extdata/femaleMiceWeights.csv"
filename <- "femaleMiceWeights2.csv"
download(url, destfile=filename)
```

Para conocer el directorio de trabajo actual (en donde la funci?n `download` a realizado la descarga) se puede utilizar la funci?n `getwd()`

### Visualizaci?n de una base

Para visualizar parte de la tabla importada en R, utilizamos la funci?n `head`
```{r}
head(dat)
```

Para visualizar todos los datos de la tabla importada en R, utilizamos la funci?n `view`
```{r, eval = FALSE}
View(dat)
```

```{r, echo = FALSE}
kable(dat, "html") %>%
  kable_styling(full_width = F)
```

## Tipo de datos en R

Existen cuatro tipos de objetos b?sicos en R

### Vector
Serie de elementos del mismo tipo (dimensi?n 1)

```{r}
vector <- seq(1, 100, by =3)
vector
```

### Lista
Contiene una selecci?n de objetos heterog?neos

```{r}
lista <- list(name="Mike", gender="M", company ="ProgramCreek")
lista
```

### Matriz
Extensi?n de vectores de 2 dimensiones

```{r}
mat <- rbind(c(1,2,3),c(4,5,6))
mat
```

### Data Frame
Una matriz con nombres de columnas (variables) y que puede incluir variables no num?ricas

```{r}
df <- data.frame(a=c(1,2,3,4,5), b=c(1,2,3,4,5))
df
```

### Identificaci?n de objetos 

La funci?n `class` nos permite identificar el tipo de dato de un objeto. En este caso, `dat` es un data.frame
```{r}
class(dat)
```

