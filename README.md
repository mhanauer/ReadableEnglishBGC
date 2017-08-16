---
title: "Power Analysis in R for Multilevel Models"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Load and clean the data
```{r}
setwd("~/Google Drive/PARCS/Projects/Reading/ReadingBGC")
dataReading = read.csv("ReadableBGC.csv")
head(dataReading)

library(splitstackshape)

dataReading =cSplit(dataReading, c("Median", "Median.1"), sep="/", stripWhite=TRUE, type.convert=FALSE)
dataReading = as.data.frame(dataReading)
head(dataReading)
dataReading = dataReading[,28:31]
head(dataReading)
colnames(dataReading) = c("WCPMPre","WIPMPre", "WCPMPost", "WIPMPost")
dataReading = na.omit(dataReading)
head(dataReading)
dataReading = as.matrix(dataReading)
dataReading = write.csv(dataReading, "dataReading.csv")
dataReading = read.csv("dataReading.csv", header = TRUE)
dataReading = dataReading[c(-1)]
head(dataReading)
dataReading$WCPMTotalPre = (dataReading[,1] - dataReading[,2])
dataReading$WCPMTotalPost = (dataReading[,3] - dataReading[,4])
dataReading = cbind(dataReading$WCPMTotalPre, dataReading$WCPMTotalPost)
colnames(dataReading) = c("WCPMTotalPre", "WCPMTotalPost")
dataReading = as.data.frame(dataReading)
head(dataReading)
dataReading  =  dataReading$WCPMTotalPost - dataReading$WCPMTotalPre
head(dataReading)
t.test(dataReading)
```
Now we are doing the work for Readable English
```{r}
setwd("~/Google Drive/PARCS/Projects/Reading/ReadingBGC")
dataReading = read.csv("ReadableBGC.csv")
head(dataReading)

library(splitstackshape)

dataReading =cSplit(dataReading, c("Median", "Median.1"), sep="/", stripWhite=TRUE, type.convert=FALSE)
dataReading = as.data.frame(dataReading)
head(dataReading)
Student = dataReading$Student
dataReading = cbind(dataReading$Median_1, dataReading$Median_2, dataReading$Median.1_1, dataReading$Median.1_2)
head(dataReading)
dataReading = dataReading
# After 17 it is HELPS
colnames(dataReading) = c("WCPMPre","WIPMPre", "WCPMPost", "WIPMPost")
dataReading = as.data.frame(dataReading)
dim(dataReading)
dataReading = as.data.frame(dataReading)
id = c(rep(1,17), rep(0,20))
dataReading = cbind(id, dataReading)
dataReading = na.omit(dataReading)
dataRading = as.data.frame(dataReading)
dataReading = write.csv(dataReading, "dataReading.csv")
dataReading  = read.csv("dataReading.csv", header= TRUE)
dataReading = dataReading[c(-1)]
head(dataReading)
dataReading$WCPMTotalPre = (dataReading[,2] - dataReading[,3])
dataReading$WCPMTotalPost = (dataReading[,4] - dataReading[,5])
dataReading = na.omit(dataReading)
head(dataReading)
dataReading = cbind(dataReading$id, dataReading$WCPMTotalPre, dataReading$WCPMTotalPost)
dataReading = as.data.frame(dataReading)
dataReadingdiff = dataReading$V3-dataReading$V2
dataReading = cbind(dataReading$V1, dataReadingdiff)
colnames(dataReading) = c("id", "diff")
dataReading  = as.data.frame(dataReading)
head(dataReading)
t.test(dataReading$id, dataReading$diff)

```

