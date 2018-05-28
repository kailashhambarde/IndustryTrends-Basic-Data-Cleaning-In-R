# Future_500_Basic-with-Basic-Data-Cleaning-in-R
Future_500 Basic with Basic Data Cleaning in R
getwd()



setwd("E:\\Locker\\Sai\\SaiHCourseNait\\DecBtch\\R_Datasets")



fin <- read.csv("Future-500.csv")



fin #ntc in the environment for the obj fin

#it has lot of objs



head(fin)



tail(fin,10)



str(fin)



summary(fin)

#note Industry Factor, ID, Year, Inception, State, Revnue, Expenses



#so how do v change something from a nonfac to a fac

#Changing from non-factor to factor: factor(fin$ID)
#ntc it has 500 levels



summary(fin$ID) summary(factor(fin$ID))



str(fin$ID)



fin$ID <- factor(fin$ID)



# v will now override ID var summary(fin$ID)
#ntc ID is recognized as fac



str(fin$ID)



#ntc ID



#repeat this for Inception also summary(fin$Inception)


fin$Inception <- factor(fin$Inception)



summary(fin$Inception)

#ntc now for Inc it is giving for 93 comps started in 2011

# and not seeing min max etc

#which makes sense for this kind of var



str(fin)



#FVT

a <- c("12","13","14","12","12")

a

#ntc these r chars

#how do v convert them to numerics b <- as.numeric(a)
b



b1 <- factor(b) b1


levels(b1)



z <- factor(c("12","13","14","12","12"))

z



levels(z)#Levels:12 13 14 thse r now categories

#next how do v convert these to numeric

#our first inclination is



y <- as.numeric(z) y


#ntc now v get

# 1 2 3 1 1 --> these r now treated as categories 1,2,3 z
#12 13 14 12 12



z <- factor(c("12","13","14","12","12"))

z



#--- Correct way

x <- as.numeric(as.character(z)) x


x1 <- factor(x) x1


z <- c("12","13","14","12","12")

z



#--- Correct way

x <- as.numeric(as.character(z)) x


#FVT Ex

head(fin$Profit)

#note Profit a simple scenario

str(fin$Profit)

#ntc Rev & Expns r facs nd v need to convert em into numeric



summary(fin$Profit)



fin$Profit <- factor(fin$Profit)



summary(fin$Profit)



fin$Profit <- as.numeric(fin$Profit)



head(fin$Profit)

#ntc Profit is a num



summary(fin)












































# *** comment all the factors now and run upto ***



fin <- read.csv("Future-500.csv")

head(fin)



tail(fin,10)



str(fin)



summary(fin)



summary(fin$Inception)



fin$Inception <- factor(fin$Inception)



summary(fin$Inception)



str(fin)



head(fin)

#note Profit a simple scenario



str(fin$Expenses)

#***

#Rev & Exp r num data treated as factors

?gsub

?sub

#when v use gsub it alrd converts a fac into chr head(fin$Expenses)


mbh <- "Mera Bharath Mahaan Mera Bharath Mahaan" mbh


sub("Mera","Hamara",mbh)



gsub("Mera","Hamara",mbh)



head(fin$Expenses)



fin$Expenses <- gsub(" Dollars","",fin$Expenses)



head(fin$Expenses)



fin$Expenses <- gsub(",","",fin$Expenses)



head(fin$Expenses)



str(fin$Expenses)

#note now Expenses is no longer a fac but a chr



head(fin$Revenue)

fin$Revenue <- gsub("$","",fin$Revenue)



head(fin$Revenue)

#ntc $ is still there as it is a special chr

#v need to use esc

fin$Revenue <- gsub("\\$","",fin$Revenue)



head(fin$Revenue)



fin$Revenue <- gsub(",","",fin$Revenue)



head(fin$Revenue)



str(fin$Revenue)

#now it is chr



#repeat the same for Growth head(fin$Growth)


fin$Growth <- gsub("%","",fin$Growth)



head(fin$Growth)



str(fin$Growth)

#so 3 of the vars r now chrs

#which means v can convert em into numerics



#it is more convenient to conv chr into numeric

#rather than a fac into numeric fin$Expenses <- as.numeric(fin$Expenses)


fin$Revenue <- as.numeric(fin$Revenue)



fin$Growth <- as.numeric(fin$Growth)



#ntc now Exp, R, & G r numeric str(fin)


summary(fin)



#what is an NA




?NA #this is the 3rd logical comp



TRUE #1 this is the first log comp in R



FALSE #0 this is the 2nd log comp in R



NA



TRUE == FALSE



TRUE == 5



TRUE == 1



FALSE == FALSE



FALSE == 0



FALSE == 4



NA == TRUE



NA == FALSE



NA == 15



15 == NA



NA == NA



NA == ""

NA == NULL

#NA

#it is sim to Null in sql





#***

