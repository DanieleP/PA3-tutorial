# How to order only a specific subset of a data frame

Let's read cities.csv.

If our purpose is to see what is the largest city in China between Shanghai and Beijing, we might be not interested
in the other cities'areas. 
To do so we subset our initial data frame, and then we order it considering the criteria we prefer.
It doesn't make much sense with 2 items, but when we are analysing thousands of items it's far more useful.

    ## grep function finds the character vector (e.g. "China") in the
    ## data$countries factor, and returns a vector of indexes. 
    ## > data$countries
    ## [1] China China USA   USA   UK    UK   
    ## Levels: China UK USA
    ## > grep("China",data$countries)
    ## [1] 1 2
    ## We then subset the main data frame, data, by these indexes
    ## > data [grep("China",data$countries),]
    ##     cities countries areakm2 populationk
    ## 1 Shanghai     China    2643       21766
    ## 2  Beijing     China    1368       21500
    sort_country <- function (data, country, column){
      countrydata <- data [grep(country,data$countries),]
      orderdata <- countrydata[order(countrydata[,column]),]
      return (orderdata)
    }

Examples:

    > sort_country(data, "USA", 4)
      cities countries areakm2 populationk
    4     LA       USA    1302        3884
    3    NYC       USA    1214        8406
    > sort_country(data, "UK", 1)
          cities countries areakm2 populationk
    5     London        UK    1737        9789
    6 Manchester        UK     116         255
