# ggseacr

<p align="right">
 <img src="https://raw.githubusercontent.com/kxuanly/ggseacr/daa65b3b967b8a81ccd37f80aaecd8349a165dd7/inst/Gradient_White_Logo.png" height="528" width="408">
</p>

The geom you always wished for adding nudibranchs to ggplot2.
The original source code of this package is based on geom_image from ggimage.
Nudibranch images done by Berkana McDowell


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
 <img src="https://raw.githubusercontent.com/kxuanly/ggseacr/main/exampleimg/ggseacr-ggplot-grid.png">
</p>

```r
ggplot(mtcars) +
  geom_nudibranch(aes(mpg, wt), nudibranch = "O.rosacea", size = 5)
```

<p align="center">
 <img src="https://raw.githubusercontent.com/kxuanly/ggseacr/main/exampleimg/ggseacr-ggplot-mtcars.png">
</p>

```r
ggplot(mtcars) +
  geom_nudibranch(aes(mpg, wt, size = cyl), nudibranch = "S.shawl")
```
<p align="center">
 <img src="https://raw.githubusercontent.com/kxuanly/ggseacr/main/exampleimg/ggseacr-ggplot-mtcars2.png">
</p>

Most of the code below came from: [Jonathan Hersh](https://twitter.com/DogmaticPrior) and RCoder.

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

dat$nudibranch <- rep(NA, 132)

dat$nudibranch[which(dat$income == "median")] <- "O.rosacea"
dat$nudibranch[which(dat$income == "99percent")] <- "H.crassicornis"

ggplot(dat, aes(x = Year, y = value, group = income, color = income)) +
  geom_line(size = 2) +
  ggtitle("ggseacr") +
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
 <img src="https://raw.githubusercontent.com/kxuanly/ggseacr/main/exampleimg/ggseacr-animated-example.gif">
</p>


