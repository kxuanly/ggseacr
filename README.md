# ggnudibranchs
The geom you always wished for adding nudibranchs to ggplot2.
The original source code of this package is based on geom_image from ggimage.


<p align="center">
 <img src="https://user-images.githubusercontent.com/67192157/105871532-b0a48700-5ff9-11eb-9371-ecd915ded374.png">
</p>



+ Follow original creator on [Twitter](https://twitter.com/RCoderWeb)
+ Follow original creator on [Facebook](https://www.facebook.com/RCODERweb)
+ Visit original creators [R programming site](https://r-coder.com/)

## Installation
```r
# install.packages("remotes")
remotes::install_github("kxuanly/ggseacr@main")
library(ggseacr)
```


## Available nudibranchs

There are 5 nudibranches available:

```r
"O.rosacea" (default), "H.crassicornis", "S.shawl", "Sea.lemon", and "T.catalinae".
```

## Some examples

```r
grid <- expand.grid(1:5, 3:1)

df <- data.frame(x = grid[, 1],
                 y = grid[, 2],
                 image = c("O.rosacea", "H.crassicornis", "S.shawl", "Sea.lemon", "T.catalinae"))
                           
library(ggplot2)
ggplot(df) +
 geom_nudibranch(aes(x, y, nudibranch = image), size = 5) +
    xlim(c(0.25, 5.5)) + 
    ylim(c(0.25, 3.5))
```

<p align="center">
 <img src="https://user-images.githubusercontent.com/67192157/106767679-6b0c3d80-663b-11eb-96f5-a21f2794bd84.png">
</p>


```r
ggplot(mtcars) +
  geom_nudibranch(aes(mpg, wt), nudibranch = "O.rosacea", size = 5)
```

<p align="center">
 <img src="https://user-images.githubusercontent.com/67192157/105848781-c86f1180-5fdf-11eb-8468-813a41235292.png">
</p>


```r
ggplot(mtcars) +
  geom_nudibranch(aes(mpg, wt, size = cyl), nudibranch = "S.shawl")
```

<p align="center">
 <img src="https://user-images.githubusercontent.com/67192157/105849119-416e6900-5fe0-11eb-904e-6dc30be87546.png">
</p>


I took the most part of the following code from [Jonathan Hersh](https://twitter.com/DogmaticPrior).

```r
library(Ecdat)
data(incomeInequality)

library(tidyverse)
library(ggseacr)
library(gganimate)


 dat <-
   incomeInequality %>%
   select(Year, P99, median) %>%
   rename(income_median = median,
          income_99percent = P99) %>%
   pivot_longer(cols = starts_with("income"),
                names_to = "income",
                names_prefix = "income_")

dat$cat <- rep(NA, 132)

dat$cat[which(dat$income == "median")] <- "O.rosacea"
dat$cat[which(dat$income == "99percent")] <- rep(c("pop_close", "pop"), 33)

ggplot(dat, aes(x = Year, y = value, group = income, color = income)) +
   geom_line(size = 2) +
   ggtitle("ggseacr) +
   geom_nudibranch(aes(nudibranch = nudibranch), size = 5) +
   xlab("Nudibranch") +
   ylab("Nudibranch") +
   theme(legend.position = "none",
         plot.title = element_text(size = 20),
         axis.text = element_blank(),
         axis.ticks = element_blank()) +
   transition_reveal(Year)
```

<p align="center">
 <img src="https://user-images.githubusercontent.com/67192157/105854010-9ad99680-5fe6-11eb-9ee0-c42e9e257d48.gif">
</p>


