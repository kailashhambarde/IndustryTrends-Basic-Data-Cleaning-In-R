# IndustryTrends-Basic-Data-Cleaning-In-R
#read data frm
fin <- read.csv("Future-500.csv")

#read topsix record
head(fin)

#last 10 record
tail(fin,10)

#meta data about data.
str(fin)

#'data.frame':	500 obs. of  11 variables:
#$ ID       : int  1 2 3 4 5 6 7 8 9 10 ...
#$ Name     : Factor w/ 500 levels "Abstractedchocolat",..: 297 451 168 40 485 199 435 339 242 395 ...
#$ Industry : Factor w/ 8 levels "","Construction",..: 8 6 7 6 8 6 3 2 6 3 ...
#$ Inception: int  2006 2009 2012 2011 2013 2013 2009 2013 2009 2010 ...
#$ Employees: int  25 36 NA 66 45 60 116 73 55 25 ...
#$ State    : Factor w/ 43 levels "","AL","AZ","CA",..: 37 34 36 4 42 28 23 30 4 9 ...
#$ City     : Factor w/ 297 levels "Addison","Alexandria",..: 94 181 105 195 151 154 53 295 232 26 ...
#$ Revenue  : Factor w/ 499 levels "","$1,614,585 ",..: 480 195 486 247 403 142 309 1 97 118 ...
#$ Expenses : Factor w/ 498 levels "","1,026,548 Dollars",..: 7 486 4 249 228 248 58 1 403 496 ...
#$ Profit   : int  8553827 13212508 8701897 10727561 4193069 8179177 3259485 NA 5274553 11412916 ...
#$ Growth   : Factor w/ 33 levels "","-2%","-3%",..: 15 17 12 15 15 19 13 1 27 17 ...

#In above Output we observe that in the columns Revenue and Expenses Variable type shown as "Factor".
#bt they must have numeric value their variable must have INT.

#Basic Stat.

summary(fin)

#note Industry Factor, ID, Year, Inception, State, Revnue, Expenses
#so how do v change something from a nonfac to a fac

#Changing from non-factor to factor: factor(fin$ID)
#notice it has 500 levels.

summary(fin$ID) 
summary(factor(fin$ID))
str(fin$ID)

fin$ID <- factor(fin$ID)

# we will now override ID var summary(fin$ID)
#ntc ID is recognized as fac.

str(fin)
str(fin$ID)


#repeat this for Inception also summary(fin$Inception)
fin$Inception <- factor(fin$Inception)
str(fin$Inception)

summary(fin$Inception)
#1999 2000 2001 2002 2003 2004 2005 2006 2007 2008 2009 2010 2011 2012 2013 2014 NA's 
# 4    9    6    9    6    7    8   13    7    6   60   83   93   80   69   39    1 
#ntc now for Inc it is giving for 93 comps started in 2011
# and not seeing min max etc


#which makes sense for this kind of var

str(fin)

#FVT

a <- c("12","13","14","12","12")
a
#notice these are character
#now we are convert them into numeric

b <-as.numeric(a)
b
#[1] 12 13 14 12 12

b1 <- as.factor(b)
b1
#[1] 12 13 14 12 12
#Levels: 12 13 14

levels(b1)
#[1] "12" "13" "14"

z <- factor(c("12","13","14","12","12"))
z
#levles(z):12 13 14 thse r now categories

#now we will try to convert them into numeric


#our first inclination is

y <-as.numeric(z)
y
# 1 2 3 1 1 --> these r now treated as categories 1,2,3 z
#12 13 14 12 12

z <- factor(c("12","13","14","12","12"))

z
#--- Correct way

x <- as.numeric(as.character(z))
x

x1 <- factor(x)
x1
z <- c("12","13","14","12","12")

z



#--- Correct way

x <- as.numeric(as.character(z)) x


#FVT Ex
#top six
head(fin$Profit)

str(fin$Profit)
#note Profit a simple scenario

str(fin$Profit)

#notice Rev & Expns are factors and we need to convert them into numeric.

summary(fin$Profit)

fin$Profit <- factor(fin$Profit)
summary(fin$Profit)

fin$Profit <- as.numeric(fin$Profit)
summary(fin$Profit)

head(fin$Profit)

#notice Profit is numeric.

summary(fin)



# *** comment all the factors now and run upto ***

#***

#Rev & Exp are numeric data treated as factors.
?gsub
#Pattern Matching and Replacementgrep, grepl, regexpr, gregexpr and regexec search for matches
#to argument pattern within each element of a character vector: they differ in the format of 
#and amount of detail in the results.
?sub

#when we use gsub it already converts a factor into chars
head(fin$Expenses)

mbh <- "Mera Bharath Mahaan Mera Bharath Mahaan" 

sub("Mera","Hamara",mbh)
#notice by using this cmmd we replace the Mear with Hamara.

gsub("Mera","Hamara",mbh)
#gsub did the similar thing.

fin$Expenses <- gsub("Dollers","",fin$Expenses)

head(fin$Expenses)
#[1] "1,130,700 Dollars" "804,035 Dollars"   "1,044,375 Dollars" 
#"4,631,808 Dollars" "4,374,841 Dollars" "4,626,275 Dollars"

#by using above cmmd we add Dollars after numeric value.

fin$Expenses <- gsub(",","",fin$Expenses)
head(fin$Expenses)
#we remove , between numbers.

str(fin$Expenses)
#chr [1:500] "1130700 Dollars" "804035 Dollars" "1044375 Dollars" 
#"4631808 Dollars" "4374841 Dollars" "4626275 Dollars" ...
#notice now Expences no longer a factor but a chars.

fin$Revenue <- gsub("$","",fin$Revenue)
head(fin$Revenue)
#[1] "$9,684,527 "  "$14,016,543 " "$9,746,272 "  "$15,359,369 " "$8,567,910 "  "$12,805,452 "
#notice#ntc $ is still there as it is a special chr

#v need to use esc

fin$Revenue <- gsub("\\$","",fin$Revenue)

