---
title: Como selecionar colunas de uma tabela no R?
author: Gustavo Paterno
date: '2018-12-12'
slug: como-selecionar-colunas-de-uma-tabela-no-r
categories:
  - tutorial
tags:
  - r
  - dplyr
image:
  caption: ''
  focal_point: ''
---



# O pacote `dplyr`

> "__dplyr__ é uma gramática para a manipulação de dados, oferecendo uma série de 
verbos consistentes que ajudam você a resolver os principais desafios de 
manipulação de dados e tabelas no R" ([https://dplyr.tidyverse.org](https://dplyr.tidyverse.org))

## `select()`

Neste tutorial iremos aprender a usar o verbo `select()` (selecionar).

A função `select()` seleciona e mantém apenas as variáveis que você deseja em uma
tabela de dados. Variáveis são as colunas do sua tabela no R (data.frame). 

### Exemplo: selecionar algumas variáveis da tabela 

A tabela abaixo possui __11 colunas__! 


```r
mtcars <- as_tibble(mtcars) # Para o print ficar melhor
head(mtcars)
```

```
## # A tibble: 6 x 11
##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
## 1  21       6   160   110  3.9   2.62  16.5     0     1     4     4
## 2  21       6   160   110  3.9   2.88  17.0     0     1     4     4
## 3  22.8     4   108    93  3.85  2.32  18.6     1     1     4     1
## 4  21.4     6   258   110  3.08  3.22  19.4     1     0     3     1
## 5  18.7     8   360   175  3.15  3.44  17.0     0     0     3     2
## 6  18.1     6   225   105  2.76  3.46  20.2     1     0     3     1
```

Suponha que você quer selecionar apenas as colunas: `mpg`, `cyl` e `wt` da
tabela `mtcars`.

__Comando usual__


```r
mtcars[, c("mpg","cyl","wt")]
```

```
## # A tibble: 32 x 3
##      mpg   cyl    wt
##    <dbl> <dbl> <dbl>
##  1  21       6  2.62
##  2  21       6  2.88
##  3  22.8     4  2.32
##  4  21.4     6  3.22
##  5  18.7     8  3.44
##  6  18.1     6  3.46
##  7  14.3     8  3.57
##  8  24.4     4  3.19
##  9  22.8     4  3.15
## 10  19.2     6  3.44
## # ... with 22 more rows
```

__Com `dplyr` e o verbo `select()`__


```r
select(mtcars, mpg, cyl, wt)
```

```
## # A tibble: 32 x 3
##      mpg   cyl    wt
##  * <dbl> <dbl> <dbl>
##  1  21       6  2.62
##  2  21       6  2.88
##  3  22.8     4  2.32
##  4  21.4     6  3.22
##  5  18.7     8  3.44
##  6  18.1     6  3.46
##  7  14.3     8  3.57
##  8  24.4     4  3.19
##  9  22.8     4  3.15
## 10  19.2     6  3.44
## # ... with 22 more rows
```

A principal vantagem do uso da função `select()` é que você não precisa colocar 
o nome das variáveis entre "aspas", o que torna o comando mais fácil e rápido. 

### Excluir colunas

Para excluir colinas de uma tabela e manter todas as outras, utilize o sinal
`-` na frente do nome da coluna.


```r
select(mtcars, -mpg, -cyl, -wt)
```

```
## # A tibble: 32 x 8
##     disp    hp  drat  qsec    vs    am  gear  carb
##  * <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1  160    110  3.9   16.5     0     1     4     4
##  2  160    110  3.9   17.0     0     1     4     4
##  3  108     93  3.85  18.6     1     1     4     1
##  4  258    110  3.08  19.4     1     0     3     1
##  5  360    175  3.15  17.0     0     0     3     2
##  6  225    105  2.76  20.2     1     0     3     1
##  7  360    245  3.21  15.8     0     0     3     4
##  8  147.    62  3.69  20       1     0     4     2
##  9  141.    95  3.92  22.9     1     0     4     2
## 10  168.   123  3.92  18.3     1     0     4     4
## # ... with 22 more rows
```

### Selecionar colunas por nome

As funções `starts_with()`, `ends_with()` e `contains()` podem ser utilizadas em conjunto com
`select()` para selecionar apenas as colunas que começam ou terminam com um determinado padrão.

1. Seleciona colunas que começam com a letra "m".


```r
select(mtcars, starts_with("m")) 
```

```
## # A tibble: 32 x 1
##      mpg
##  * <dbl>
##  1  21  
##  2  21  
##  3  22.8
##  4  21.4
##  5  18.7
##  6  18.1
##  7  14.3
##  8  24.4
##  9  22.8
## 10  19.2
## # ... with 22 more rows
```

2. Seleciona colunas que terminam com a letra "t".


```r
select(mtcars, ends_with("t")) 
```

```
## # A tibble: 32 x 2
##     drat    wt
##  * <dbl> <dbl>
##  1  3.9   2.62
##  2  3.9   2.88
##  3  3.85  2.32
##  4  3.08  3.22
##  5  3.15  3.44
##  6  2.76  3.46
##  7  3.21  3.57
##  8  3.69  3.19
##  9  3.92  3.15
## 10  3.92  3.44
## # ... with 22 more rows
```

3. Seleciona colunas que contém com a letra "a".


```r
select(mtcars, contains("g")) 
```

```
## # A tibble: 32 x 2
##      mpg  gear
##  * <dbl> <dbl>
##  1  21       4
##  2  21       4
##  3  22.8     4
##  4  21.4     3
##  5  18.7     3
##  6  18.1     3
##  7  14.3     3
##  8  24.4     4
##  9  22.8     4
## 10  19.2     4
## # ... with 22 more rows
```

### Mover uma coluna para a primeira posição

Selecione uma coluna e depois adicione todas as outras com `everything()`.


```r
select(mtcars, mpg, everything()) 
```

```
## # A tibble: 32 x 11
##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##  * <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
##  2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
##  3  22.8     4  108     93  3.85  2.32  18.6     1     1     4     1
##  4  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
##  5  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
##  6  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
##  7  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
##  8  24.4     4  147.    62  3.69  3.19  20       1     0     4     2
##  9  22.8     4  141.    95  3.92  3.15  22.9     1     0     4     2
## 10  19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4
## # ... with 22 more rows
```

### Mover uma coluna para a última posição

Primeiro remova a coluna com `-mpg` depois adicione novamente.


```r
select(mtcars, -mpg, mpg) 
```

```
## # A tibble: 32 x 11
##      cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb   mpg
##  * <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1     6  160    110  3.9   2.62  16.5     0     1     4     4  21  
##  2     6  160    110  3.9   2.88  17.0     0     1     4     4  21  
##  3     4  108     93  3.85  2.32  18.6     1     1     4     1  22.8
##  4     6  258    110  3.08  3.22  19.4     1     0     3     1  21.4
##  5     8  360    175  3.15  3.44  17.0     0     0     3     2  18.7
##  6     6  225    105  2.76  3.46  20.2     1     0     3     1  18.1
##  7     8  360    245  3.21  3.57  15.8     0     0     3     4  14.3
##  8     4  147.    62  3.69  3.19  20       1     0     4     2  24.4
##  9     4  141.    95  3.92  3.15  22.9     1     0     4     2  22.8
## 10     6  168.   123  3.92  3.44  18.3     1     0     4     4  19.2
## # ... with 22 more rows
```

## Dicas e sugestões?

Tem alguma crítica? Sugestão? Deixe um comentário ;) 

Até a próxima aventura =)
 
