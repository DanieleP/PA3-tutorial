# How to return a specific ranking after ordering

Working on cities.csv, we want to know what's the second biggest city in our UK database. 
We are not interested in an ordered data frame, we just want to know the name of the city.

    ## argument decreasing = TRUE inverts the direction of the order. Numbers from biggest to smallest and 
    ## characters from Z to A. This is helpful when we consider rank#1 the biggest city.
    ## as.character () will return the vector with the name of the city. If we just return orderdata[rank,1] 
    ## we get a factor instead.
    find_city_rank <- function(data,column,rank){
        orderdata <- data[order(decreasing = TRUE,data[,column]),]
        return(as.character(orderdata[rank,1]))
    }
    
Examples:

    > find_city_rank (data,3,1)
    [1] "Shanghai"
    > find_city_rank (data,3,2)
    [1] "London"
    > find_city_rank (data,4,2)
    [1] "Beijing"
    
Now let's consider the case in which we don't know the length of the csv file and we just want to get the
last city in the ranking.

    ## nrow() returns the number of rows of a data frame. We use this function to determine the index of the last item.
    find_last_city <- function(data,column){
        orderdata <- data[order(decreasing = TRUE,data[,column]),]
        return(as.character(orderdata[nrow(orderdata),1]))
    }
    
Examples:

    > find_last_city (data,3)
    [1] "Manchester"
    > find_last_city (data,1)
    [1] "Beijing"
  
Note that in the last example Beijing it's the last in alphabetical ranking. This is because decreasing = TRUE.