head(fin$Revenue)
#[1] "9,684,527 "  "14,016,543 " "9,746,272 "  "15,359,369 " "8,567,910 "  "12,805,452 "

fin$Revenue <- gsub(",","",fin$Revenue)
head(fin$Revenue)
#[1] "9684527 "  "14016543 " "9746272 "  "15359369 " "8567910 "  "12805452 "
#remove , .
str(fin$Revenue)
#now it is chr
#chr [1:500] "9684527 " "14016543 " "9746272 " "15359369 " "8567910 " "12805452 " "5387469 " "" 
#"11757018 " "12329371 " ...

#we repeat the same for growth
head(fin$Growth)

fin$Growth <- gsub("%","",fin$Growth)
head(fin$Growth)
#[1] "19" "20" "16" "19" "19" "22"


str(fin$Growth)

#so three of vars are now chars

#which means we can convert them into numeric.

#it is more convenient to convert chars into numeric.

#rather than factor into numeric.

fin$Expenses <- as.numeric(fin$Expenses)

fin$Revenue <- as.numeric(fin$Revenue)

fin$Growth <- as.numeric(fin$Growth)

#notice now revenue, expences and growth are  numeric
str(fin)
#'data.frame':	500 obs. of  11 variables:
# $ ID       : Factor w/ 500 levels "1","2","3","4",..: 1 2 3 4 5 6 7 8 9 10 ...
#$ Name     : Factor w/ 500 levels "Abstractedchocolat",..: 297 451 168 40 485 199 435 339 242 395 ...
#$ Industry : Factor w/ 8 levels "","Construction",..: 8 6 7 6 8 6 3 2 6 3 ...
#$ Inception: Factor w/ 16 levels "1999","2000",..: 8 11 14 13 15 15 11 15 11 12 ...
#$ Employees: int  25 36 NA 66 45 60 116 73 55 25 ...
#$ State    : Factor w/ 43 levels "","AL","AZ","CA",..: 37 34 36 4 42 28 23 30 4 9 ...
#$ City     : Factor w/ 297 levels "Addison","Alexandria",..: 94 181 105 195 151 154 53 295 232 26 ...
#$ Revenue  : num  9684527 14016543 9746272 15359369 8567910 ...
#$ Expenses : num  NA NA NA NA NA NA NA NA NA NA ...
#$ Profit   : num  342 476 348 420 150 321 125 NA 195 446 ...
#$ Growth   : num  19 20 16 19 19 22 17 NA 30 20 ...
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

#locating missing data
head(fin,24)

#ID            Name            Industry Inception Employees State           City  Revenue Expenses Profit Growth
#1   1        Over-Hex            Software      2006        25    TN       Franklin  9684527       NA    342     19
#2   2       Unimattax         IT Services      2009        36    PA Newtown Square 14016543       NA    476     20
#3   3        Greenfax              Retail      2012        NA    SC     Greenville  9746272       NA    348     16
#4   4       Blacklane         IT Services      2011        66    CA         Orange 15359369       NA    420     19
#5   5        Yearflex            Software      2013        45    WI        Madison  8567910       NA    150     19
#6   6    Indigoplanet         IT Services      2013        60    NJ      Manalapan 12805452       NA    321     22
#7   7         Treslam  Financial Services      2009       116    MO        Clayton  5387469       NA    125     17
#8   8       Rednimdox        Construction      2013        73    NY       Woodside       NA       NA     NA     NA
#9   9         Lamtone         IT Services      2009        55    CA      San Ramon 11757018       NA    195     30
#10 10       Stripfind  Financial Services      2010        25    FL     Boca Raton 12329371       NA    446     20
#11 11 Canecorporation              Health      2012         6             New York 10597009       NA    115      7
#12 12        Mattouch         IT Services      2013         6    WA       Bellevue 14026934       NA    254     26
#13 13       Techdrill              Health      2009         9    MS        Flowood 10573990       NA    120      8
#14 14        Techline                          2006        65    CA      San Ramon 13898119       NA    338     23
#15 15         Cityace                          2010        25    CO     Louisville  9254614       NA    114      6
#16 16  Kayelectronics              Health      2009       687    NC        Clayton  9451943       NA    206      4
#17 17         Ganzlax         IT Services      2011        75    NJ         Iselin 14001180       NA    454     18
#18 18     Trantraxlax Government Services      2011        35    VA        Suffolk 11088336       NA    201      7
#19 19           E-Zim              Retail      2008       320    OH         Monroe 10746451       NA    227     13
#20 20        Daltfase            Software      2011        78    NC         Durham 10410628       NA    151     17
#21 21         Hotlane Government Services      2012        87    AL     Huntsville  7978332       NA     87      2
#22 22      Lathotline              Health      <NA>       103    VA         McLean  9418303       NA     74      2
#23 23          Lambam         IT Services      2012       210    SC       Columbia 11950148       NA    303     20
#24 24          Quozap            Software      2004        21    NJ   Collingswood  8304480       NA     45     20

?complete.cases

#Find Complete Cases
#Description
#Return a logical vector indicating which cases are complete, i.e., have no missing values.

complete.cases(fin)
#returens a vec of ture or false,
#checking to see if there are nas or not in row.

#now we will to look at subset of DF

!complete.cases(fin)

