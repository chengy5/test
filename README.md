# data cleaning-week 3-quiz
##Q3
library(dplyr)
GDPData <- read.csv("https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FGDP.csv",
                    skip = 4, col.names = c("CountryCode","Rank",3,"Country","Dollar",6,7,8,9,10),nrow = 190)
GDpData2 <- select(GDPData,CountryCode,Rank,Country,Dollar)
EDUData <- read.csv("https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FEDSTATS_Country.csv") 
mergeData <- merge(GDpData2, EDUData, by.x = "CountryCode", by.y = "CountryCode") %>% arrange(desc(Rank))
head(mergeData,13)

##Q4
AverageRank <- group_by(mergeData,Income.Group) %>% summarize(Rank = mean(Rank, na.rm=TRUE))

##Q5
library(Hmisc)
mergeData$quantile <- cut2(mergeData$Rank, g=5)
table(mergeData$quantile,mergeData$Income.Group)