#Locating missing data head(fin,24)
#note NAs, row 22 has <NA>, also theer r empty vals



?complete.cases



complete.cases(fin)

# returns a vec of true or false,

#checking to see if there r nas or not in rows



#how to look at subset of DF

!complete.cases(fin)



fin[!complete.cases(fin),]



#note v got 6 rows



#*** head(fin,24) nrow(fin)


#fin <- read.csv("Future-500.csv")

fin <- read.csv("Future-500.csv",na.strings=c(""))



head(fin,24)



# v cld also treat NY as NA

#fin <- read.csv("Future-500.csv",na.strings=c("","NY","Xyz"))



#note now row 14 & 15 <NA>



fin$Expenses <- gsub(" Dollars","",fin$Expenses) fin$Expenses <- gsub(",","",fin$Expenses) fin$Revenue <- gsub("\\$","",fin$Revenue) fin$Revenue <- gsub(",","",fin$Revenue) fin$Growth <- gsub("%","",fin$Growth) fin$Expenses <- as.numeric(fin$Expenses) fin$Revenue <- as.numeric(fin$Revenue) fin$Growth <- as.numeric(fin$Growth)




fin[!complete.cases(fin),]

#now ntc it picks up more rows for NAs

#wht is the diff btw <NA> & NA



str(fin)

# it is factors vs numerics



#Filtering: using which() for non-missing data head(fin)


fin[!complete.cases(fin),]

#lets say v want every single row with rev 9746272 fin$Revenue == 9746272


fin[fin$Revenue == 9746272,]

#so why r there so many NAs in the 2 rows below



NA == 9746272



9746272 == NA



?which



fin[fin$Revenue == 9746272,]



which(fin$Revenue == 9746272)



fin[which(fin$Revenue == 9746272),]

#now v r passing this

#***





#this is the second approach

#fin[c(3,4,5),]



#lets take another ex head(fin)
#ntc 3rd row empls cols is NA



#if v want all the comps which hv 45 empls

#ntc 2 NAs

#1 is NA

# 2nd is NA.1



filter = fin$Employees==45 fin[filter,]


fin[which(filter),]

#ntc NAs r gone



#***

#Filtering: using is.na() for missing data

#how do v pick up those rows whic hv NAs head(fin)

fin$Expenses == NA #this is how the filter looks



fin[fin$Expenses == NA,] #this is not what v want and this is not helpful



#which(fin$Expenses == NA) #this is how the filter looks



?is.na



a <- c(1,24,543,NA,76)

a



is.na(a)



is.na(fin$Expenses)



#which(!is.na(fin$Expenses))



fin[is.na(fin$Expenses),]

#ntc v get exact 3 rows and all of em hv expenses as NA

#repeat this process for state col or other cols



























# first always make backup of your data fin_backup <- fin


nrow(fin)



fin[!complete.cases(fin),] #this will gv us all the rows

#which hv NAs in some or other cols



fin[is.na(fin$Industry),] #this gvs which rows r NAs for industry col



head(fin,20)



nrow(fin[!is.na(fin$Industry),])

nrow(fin[!complete.cases(fin),])



nrow(fin[!complete.cases(fin$Industry),])



nrow(fin)



fin <- fin[!is.na(fin$Industry),]



nrow(fin)



head(fin,20)



fin[!complete.cases(fin),]

#verify rows 14 & 15 hv been dealt with and not there



#Resetting the DF index



rownames(fin)



nrow(fin)



1:nrow(fin)



head(fin,20)

rownames(fin) <- 1:nrow(fin)



head(fin,20)



View(fin)

#now ntc the row indx is 498 diff from ID  col



# another alt way is View(fin_backup)


fin <- fin_backup



nrow(fin)



fin[!complete.cases(fin),]



fin[is.na(fin$Industry),] # gvs which rows r empty



fin <- fin[!is.na(fin$Industry),]



head(fin,15)



rownames(fin) <- NULL



head(fin,15)



View(fin)

#***

# v r telling R to set the rownames

#this is not nece but good to know




#Factual Analysis: Replacing missing Data fin[!complete.cases(fin),]




fin[is.na(fin$State),]

#ntc state and city

fin[is.na(fin$State) & fin$City=="New York",]



fin[is.na(fin$State) & fin$City=="New York","State"] <- "NY"



fin[is.na(fin$State),]



fin[is.na(fin$State) & fin$City=="New York",]

#check manually fin[c(11,377),]


fin[!complete.cases(fin),]

fin[is.na(fin$State) & fin$City=="San Francisco",]



#ntc this is getting smaller everytime



fin[is.na(fin$State) & fin$City=="San Francisco","State"] <- "CA"



fin[c(82,265),]



fin[!complete.cases(fin),]

#ntc this is getting smaller everytime



#***

#Median imputation method



fin[!complete.cases(fin),]



median(fin[,"Employees"])

#NA