fin[!complete.cases(fin),]
#ID                 Name            Industry Inception Employees State               City  Revenue Expenses Profit Growth
#1     1             Over-Hex            Software      2006        25    TN           Franklin  9684527       NA    342     19
#2     2            Unimattax         IT Services      2009        36    PA     Newtown Square 14016543       NA    476     20
#3     3             Greenfax              Retail      2012        NA    SC         Greenville  9746272       NA    348     16
#4     4            Blacklane         IT Services      2011        66    CA             Orange 15359369       NA    420     19
#5     5             Yearflex            Software      2013        45    WI            Madison  8567910       NA    150     19
#6     6         Indigoplanet         IT Services      2013        60    NJ          Manalapan 12805452       NA    321     22
#7     7              Treslam  Financial Services      2009       116    MO            Clayton  5387469       NA    125     17
#8     8            Rednimdox        Construction      2013        73    NY           Woodside       NA       NA     NA     NA
#9     9              Lamtone         IT Services      2009        55    CA          San Ramon 11757018       NA    195     30
#10   10            Stripfind  Financial Services      2010        25    FL         Boca Raton 12329371       NA    446     20
#11   11      Canecorporation              Health      2012         6                 New York 10597009       NA    115      7
#12   12             Mattouch         IT Services      2013         6    WA           Bellevue 14026934       NA    254     26
#13   13            Techdrill              Health      2009         9    MS            Flowood 10573990       NA    120      8
#14   14             Techline                          2006        65    CA          San Ramon 13898119       NA    338     23
#15   15              Cityace                          2010        25    CO         Louisville  9254614       NA    114      6
#16   16       Kayelectronics              Health      2009       687    NC            Clayton  9451943       NA    206      4
#17   17              Ganzlax         IT Services      2011        75    NJ             Iselin 14001180       NA    454     18
#18   18          Trantraxlax Government Services      2011        35    VA            Suffolk 11088336       NA    201      7
#19   19                E-Zim              Retail      2008       320    OH             Monroe 10746451       NA    227     13
#20   20             Daltfase            Software      2011        78    NC             Durham 10410628       NA    151     17
#21   21              Hotlane Government Services      2012        87    AL         Huntsville  7978332       NA     87      2
#22   22           Lathotline              Health      <NA>       103    VA             McLean  9418303       NA     74      2
#23   23               Lambam         IT Services      2012       210    SC           Columbia 11950148       NA    303     20
#24   24               Quozap            Software      2004        21    NJ       Collingswood  8304480       NA     45     20
#5   25             Tampware        Construction      2011        13    TX            Houston  9785982       NA    279     11
#26   26              Dalthow              Health      2000        20    GA             Dacula 10800718       NA    117      7
#27   27             Ranktech Government Services      2010       607    FL              Tampa 10515557       NA    118      8
#28   28               Unadex            Software      2013       280    NC               Cary  5231275       NA    106     19
#29   29           Groovecane        Construction      2011        17    UT       South Jordan  6811168       NA    123     15
#30   30              Tambase            Software      2010        29    AZ         Scottsdale  9141817       NA    269     21
#31   31           Georedfase         IT Services      2008        19    VA             Vienna 13165222       NA    463     16
#32   32          Konktraxbam            Software      2011         3    WI           Franklin 11504780       NA    276     19
#33   33            Stanquote         IT Services      2011       133    IL        Des Plaines 15421180       NA    491     26
#34   34          Lexiholding              Health      2011        10    CA      Newport Beach  6595798       NA     62      7
#35   35             Mediahex         IT Services      2005        29    TX            Houston 14772570       NA    436     19
#36   36              Triojob  Financial Services      2011        33    TX             Dallas  9403633       NA    370     18
#37   37            D-Zoocare  Financial Services      2010        98    WA            Seattle  9153440       NA    264     13
#38   38             Zun-Trax              Retail      2013        23    SC           Columbia  9732190       NA    197     12
#39   39              Biotain        Construction      2012        62    IA          Davenport 11642543       NA    278     13
#40   40             Newjofix  Financial Services      2010        90    CA     West Hollywood 12339863       NA    429     19
#41   41             Ozer-Dox              Health      2013        35    GA             Duluth  9621471       NA    107      9
#42   42                Iscom              Health      2013       595    CT      West Hartford  8027658       NA     33      8
#43   43               Istone            Software      2011        50    VA             Reston  4424720       NA    143     20
#44   44            Ganzgreen        Construction      2010       224    TN           Franklin       NA       NA     NA      9
#45   45             Zamhouse        Construction      2009        39    ME       Lisbon Falls  7543695       NA     39     12
#46   46            Openjocon        Construction      2013        75    IL         Midlothian 11374343       NA    286     13
#47   47              Trisity              Health      2012        26    CA          San Diego  6918290       NA     24      0
#48   48            Planetice              Health      2012        42    MD      Silver Spring 10757724       NA    145      4
#49   49             Villadox        Construction      2012        20    CA           Carlsbad  8651649       NA    301     11
#50   50            Alphacane              Retail      2013         3    MO           O'Fallon  7903763       NA     78     14
#51   51             Rankcone Government Services      2011        36    VA     Virginia Beach  6036944       NA     41      6
#52   52               Iceice Government Services      2010        21    WV          Star City  6352466       NA    175      6
#53   53          Fixquadtech              Health      2012        85    PA       Philadelphia  8299901       NA     50      8
#54   54              Zonhigh         IT Services      2010        96    IL            Chicago 12723684       NA    323     21
#55   55             Toughway  Financial Services      2010       219    FL     St. Petersburg 13442136       NA    398     19
#56   56            Bluetexon         IT Services      2010       117    TX              Plano 12685910       NA    155     18
#57   57          Nimvivafind  Financial Services      2009        34    NJ             Newark 11605855       NA    360     19
#58   58             Eremenko  Financial Services      2012        60    FL           Maitland 11445633       NA    327     15
#59   59        Hot-Electrics         IT Services      2006        46    GA            Augusta 17214068       NA    495     16
#60   60               Namdom            Software      2013       105    IL            Chicago  8362411       NA    216     19
#61   61              Tempbam            Software      2013       134    WA            Seattle  8980591       NA    108     25
#62   62            Goodhouse         IT Services      2009        63    VA            Herndon 14833220       NA    367     24
#63   63            Sumzoomit        Construction      2010        32    MO       Lee's Summit 18429577       NA    419     19
#64   64              Goodtex Government Services      2011       150    VA      Tysons Corner 13118996       NA    124     -3
#65   65             Ranquote              Health      2013       400    GA         Alpharetta  7147363       NA    110      6
#66   66             Zathtone            Software      2009       121    NY           New York  8953759       NA    174     21
#67   67             Vivacode        Construction      2009        28    LA       Lake Charles  9410642       NA    196      5
#68   68              Dongcom              Retail      2002         8    NY        Cheektowaga 14477085       NA    450     10
#69   69             Hexhouse            Software      2006       668    MA          Cambridge 10221740       NA    330     14
#70   70           Jobzencane            Software      2011        40    PA              WAYNE  7482411       NA    183     21
#71   71             Sailtech            Software      2012       850    CA        Santa Clara  4543509       NA      4     21
#72   72              Vilacan              Retail      1999        28    UT               Orem 12916975       NA    282     12
#73   73           Stattechno              Health      2014        80    WA            Seattle  6619705       NA     98     10
#74   74                Conin        Construction      2009        23    CA   Rancho Dominguez  9903489       NA    140      8
#75   75            Rezumfind         IT Services      2000        50    VA            Herndon 14024010       NA    428     23
#76   76             Xx--Fase         IT Services      2012       430    TN          Nashville 14048981       NA    397     25
#77   77              Stiming         IT Services      2014        24    NY      Williamsville  9779076       NA    371     22
#78   78                E-Can  Financial Services      2013      1628    NJ       Mount Laurel  8218086       NA    193     16
#79   79               Tonjob  Financial Services      2010        87    CA      Santa Barbara  8475261       NA    234     16
#80   80             Flextone  Financial Services      2010       250    FL         Boca Raton 10335149       NA    308     19
#81   81              Lineity Government Services      2006       113    MA          Billerica  8621837       NA    238      4
#82   82            Voyadexon              Health      2010       545    TX             Dallas  8913061       NA     11      8
#83   83             Xn-Media              Health      2012       104    NJ          Lyndhurst  7863279       NA     75      5
#84   84           Drilldrill            Software      2010        30            San Francisco  7800620       NA    182     17
#85   85             Tristone        Construction      2013        43    MD       Millersville 11755980       NA    326      8
#86   86        Treeelectrics Government Services      2013       485    VA        Clarksville 12208678       NA    261     -2
#87   87               Tontam        Construction      2007        26    VA            Ashburn  7635932       NA     22      8
#88   88             Ganjatam         IT Services      2009        70    NJ             Iselin 16195183       NA    435     18
#89   89               Sumice              Retail      2013       318    UT              Sandy  8697300       NA    116     19
#90   90              Vivadom            Software      2010        72    CA      Santa Barbara  5190812       NA     57     17
#[ reached getOption("max.print") -- omitted 410 rows ]


