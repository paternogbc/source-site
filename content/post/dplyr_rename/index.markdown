---
title: Como renomear colunas de uma tabela (data.frame) com o pacote dplyr?
author: Gustavo Paterno
date: '2018-12-13'
slug: como-renomear-colunas-de-uma-tabela-data-frame-com-o-pacote-dplyr
categories:
  - tutorial
tags:
  - dplyr
  - r
---



# O pacote `dplyr`

> "__dplyr__ é uma gramática para a manipulação de dados, oferecendo uma série de 
verbos consistentes que ajudam você a resolver os principais desafios de 
manipulação de dados e tabelas no R" ([https://dplyr.tidyverse.org](https://dplyr.tidyverse.org))

## `rename()`

Neste tutorial iremos aprender a usar o verbo `rename()` (renomear).

A função `renomear()` modifica o nome de uma ou mais colunas de uma 
tabela de dados. Todas as colunas são mantidas. 

## Forma de uso

A forma de usar a função segue essa formula:


```r
dados <- rename(dados, new_name = old_name)
```

Este comando irá modificar o nome da coluna "old_name" para "new_name". 
Vamos ver como funciona na prática.

## Exemplos

A tabela abaixo possui __5 colunas__! 


```r
iris <- as_tibble(iris) # transformando em tibble (não é necessário)
head(iris)
```

```
## # A tibble: 6 x 5
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
##          <dbl>       <dbl>        <dbl>       <dbl> <fct>  
## 1          5.1         3.5          1.4         0.2 setosa 
## 2          4.9         3            1.4         0.2 setosa 
## 3          4.7         3.2          1.3         0.2 setosa 
## 4          4.6         3.1          1.5         0.2 setosa 
## 5          5           3.6          1.4         0.2 setosa 
## 6          5.4         3.9          1.7         0.4 setosa
```


Suponha que queremos modificar o nome da coluna "Species" e trocar por "SP".

### Comando sem `dplyr`


```r
colnames(iris)[5] <- "sp"
iris
```

### Comando com `dplyr`


```r
iris <- rename(iris, SP = Species)
iris
```

```
## # A tibble: 150 x 5
##    Sepal.Length Sepal.Width Petal.Length Petal.Width SP    
##           <dbl>       <dbl>        <dbl>       <dbl> <fct> 
##  1          5.1         3.5          1.4         0.2 setosa
##  2          4.9         3            1.4         0.2 setosa
##  3          4.7         3.2          1.3         0.2 setosa
##  4          4.6         3.1          1.5         0.2 setosa
##  5          5           3.6          1.4         0.2 setosa
##  6          5.4         3.9          1.7         0.4 setosa
##  7          4.6         3.4          1.4         0.3 setosa
##  8          5           3.4          1.5         0.2 setosa
##  9          4.4         2.9          1.4         0.2 setosa
## 10          4.9         3.1          1.5         0.1 setosa
## # ... with 140 more rows
```

Agora suponha que queremos modificar o nome das colunas "Sepal.Length" e "Sepal.Width para "sepL"
e "sepW".


```r
iris <- rename(iris, sepL = Sepal.Length, sepW = Sepal.Width)
iris
```

```
## # A tibble: 150 x 5
##     sepL  sepW Petal.Length Petal.Width SP    
##    <dbl> <dbl>        <dbl>       <dbl> <fct> 
##  1   5.1   3.5          1.4         0.2 setosa
##  2   4.9   3            1.4         0.2 setosa
##  3   4.7   3.2          1.3         0.2 setosa
##  4   4.6   3.1          1.5         0.2 setosa
##  5   5     3.6          1.4         0.2 setosa
##  6   5.4   3.9          1.7         0.4 setosa
##  7   4.6   3.4          1.4         0.3 setosa
##  8   5     3.4          1.5         0.2 setosa
##  9   4.4   2.9          1.4         0.2 setosa
## 10   4.9   3.1          1.5         0.1 setosa
## # ... with 140 more rows
```

Agora suponha que queremos modificar o nome das colunas "Peal.Length" e "Peal.Width para "petL"
e "petW".


```r
iris <- rename(iris, petL = Petal.Length, petW = Petal.Width)
iris
```

```
## # A tibble: 150 x 5
##     sepL  sepW  petL  petW SP    
##    <dbl> <dbl> <dbl> <dbl> <fct> 
##  1   5.1   3.5   1.4   0.2 setosa
##  2   4.9   3     1.4   0.2 setosa
##  3   4.7   3.2   1.3   0.2 setosa
##  4   4.6   3.1   1.5   0.2 setosa
##  5   5     3.6   1.4   0.2 setosa
##  6   5.4   3.9   1.7   0.4 setosa
##  7   4.6   3.4   1.4   0.3 setosa
##  8   5     3.4   1.5   0.2 setosa
##  9   4.4   2.9   1.4   0.2 setosa
## 10   4.9   3.1   1.5   0.1 setosa
## # ... with 140 more rows
```

> Note que não precisamos colocar o nome das colunas entre aspas, o que facilita 
muito o processo. Além disso, podemos renomear múltiplas colunas ao mesmo tempo
sepando por vígula. 

## Dicas e sugestões?

Tem alguma crítica? Sugestão? Deixe um comentário ;) 

Até a próxima aventura =)

![Alt Text](https://media.giphy.com/media/vFKqnCdLPNOKc/giphy.gif)
