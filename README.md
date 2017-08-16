---
title: "Power Analysis in R for Multilevel Models"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Load and clean the data  Group 1 = Readable English; Group 0 = HELPS 
Now with the clean data
```{r}
setwd("~/Google Drive/PARCS/Projects/Reading/ReadingBGC")
dataReading = read.csv("ReadableBGC.csv")
head(dataReading)
t.test(dataReading$diff)
t.test(dataReading$diff, dataReading$Group)
library(MASS)
wilcox.test(dataReading$diff)
```