#note we got 6 rows

#*** 
head(fin,24) 
nrow(fin)

#fin <- read.csv("Future-500.csv")

fin <- read.csv("Future-500.csv", na.strings = c(""))
head(fin,24)
# v cld also treat NY as NA

fin$Expenses <- gsub(" Dollars","",fin$Expenses)
fin$Expenses <- gsub(",","",fin$Expenses)
fin$Revenue <- gsub("\\$","",fin$Revenue)
fin$Revenue <- gsub(",","",fin$Revenue)
fin$Growth <- gsub("%","",fin$Growth)
fin$Expenses <- as.numeric(fin$Expenses)
fin$Revenue <- as.numeric(fin$Revenue)
fin$Growth <- as.numeric(fin$Growth)

fin[!complete.cases(fin),]
#ID            Name           Industry Inception Employees State          City  Revenue Expenses   Profit Growth
#3     3        Greenfax             Retail      2012        NA    SC    Greenville  9746272  1044375  8701897     16
#8     8       Rednimdox       Construction      2013        73    NY      Woodside       NA       NA       NA     NA
#11   11 Canecorporation             Health      2012         6  <NA>      New York 10597009  7591189  3005820      7
#14   14        Techline               <NA>      2006        65    CA     San Ramon 13898119  5470303  8427816     23
#15   15         Cityace               <NA>      2010        25    CO    Louisville  9254614  6249498  3005116      6
#17   17         Ganzlax        IT Services      2011        75    NJ        Iselin 14001180       NA 11901180     18
#22   22      Lathotline             Health        NA       103    VA        McLean  9418303  7567233  1851070      2
#44   44       Ganzgreen       Construction      2010       224    TN      Franklin       NA       NA       NA      9
#84   84      Drilldrill           Software      2010        30  <NA> San Francisco  7800620  2785799  5014821     17
#267 267      Circlechop           Software      2010        14  <NA> San Francisco  9067070  5929828  3137242     20
#332 332     Westminster Financial Services      2010        NA    MI          Troy 11861652  5245126  6616526     15
#379 379       Stovepuck             Retail      2013        73  <NA>      New York 13814975  5904502  7910473     10

#now notice it picks up more rows for NAs

#wht is the diff btw <NA> & NA

str(fin)
#differnce is <NA> treated as Factor and NA is Treated as Numeric.

#Filtering: using which() for non-missing data 
head(fin)

fin[!complete.cases(fin),]


#lets say we want every single row with rev 9746272 fin$Revenue == 9746272

fin[fin$Revenue==9746272,]
#ID     Name Industry Inception Employees State       City Revenue Expenses  Profit Growth
#3     3 Greenfax   Retail      2012        NA    SC Greenville 9746272  1044375 8701897     16
#NA   NA     <NA>     <NA>        NA        NA  <NA>       <NA>      NA       NA      NA     NA
#NA.1 NA     <NA>     <NA>        NA        NA  <NA>       <NA>      NA       NA      NA     NA
#so why r there so many NAs in the 2 rows below

NA == 9746272



9746272 == NA


?which
#Which indices are TRUE?
#Description
#Give the TRUE indices of a logical object, allowing for array indices.

fin[fin$Revenue == 9746272,]

which(fin$Revenue==9746272)
#[1] 3

fin[which(fin$Revenue==9746272),]
#ID     Name Industry Inception Employees State       City Revenue Expenses  Profit Growth
#3  3 Greenfax   Retail      2012        NA    SC Greenville 9746272  1044375 8701897     16

