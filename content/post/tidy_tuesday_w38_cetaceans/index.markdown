---
title: TidyTuesday semana 38 - Cetáceos dos estados Unidos
author: Gustavo Paterno
date: '2018-12-18'
categories:
  - tidytuesday
tags:
  - r
  - dplyr
image:
  caption: ''
  focal_point: ''
---



# O projeto `Tidy Tuesday`

> O projeto [Tidy Tuesday](https://github.com/rfordatascience/tidytuesday) é um
projeto semanal de análise de dados no R. A iniciativa dá ênfase em compreender como 
organizar, processar e visualizar dados utilizando os pacotes [ggplot2](https://ggplot2.tidyverse.org), 
[tidyr](https://tidyr.tidyverse.org), [dplyr](https://dplyr.tidyverse.org) e 
outras ferramentas do universo [tidyverse](https://www.tidyverse.org).

## __A iniciativa__
  __1.__ toda terça-feira será publicado um banco de dados novo 
e diferente sobre os mais variados assuntos. O banco de dados é disponibilizado 
através deste [repósitório]() no Github.    
  __2.__ Cientistas, entusiastas e estudantes do mundo todo utilizam o mesmo banco de 
dados para realizar análises e responder perguntas diferentes.  
  __3.__ Os gráficos e o código das análises são compartilhados com a hashtag 
`#TidyTuesday` nas redes sociais.   
  __4.__ Todo mundo aprende um pouco sobre R, gráficos e sobre o tema da semana. 

Gostaram? Então mãos a obra. 

# Semana 38: `Cetacean Dataset` 

O banco de dados desta semana é sobre [Cetáceos](https://pt.wikipedia.org/wiki/Cetáceos) e
esta disponível no [GIthub](https://github.com/rfordatascience/tidytuesday/tree/master/data/2018-12-18).

## Pacotes necessários


```r
library(tidyverse) # ggplot2, dplyr, etc
library(RCurl)     # para baixar os dados diretamente do Github
```

## Banco de dados

__Descrição:__

Uma coleção de dados sobre baleias e golfinhos que passram algum tempo em cativeiro 
nos USA entre 1938 e 2017.

## Baixando os dados

Utilizamos o pacote `RCurl` para baixar os dados do repositório.


```r
### Load data----
url <- "https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2018/2018-12-18/allCetaceanData.csv"
d <- read_csv(getURL(url))

glimpse(d)
```

```
## Observations: 2,194
## Variables: 22
## $ X1             <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15…
## $ species        <chr> "Bottlenose", "Bottlenose", "Bottlenose", "Bottle…
## $ id             <chr> "NOA0004614, AZA 428, MLF-428", "NOA0004386, AZA …
## $ name           <chr> "Dazzle", "Tursi", "Starbuck", "Sandy", "Sandy", …
## $ sex            <chr> "F", "F", "M", "F", "M", "F", "M", "F", "M", "F",…
## $ accuracy       <chr> "a", "a", "a", "a", "a", "a", "a", "a", "a", "a",…
## $ birthYear      <chr> "1989", "1973", "1978", "1979", "1979", "1980", "…
## $ acquisition    <chr> "Born", "Born", "Born", "Born", "Born", "Born", "…
## $ originDate     <date> 1989-04-07, 1973-11-26, 1978-05-13, 1979-02-03, …
## $ originLocation <chr> "Marineland Florida", "Dolphin Research Center", …
## $ mother         <chr> "Betty III", "Little Bit", "Cindy (T.t. gilli)", …
## $ father         <chr> "Davy II", "Mr. Gipper", "Sambo", NA, NA, "Jethro…
## $ transfers      <chr> NA, NA, "SeaWorld San Diego to SeaWorld Aurora (?…
## $ currently      <chr> "Marineland Florida", "Dolphin Research Center", …
## $ region         <chr> "US", "US", "US", "US", "US", "US", "US", "US", "…
## $ status         <chr> "Alive", "Alive", "Alive", "Alive", "Alive", "Ali…
## $ statusDate     <date> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ COD            <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
## $ notes          <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, "Sunny wa…
## $ transferDate   <date> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
## $ transfer       <chr> "US", "US", "US", "US", "US", "US", "US", "US", "…
## $ entryDate      <date> 1989-04-07, 1973-11-26, 1978-05-13, 1979-02-03, …
```

O banco de dados possui 2194 observações (linhas) e 22 variáveis (colunas).

## Análises e perguntas

Olhando este banco de dados eu me fiz as seguintes perguntas

### Quais são as espécies mais frequentes (top 10)?


```r
nsp <-
  d %>%
  count(species, sort = T) %>%
  top_n(n = 10)
nsp
```

```
## # A tibble: 10 x 2
##    species                      n
##    <chr>                    <int>
##  1 Bottlenose                1668
##  2 Killer Whale; Orca          79
##  3 Beluga                      68
##  4 White-sided, Pacific        56
##  5 Pacific White-Sided         41
##  6 Commerson's                 37
##  7 Spinner                     36
##  8 Beluga Whale                28
##  9 Short-Finned Pilot Whale    25
## 10 Pilot, Short-fin            22
```

```r
### Gráfico
ggplot(nsp, aes(x = reorder(species, n), y = n)) +
  geom_col(fill = "lightblue", color = "white") +
  scale_y_log10() +
  theme_minimal(base_size = 14) +
  labs(x = "Espécie", 
       y = "Número de indivíduos em cativeiro") +
  coord_flip() 
```

<img src="/post/tidy_tuesday_w38_cetaceans/index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

Como podemos ver o grupo [Tursiops (Bottlenose)](https://pt.wikipedia.org/wiki/Tursiops) é o que tem o maior número de indivíduos em cativeiro (mais de 1000 indivíduos). Este grupo é um gênero de golvinhos cosmopolitas, com
pelo menos três espécies:

1. [Tursiops aduncus](https://pt.wikipedia.org/wiki/Tursiops_aduncus)  
2. [Tursiops australis](https://pt.wikipedia.org/wiki/Tursiops_australis)  
3. [Tursiops truncatus](https://pt.wikipedia.org/wiki/Tursiops_truncatus)   

![Tursiops](https://upload.wikimedia.org/wikipedia/commons/1/10/Tursiops_truncatus_01.jpg)

Para incluir também uma espécies de baleia, irei filtrar o banco de dados para 
as especies: `"Bottlenose"` e `"Killer Whale; Orca"`.

![Orca](https://upload.wikimedia.org/wikipedia/commons/3/37/Killerwhales_jumping.jpg)

Faremos todas as análises de dados a partir destas duas espécies.


```r
dd <- d  %>% 
  filter(species %in% c("Bottlenose", "Killer Whale; Orca" ))
```

### Qual a a distribuição do sexo dos indivíduos entre essas duas espécies?


```r
dc <- dd %>%
  group_by(species, sex) %>%
  count()

### Gráfico
ggplot(dc, aes(x = species, y = n, fill = sex)) +
  geom_col(position = "fill", alpha = .75) +
  geom_hline(yintercept = 0.5, lty = "dotted") +
  theme_minimal(base_size = 14) +
  scale_fill_manual(values = c("#66c2a5", 
                               "#fc8d62",
                               gray(.8)),
                    name = "Sexo",
                    labels = c("Macho", "Fêmea", "Sem informação")) +
  labs(y = "Proporção de indivíduos",
       x = "") +
  coord_flip()
```

<img src="/post/tidy_tuesday_w38_cetaceans/index_files/figure-html/unnamed-chunk-5-1.png" width="672" />


## Dicas e sugestões?

Tem alguma crítica? Sugestão? Deixe um comentário ;) 

Até a próxima aventura =)
 
![Alt Text](https://media.giphy.com/media/vFKqnCdLPNOKc/giphy.gif)
