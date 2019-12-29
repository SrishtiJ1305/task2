# Introduction
This is my work from the Google Code-in task Exploring E-commerce data. Below you can see the code with comments.

# Prerequisites
- R
- RStudio
- Dplyr

# Code Description
The code below can be copied to R and executed as is.
```
# task2 
library(dplyr)

e_commerce = read.csv("https://raw.githubusercontent.com/FahroziFahrozi/Google-Code-In-Task/master/Task%20Dataset.csv",
             header = TRUE)

View(e_commerce)
#how many observation and variables are in the data set?
nrow(e_commerce)
#1593
ncol(e_commerce)
#45

#which city had the most visitors and how many? Among Australia cities
subset_australia=subset(e_commerce,e_commerce$country=="Australia")
subset_australia %>% 
  group_by(city) %>% 
  summarise(behavNumVisits= sum(behavNumVisits)) %>% arrange(desc(behavNumVisits))
#"Brisbane"                    10
            
#Draw a horizontal box plot for the number of site visits.
boxplot(e_commerce$behavNumVisits, horizontal=TRUE)

#Solve the previous problem for the city with the most visitors, using the which.max function
citywithmostvisitor = e_commerce %>% 
  group_by(city) %>% 
  summarise(behavNumVisits= sum(behavNumVisits))

maxcitywithvisit = which.max (citywithmostvisitor$behavNumVisits)
citywithmostvisitor [maxcitywithvisit,]
#Lakewood            104

#What is the mean-median difference for number of site visits?
meansite_visit = mean(e_commerce$behavNumVisits)
mediansite_visit = median(e_commerce$behavNumVisits)
meansite_visit-mediansite_visit
#0.7715003

#What is the mean-median difference for site visits, after excluding the person who had the most visits?
max_index = which.max(e_commerce$behavNumVisits)
e_commerce_exclude=e_commerce[-c(max_index),]
meansite_visit = mean(e_commerce_exclude$behavNumVisits)
mediansite_visit = median(e_commerce_exclude$behavNumVisits)
meansite_visit-mediansite_visit
#0.7091709
```

# Screen Record
![Screen Recording](http://g.recordit.co/RahvUnnAYD.gif)

# Authors
- Srishti Jain