#now we are passing this

#this is the se cond approach

#fin[c(3,4,5),]
#lets take another ex head(fin)
#ntc 3rd row empls cols is NA
#if we want all the columns which have 45 employess

#ntc 2 NAs

#1 is NA

# 2nd is NA.1


filter = fin$Employees == 45
fin[filter,]
#ID           Name     Industry Inception Employees State          City  Revenue Expenses   Profit Growth
#NA    NA           <NA>         <NA>        NA        NA  <NA>          <NA>       NA       NA       NA     NA
#5      5       Yearflex     Software      2013        45    WI       Madison  8567910  4374841  4193069     19
#137  137      Toughcare       Retail      2009        45    CA       Burbank 12429629  5796075  6633554     14
#183  183         Ittech  IT Services      2013        45    MN   Minneapolis 11133739  6544488  4589251     20
#200  200         Lalane       Retail      2003        45    MN Golden Valley 12461526  4934351  7527175     14
#208  208  Countslovenly Construction      2010        45    FL   Spring Hill  8380367  8213905   166462     10
#245  245  Peskyevaluate  IT Services      2010        45    VA      Richmond 13011611  4284410  8727201     23
#NA.1  NA           <NA>         <NA>        NA        NA  <NA>          <NA>       NA       NA       NA     NA
#360  360 Remembergabbro Construction      2012        45    UT        Lindon 10878578  4515112  6363466     12
#380  380      Pickyfive  IT Services      2011        45    CO        Denver 14826723  4458447 10368276     26
#435  435   Lucrepickled  IT Services      2004        45    VA    Glen Allen 12894933  3512395  9382538     17
#487  487       Genusequ Construction      2007        45    NC    Greensboro  8498464  5741773  2756691     11

fin[which(filter),]
#ID           Name     Industry Inception Employees State          City  Revenue Expenses   Profit Growth
#5     5       Yearflex     Software      2013        45    WI       Madison  8567910  4374841  4193069     19
#137 137      Toughcare       Retail      2009        45    CA       Burbank 12429629  5796075  6633554     14
#183 183         Ittech  IT Services      2013        45    MN   Minneapolis 11133739  6544488  4589251     20
#200 200         Lalane       Retail      2003        45    MN Golden Valley 12461526  4934351  7527175     14
#208 208  Countslovenly Construction      2010        45    FL   Spring Hill  8380367  8213905   166462     10
#245 245  Peskyevaluate  IT Services      2010        45    VA      Richmond 13011611  4284410  8727201     23
#360 360 Remembergabbro Construction      2012        45    UT        Lindon 10878578  4515112  6363466     12
#380 380      Pickyfive  IT Services      2011        45    CO        Denver 14826723  4458447 10368276     26
#435 435   Lucrepickled  IT Services      2004        45    VA    Glen Allen 12894933  3512395  9382538     17
#487 487       Genusequ Construction      2007        45    NC    Greensboro  8498464  5741773  2756691     11

#notic NAs are gone


#***


#filtering: using is.na() for missing data

#now we will pick up those rows whic have NAs 
head(fin)
#ID         Name    Industry Inception Employees State           City  Revenue Expenses   Profit Growth
#1  1     Over-Hex    Software      2006        25    TN       Franklin  9684527  1130700  8553827     19
#2  2    Unimattax IT Services      2009        36    PA Newtown Square 14016543   804035 13212508     20
#3  3     Greenfax      Retail      2012        NA    SC     Greenville  9746272  1044375  8701897     16
#4  4    Blacklane IT Services      2011        66    CA         Orange 15359369  4631808 10727561     19
#5  5     Yearflex    Software      2013        45    WI        Madison  8567910  4374841  4193069     19
#6  6 Indigoplanet IT Services      2013        60    NJ      Manalapan 12805452  4626275  8179177     22

#notice row number have NA value.

fin$Expenses == NA
fin$Expenses == NA
#[1] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
#[36] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
#[71] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
#[106] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
#[141] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
#[176] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
#[211] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
#[246] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
#[281] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
#[316] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
#[351] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
#[386] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
#[421] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
#[456] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
#[491] NA NA NA NA NA NA NA NA NA NA
#this is how the filter looks

?is.na
#‘Not Available’ / Missing Values
#NA is a logical constant of length 1 which contains a missing value indicator. NA can be coerced to any other 
#vector type except raw. There are also constants NA_integer_, NA_real_, NA_complex_ and NA_character_ of 
#the other atomic vector types which support missing values: all of these are reserved words in the R 
#language.

a <- c(1,24,56,NA,76)
a

is.na(a)
#[1] FALSE FALSE FALSE  TRUE FALSE

is.na(fin$Expenses)
#[1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE
#[18] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[35] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[52] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[69] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[86] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[103] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[120] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[137] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[154] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[171] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[188] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[205] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[222] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[239] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[256] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[273] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[290] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[307] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[324] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[341] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[358] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[375] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[392] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[409] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[426] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[443] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[460] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[477] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
#[494] FALSE FALSE FALSE FALSE FALSE FALSE FALSE


#fin[is.na(fin$Expenses),]
fin[is.na(fin$Expenses),]
#ID      Name     Industry Inception Employees State     City  Revenue Expenses   Profit Growth
#8   8 Rednimdox Construction      2013        73    NY Woodside       NA       NA       NA     NA
#17 17   Ganzlax  IT Services      2011        75    NJ   Iselin 14001180       NA 11901180     18
#44 44 Ganzgreen Construction      2010       224    TN Franklin       NA       NA       NA      9

#notice we get exact 3 rows and all of them have expenses as NA

#repeat this process for state col or other cols.
fin_backup <- fin
nrow(fin)

fin[!complete.cases(fin),]
#this will give us akk the rows

#which have NAs in some or other cols

fin[is.na(fin$Industry),]
#ID     Name Industry Inception Employees State       City  Revenue Expenses  Profit Growth
#14 14 Techline     <NA>      2006        65    CA  San Ramon 13898119  5470303 8427816     23
#15 15  Cityace     <NA>      2010        25    CO Louisville  9254614  6249498 3005116      6

