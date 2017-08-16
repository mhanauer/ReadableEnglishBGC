---
title: "Readable English"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Group 1 = Readable English; Group 0 = HELPS 
```{r}
setwd("~/Google Drive/PARCS/Projects/Reading/ReadingBGC")
dataReading = read.csv("ReadableBGC.csv")
head(dataReading)
t.test(dataReading$diff)
t.test(dataReading$diff, dataReading$Group)
library(MASS)
install.packages("exactRankTests")
library(exactRankTests)
wilcox.exact(dataReading$diff)
wilcox.exact(dataReading$diff, dataReading$Group)
```

