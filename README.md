#Importing the Dataset
getwd()
setwd('C:\\Users\\Harshali\\Documents\\Datasets')
A<-read.csv("basket.csv")

#Installing the neccesary libraries
install.packages("arules")
library(arules)
install.packages("arulesViz")
library(arulesViz)

#Converting the dataset into Transaction Object
B<-read.transactions("basket.csv",format = "basket", sep = ",")
itemFrequencyPlot(B, topN=20, type = "absolute")

#Applying the Association Rule
rules<-apriori(data=B, parameter=list(supp=0.001, conf=0.08),
appearance = list(default = "lhs", rhs = "rolls/buns"), control=list(verbose=F))
rules<-sort(rules, decreasing = TRUE, by = "confidence")
inspect(rules[1:10])
plot(rules, method="graph", interactive=TRUE)