#this give which rows are nas for industry col

head(fin,20)
nrow(fin[is.na(fin$Industry),])
#[1] 2
nrow(fin[!complete.cases(fin),])
#[1] 12

nrow(fin[!complete.cases(fin$Industry),])

nrow(fin)
#[1]500

fin <- fin[!is.na(fin$Industry),]
nrow(fin)
#[1] 498
head(fin,20)


fin[!complete.cases(fin),]
fin[!complete.cases(fin),]
#ID            Name           Industry Inception Employees State          City  Revenue Expenses   Profit Growth
#3     3        Greenfax             Retail      2012        NA    SC    Greenville  9746272  1044375  8701897     16
#8     8       Rednimdox       Construction      2013        73    NY      Woodside       NA       NA       NA     NA
#11   11 Canecorporation             Health      2012         6  <NA>      New York 10597009  7591189  3005820      7
#17   17         Ganzlax        IT Services      2011        75    NJ        Iselin 14001180       NA 11901180     18
#22   22      Lathotline             Health        NA       103    VA        McLean  9418303  7567233  1851070      2
#44   44       Ganzgreen       Construction      2010       224    TN      Franklin       NA       NA       NA      9
#84   84      Drilldrill           Software      2010        30  <NA> San Francisco  7800620  2785799  5014821     17
#267 267      Circlechop           Software      2010        14  <NA> San Francisco  9067070  5929828  3137242     20
#332 332     Westminster Financial Services      2010        NA    MI          Troy 11861652  5245126  6616526     15
#379 379       Stovepuck             Retail      2013        73  <NA>      New York 13814975  5904502  7910473     10

#verify rows 14 & 15 hv been dealt with and not there

#Resetting the DF index

rownames(fin)
nrow(fin)

1:nrow(fin)
head(fin,20)

rownames(fin) <- 1:nrow(fin)


View(fin)
#now ntc the row indx is 498 diff from ID  col
# another alt way is View(fin_backup)
fin <- fin_backup
nrow(fin)
fin[!complete.cases(fin),]
fin[is.na(fin$Industry),] # gvs which rows r empty
#14 14 Techline     <NA>      2006        65    CA  San Ramon 13898119  5470303 8427816     23
#15 15  Cityace     <NA>      2010        25    CO Louisville  9254614  6249498 3005116      6

fin <- fin[!is.na(fin$Industry),]
#15 15  Cityace     <NA>      2010        25    CO Louisville  9254614  6249498 3005116      6

head(fin,15)
#ID            Name           Industry Inception Employees State           City  Revenue Expenses   Profit Growth
#1   1        Over-Hex           Software      2006        25    TN       Franklin  9684527  1130700  8553827     19
#2   2       Unimattax        IT Services      2009        36    PA Newtown Square 14016543   804035 13212508     20
#3   3        Greenfax             Retail      2012        NA    SC     Greenville  9746272  1044375  8701897     16
#4   4       Blacklane        IT Services      2011        66    CA         Orange 15359369  4631808 10727561     19
#5   5        Yearflex           Software      2013        45    WI        Madison  8567910  4374841  4193069     19
#6   6    Indigoplanet        IT Services      2013        60    NJ      Manalapan 12805452  4626275  8179177     22
#7   7         Treslam Financial Services      2009       116    MO        Clayton  5387469  2127984  3259485     17
#8   8       Rednimdox       Construction      2013        73    NY       Woodside       NA       NA       NA     NA
#9   9         Lamtone        IT Services      2009        55    CA      San Ramon 11757018  6482465  5274553     30
#10 10       Stripfind Financial Services      2010        25    FL     Boca Raton 12329371   916455 11412916     20
#11 11 Canecorporation             Health      2012         6  <NA>       New York 10597009  7591189  3005820      7
#12 12        Mattouch        IT Services      2013         6    WA       Bellevue 14026934  7429377  6597557     26
#13 13       Techdrill             Health      2009         9    MS        Flowood 10573990  7435363  3138627      8
#16 16  Kayelectronics             Health      2009       687    NC        Clayton  9451943  3878113  5573830      4
#17 17         Ganzlax        IT Services      2011        75    NJ         Iselin 14001180       NA 11901180     18


rownames(fin) <- NULL
head(fin,15)
#now row names chnaged.

head(fin,15)


# v r telling R to set the rownames

#this is not nece but good to know


#Factual Analysis: Replacing missing Data 
fin[!complete.cases(fin),]
fin[is.na(fin$State),]

#ntc state and city
#ID            Name Industry Inception Employees State          City  Revenue Expenses  Profit Growth
#11   11 Canecorporation   Health      2012         6  <NA>      New York 10597009  7591189 3005820      7
#82   84      Drilldrill Software      2010        30  <NA> San Francisco  7800620  2785799 5014821     17
#265 267      Circlechop Software      2010        14  <NA> San Francisco  9067070  5929828 3137242     20
#377 379       Stovepuck   Retail      2013        73  <NA>      New York 13814975  5904502 7910473     10

fin[is.na(fin$State) & fin$City=="New York",]
#15 15  Cityace     <NA>      2010        25    CO Louisville  9254614  6249498 3005116      6

fin[is.na(fin$State) & fin$City=="New York","State"] <- "NY"
#15 15  Cityace     <NA>      2010        25    CO Louisville  9254614  6249498 3005116      6

fin[is.na(fin$State),]
#ntc state and city

fin[is.na(fin$State) & fin$City=="New York",]
fin[is.na(fin$State) & fin$City=="New York","State"] <- "NY"
fin[is.na(fin$State),]
fin[is.na(fin$State) & fin$City=="New York",]
#ID            Name Industry Inception Employees State     City  Revenue Expenses  Profit Growth
#11   11 Canecorporation   Health      2012         6    NY New York 10597009  7591189 3005820      7
#377 379       Stovepuck   Retail      2013        73    NY New York 13814975  5904502 7910473     10
#check manually
fin[c(11,377),]