median(fin[,"Employees"], na.rm=TRUE)



mean(fin[,"Employees"], na.rm=TRUE)



fin[!complete.cases(fin),]



median(fin[fin$Industry=="Retail","Employees"],  na.rm=TRUE)



mean(fin[fin$Industry=="Retail","Employees"],  na.rm=TRUE)

#209

med_emp_retail <- median(fin[fin$Industry=="Retail","Employees"], na.rm=TRUE)



fin[is.na(fin$Employees) & fin$Industry=="Retail","Employees"] <- med_emp_retail



#check fin[3,]


#repeat this same process for Financial services



mean(fin[,"Employees"], na.rm=TRUE)



mean(fin[fin$Industry=="Financial  Services","Employees"],na.rm=TRUE)



median(fin[,"Employees"], na.rm=TRUE)



median(fin[fin$Industry=="Financial  Services","Employees"],na.rm=TRUE)



med_empl_finserv <- median(fin[fin$Industry=="Financial Services","Employees"],na.rm=TRUE)



fin[is.na(fin$Employees) & fin$Industry=="Financial Services",]



fin[is.na(fin$Employees) & fin$Industry=="Financial Services","Employees"] <- med_empl_finserv

#Check fin[330,]


head(fin)



str(fin)
































#***



fin[!complete.cases(fin),]

#Growth col

med_growth_constr <- median(fin[fin$Industry=="Construction","Growth"],na.rm=TRUE)



fin[is.na(fin$Growth) & fin$Industry=="Construction","Growth"] <- med_growth_constr

#check fin[8,]

fin[!complete.cases(fin),]



#Mini exrcise

#Revenue

med_rev_constr <- median(fin[fin$Industry=="Construction","Revenue"],na.rm=TRUE) med_rev_constr
#9055058



fin[is.na(fin$Revenue) & fin$Industry=="Construction",]



fin[is.na(fin$Revenue) & fin$Industry=="Construction","Revenue"]<-med_rev_constr



fin[is.na(fin$Revenue) & fin$Industry=="Construction",]

#



fin[!complete.cases(fin),]



#Expenses

#ntc v get 4 rows



med_exp_constr <- median(fin[fin$Industry=="Construction","Expenses"],na.rm=TRUE) med_exp_constr


fin[is.na(fin$Expenses) & fin$Industry=="Construction",]

fin[is.na(fin$Expenses) & fin$Industry=="Construction","Expenses"] <- med_exp_constr



fin[!complete.cases(fin),]




#*** Deriving vals

#Revenue = Expenses + Profit



fin[is.na(fin$Profit),]



vecRev <- fin[is.na(fin$Profit),"Revenue"] vecRev


vecExpns <- fin[is.na(fin$Profit),"Expenses"]



vecPrfts <- vecRev - vecExpns



fin[is.na(fin$Profit),"Profit"] <- vecPrfts



fin[c(8,42),]



fin[!complete.cases(fin),]



fin[is.na(fin$Expense),]

fin[is.na(fin$Expense),"Expenses"] <- fin[is.na(fin$Expense),"Revenue"] - fin[is.na(fin$Expense),"Profit"]



fin[15,]




fin[!complete.cases(fin),]

#ntc there is only 1 row



#***

#Visualize results

#scatterplot classified by industry showing rev, expense, profit

#scplt that includes industry trends for the expenses-revenue relationship

#Boxplots showing growth by industry



#install.packages("ggplot2") library(ggplot2)


head(fin)

#scatterplot classified by industry showing rev, expense, profit p <- ggplot(data=fin)
p



p + geom_point(aes(x=Revenue, y=Expenses))



p + geom_point(aes(x=Revenue, y=Expenses,

                                 colour=Industry, size=10))



p + geom_point(aes(x=Revenue, y=Expenses,

colour=Industry, size=Profit))



#scplt that includes industry trends for the expenses-revenue relationship



#p + geom_point(aes(x=Revenue, y=Expenses,

#colour=Industry))



#p   + geom_smooth(aes(x=Revenue, y=Expenses,

                                 #colour=Industry))



d <- ggplot(data=fin, aes(x=Revenue, y=Expenses,

colour=Industry))



#d + geom_point() + geom_smooth()



d + geom_point() + geom_smooth(fill=NA,size=1.2)

#ntc construction trend



#*** library(ggplot2)
#Boxplots showing growth by industry

f <- ggplot(data=fin,aes(x=Industry, y=Growth,

colour=Industry))

f

#f + geom_boxplot()



f + geom_boxplot(size=1)

#ntc the medians

#for IT services it is the highest

#for Govt it is lowest

#for constr is 10



f + geom_jitter() + geom_boxplot(size=1, alpha=0.5, outlier.color=NA)




f <- ggplot(data=fin,aes(x=Industry, y=Profit, colour=Industry))
f + geom_boxplot(size=1)

