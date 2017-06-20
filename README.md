---
title: "QuadTrendR"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Here is an example showing the when you include the original term and plot the original term with the quadtric version it either makes a u or n shape depending upon its relationship with the dependent variable.
```{r}
rm(list=ls())
A <- structure(list(Time = c(0, 1, 2, 4, 6, 8, 9, 10, 11, 12, 13, 
14, 15, 16, 18, 19, 20, 21, 22, 24, 25, 26, 27, 28, 29, 30), 
Counts = c(4,6,8,10,12,14,16,18,20,24,26,28,30,28,26,24,22,20,18,16,14,12,10,8,6,4)), .Names = c("Time", "Counts"),
row.names = c(1L, 2L, 3L, 5L, 7L, 9L, 10L, 11L, 12L, 13L, 14L, 15L, 16L, 17L, 19L, 20L, 21L, 22L, 23L, 25L, 26L, 27L, 28L, 29L, 30L, 31L),
class = "data.frame")
length(A$Time)
length(A$Counts)
attach(A)
names(A)
lm1 = lm(Counts ~ Time)
summary(lm1)

# Plotting doesn't work in R Markdown
plot(Time, Counts, ylab = "Counts ", col = "red" )
abline(lm1)


Time2 = Time^2
lm2 = lm(Counts~ Time +  Time2)
timevalues <- seq(0, 30, 0.1)
predictedcounts <- predict(lm2,list(Time = timevalues, Time2=timevalues^2))
plot(Time, Counts, pch=16, xlab = "Time (s)", ylab = "Counts", cex.lab = 1.3, col = "blue")
lines(timevalues, predictedcounts, col = "darkgreen", lwd = 3)
```
Here we seeing if the quadratic model is a better fit.
```{r}
anova(lm1, lm2)
AIC(lm1, lm2)
BIC(lm1, lm2)
```