fin[!complete.cases(fin),]

fin[is.na(fin$State) & fin$City=="San Francisco",]
#ID       Name Industry Inception Employees State          City Revenue Expenses  Profit Growth
#82   84 Drilldrill Software      2010        30  <NA> San Francisco 7800620  2785799 5014821     17
#265 267 Circlechop Software      2010        14  <NA> San Francisco 9067070  5929828 3137242     20

#ntc this is getting smaller everytime


#***

#Median imputation method


fin[!complete.cases(fin),]

#ID        Name           Industry Inception Employees State       City  Revenue Expenses   Profit Growth
#3     3    Greenfax             Retail      2012        NA    SC Greenville  9746272  1044375  8701897     16
#8     8   Rednimdox       Construction      2013        73    NY   Woodside       NA       NA       NA     NA
#15   17     Ganzlax        IT Services      2011        75    NJ     Iselin 14001180       NA 11901180     18
#20   22  Lathotline             Health        NA       103    VA     McLean  9418303  7567233  1851070      2
#42   44   Ganzgreen       Construction      2010       224    TN   Franklin       NA       NA       NA      9
#330 332 Westminster Financial Services      2010        NA    MI       Troy 11861652  5245126  6616526     15

median(fin[,"Employees"])

#[1] NA

median(fin[,"Employees"], na.rm=TRUE)
#[1] 56
#we calculate the median of Employees col

mean(fin[,"Employees"], na.rm=TRUE)
#mean


fin[!complete.cases(fin),]
#ID        Name           Industry Inception Employees State       City  Revenue Expenses   Profit Growth
#3     3    Greenfax             Retail      2012        NA    SC Greenville  9746272  1044375  8701897     16
#8     8   Rednimdox       Construction      2013        73    NY   Woodside       NA       NA       NA     NA
#15   17     Ganzlax        IT Services      2011        75    NJ     Iselin 14001180       NA 11901180     18
#20   22  Lathotline             Health        NA       103    VA     McLean  9418303  7567233  1851070      2
#42   44   Ganzgreen       Construction      2010       224    TN   Franklin       NA       NA       NA      9
#330 332 Westminster Financial Services      2010        NA    MI       Troy 11861652  5245126  6616526     15


median(fin[fin$Industry=="Retail","Employees"],  na.rm=TRUE)
#[1] 28

mean(fin[fin$Industry=="Retail","Employees"],  na.rm=TRUE)
#[1] 209.2766

med_emp_retail <- median(fin[fin$Industry=="Retail","Employees"], na.rm=TRUE)
fin[is.na(fin$Employees) & fin$Industry=="Retail","Employees"] <- med_emp_retail
#check
fin[3,]
#ID     Name Industry Inception Employees State       City Revenue Expenses  Profit Growth
#3  3 Greenfax   Retail      2012        28    SC Greenville 9746272  1044375 8701897     16

#repeat this same process for Financial services



mean(fin[,"Employees"], na.rm=TRUE)



mean(fin[fin$Industry=="Financial  Services","Employees"],na.rm=TRUE)



median(fin[,"Employees"], na.rm=TRUE)



median(fin[fin$Industry=="Financial  Services","Employees"],na.rm=TRUE)



med_empl_finserv <- median(fin[fin$Industry=="Financial Services","Employees"],na.rm=TRUE)



fin[is.na(fin$Employees) & fin$Industry=="Financial Services",]



fin[is.na(fin$Employees) & fin$Industry=="Financial Services","Employees"] <- med_empl_finserv
fin[330,]
#ID        Name           Industry Inception Employees State City  Revenue Expenses  Profit Growth
#330 332 Westminster Financial Services      2010        80    MI Troy 11861652  5245126 6616526     15

head(fin)



str(fin)
































#***



fin[!complete.cases(fin),]
#ID       Name     Industry Inception Employees State     City  Revenue Expenses   Profit Growth
#8   8  Rednimdox Construction      2013        73    NY Woodside       NA       NA       NA     NA
#15 17    Ganzlax  IT Services      2011        75    NJ   Iselin 14001180       NA 11901180     18
#20 22 Lathotline       Health        NA       103    VA   McLean  9418303  7567233  1851070      2
#42 44  Ganzgreen Construction      2010       224    TN Franklin       NA       NA       NA      9

#Growth col

med_growth_constr <- median(fin[fin$Industry=="Construction","Growth"],na.rm=TRUE)



fin[is.na(fin$Growth) & fin$Industry=="Construction","Growth"] <- med_growth_constr

#check 
fin[8,]
#ID      Name     Industry Inception Employees State     City Revenue Expenses Profit Growth
#8  8 Rednimdox Construction      2013        73    NY Woodside      NA       NA     NA     10

fin[!complete.cases(fin),]

#ID       Name     Industry Inception Employees State     City  Revenue Expenses   Profit Growth
#8   8  Rednimdox Construction      2013        73    NY Woodside       NA       NA       NA     10
#15 17    Ganzlax  IT Services      2011        75    NJ   Iselin 14001180       NA 11901180     18
#20 22 Lathotline       Health        NA       103    VA   McLean  9418303  7567233  1851070      2
#42 44  Ganzgreen Construction      2010       224    TN Franklin       NA       NA       NA      9

#Mini exrcise

#Revenue

med_rev_constr <- median(fin[fin$Industry=="Construction","Revenue"],na.rm=TRUE) 
med_rev_constr
#[1]9055058





fin[is.na(fin$Revenue) & fin$Industry=="Construction",]

#ID      Name     Industry Inception Employees State     City Revenue Expenses Profit Growth
#8   8 Rednimdox Construction      2013        73    NY Woodside      NA       NA     NA     10
#42 44 Ganzgreen Construction      2010       224    TN Franklin      NA       NA     NA      9

fin[is.na(fin$Revenue) & fin$Industry=="Construction","Revenue"]<-med_rev_constr



fin[is.na(fin$Revenue) & fin$Industry=="Construction",]

