# R2cancerEpidemiology
A series of R scripts to QC, explore, analyze, and visualize Epidemium Open Datasets

Repository content:

* core2R.r:  Script to import QC the Epidemium Core data set.
* 


Import mortality data (Epidemium Core dataset) into R

```
datadir   <- "/home/common/data/" 
filename  <-"mortalite_1950_2013.csv"
setwd(datadir)
mortality <- read.csv(filename, header = TRUE, sep=";") 
dim(mortality) 
[1] 3191598       6 
head(mortality)    
id.cancer  sex age registry year cases.number
1        C11 Male 0-4  Albania 2009            0
2     C00-14 Male 0-4  Albania 2009            0
3 C00-15,C32 Male 0-4  Albania 2009            0
4        C15 Male 0-4  Albania 2009            0
5        C16 Male 0-4  Albania 2009            0
6     C17-21 Male 0-4  Albania 2009            0 

# To extract data for France only, you need to do a subset on the registry column.
dataFrance <- subset(mortality, mortality[,4] =="France") 
dim(dataFrance)
[1] 59850     6
```

Import cancer incidences data

```
setwd("..BD4Cancer/data")
dat <- read.csv("incidence_1953_2007.csv", header=T, sep=",")
header(dat)

# use the function grep to extract data for France.
datFrance <- dat[grep("^France", dat$registry), ]

# Export data as .TXT file or RData Object (more efficient for further analyses)
write.table(datFrance,"incidenceCanFrance.txt", sep = "\t")
save(dat, file = "incidencesAllCoreDataset.RData")
save(datFrance, file = "incidenceCancFrance.RData")
```