#



fin[!complete.cases(fin),]

#ID       Name     Industry Inception Employees State     City  Revenue Expenses   Profit Growth
#8   8  Rednimdox Construction      2013        73    NY Woodside  9055059       NA       NA     10
#15 17    Ganzlax  IT Services      2011        75    NJ   Iselin 14001180       NA 11901180     18
#20 22 Lathotline       Health        NA       103    VA   McLean  9418303  7567233  1851070      2
#42 44  Ganzgreen Construction      2010       224    TN Franklin  9055059       NA       NA      9

#Expenses

#ntc v get 4 rows



med_exp_constr <- median(fin[fin$Industry=="Construction","Expenses"],na.rm=TRUE) 
med_exp_constr

#[1] 4506976


fin[is.na(fin$Expenses) & fin$Industry=="Construction",]

#ID      Name     Industry Inception Employees State     City Revenue Expenses Profit Growth
#8   8 Rednimdox Construction      2013        73    NY Woodside 9055059       NA     NA     10
#42 44 Ganzgreen Construction      2010       224    TN Franklin 9055059       NA     NA      9
fin[is.na(fin$Expenses) & fin$Industry=="Construction","Expenses"] <- med_exp_constr



fin[!complete.cases(fin),]
#8   8  Rednimdox Construction      2013        73    NY Woodside  9055059  4506976       NA     10
#15 17    Ganzlax  IT Services      2011        75    NJ   Iselin 14001180       NA 11901180     18
#20 22 Lathotline       Health        NA       103    VA   McLean  9418303  7567233  1851070      2
#42 44  Ganzgreen Construction      2010       224    TN Franklin  9055059  4506976       NA      9



#*** Deriving vals

#Revenue = Expenses + Profit



fin[is.na(fin$Profit),]

#ID      Name     Industry Inception Employees State     City Revenue Expenses Profit Growth
#8   8 Rednimdox Construction      2013        73    NY Woodside 9055059  4506976     NA     10
#42 44 Ganzgreen Construction      2010       224    TN Franklin 9055059  4506976     NA      9

vecRev <- fin[is.na(fin$Profit),"Revenue"]
vecRev
#[1] 9055059 9055059

vecExpns <- fin[is.na(fin$Profit),"Expenses"]



vecPrfts <- vecRev - vecExpns



fin[is.na(fin$Profit),"Profit"] <- vecPrfts



fin[c(8,42),]

#ID      Name     Industry Inception Employees State     City Revenue Expenses  Profit Growth
#8   8 Rednimdox Construction      2013        73    NY Woodside 9055059  4506976 4548083     10
#42 44 Ganzgreen Construction      2010       224    TN Franklin 9055059  4506976 4548083      9

fin[!complete.cases(fin),]

#ID       Name    Industry Inception Employees State   City  Revenue Expenses   Profit Growth
#15 17    Ganzlax IT Services      2011        75    NJ Iselin 14001180       NA 11901180     18
#20 22 Lathotline      Health        NA       103    VA McLean  9418303  7567233  1851070      2

fin[is.na(fin$Expense),]
#ID    Name    Industry Inception Employees State   City  Revenue Expenses   Profit Growth
#15 17 Ganzlax IT Services      2011        75    NJ Iselin 14001180       NA 11901180     18

fin[is.na(fin$Expense),"Expenses"] <- fin[is.na(fin$Expense),"Revenue"] - fin[is.na(fin$Expense),"Profit"]



fin[15,]

#ID    Name    Industry Inception Employees State   City  Revenue Expenses   Profit Growth
#15 17 Ganzlax IT Services      2011        75    NJ Iselin 14001180  2100000 11901180     18


fin[!complete.cases(fin),]

#ID       Name Industry Inception Employees State   City Revenue Expenses  Profit Growth
#20 22 Lathotline   Health        NA       103    VA McLean 9418303  7567233 1851070      2

#ntc there is only 1 row



#***

#Visualize results

#scatterplot classified by industry showing rev, expense, profit

#scplt that includes industry trends for the expenses-revenue relationship

#Boxplots showing growth by industry



#install.packages("ggplot2") 
library(ggplot2)


head(fin)

#ID         Name    Industry Inception Employees State           City  Revenue Expenses   Profit Growth
#1  1     Over-Hex    Software      2006        25    TN       Franklin  9684527  1130700  8553827     19
#2  2    Unimattax IT Services      2009        36    PA Newtown Square 14016543   804035 13212508     20
#3  3     Greenfax      Retail      2012        28    SC     Greenville  9746272  1044375  8701897     16
#4  4    Blacklane IT Services      2011        66    CA         Orange 15359369  4631808 10727561     19
#5  5     Yearflex    Software      2013        45    WI        Madison  8567910  4374841  4193069     19
#6  6 Indigoplanet IT Services      2013        60    NJ      Manalapan 12805452  4626275  8179177     22


#scatterplot classified by industry showing rev, expense, profit 

p <- ggplot(data=fin)
p



p + geom_point(aes(x=Revenue, y=Expenses))



p + geom_point(aes(x=Revenue, y=Expenses,colour=Industry, size=10))

#IT Services have High Revenue and low expences
#Construction Industry have High Expences and low revenue
#Health Ind. have High Expences and low revenue.


p + geom_point(aes(x=Revenue, y=Expenses,colour=Industry, size=Profit))



#scplt that includes industry trends for the expenses-revenue relationship



#p + geom_point(aes(x=Revenue, y=Expenses,

#colour=Industry))



#p   + geom_smooth(aes(x=Revenue, y=Expenses,

#colour=Industry))



d <- ggplot(data=fin, aes(x=Revenue, y=Expenses,colour=Industry))



#d + geom_point() + geom_smooth()



d + geom_point() + geom_smooth(fill=NA,size=1.2)

#ntc construction trend



#*** library(ggplot2)
#Boxplots showing growth by industry

f <- ggplot(data=fin,aes(x=Industry, y=Growth, colour=Industry))

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
