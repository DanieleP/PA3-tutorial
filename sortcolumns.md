# How to order a data frame by the values in its columns

Let's read first the cities.csv file

    > data <- read.csv("cities.csv")
    > data
          cities countries areakm2 populationk
    1   Shanghai     China    2643       21766
    2    Beijing     China    1368       21500
    3        NYC       USA    1214        8406
    4         LA       USA    1302        3884
    5     London        UK    1737        9789
    6 Manchester        UK     116         255
    > class(data)
    [1] "data.frame"

As we can see data is a data.frame with 6 rows and 4 columns, both character and numeric.
Below is the function to order the data frame by column:

	  ## orderdata: output data.frame with the ordered rows
	  ## order(): sort by default in decreasing order the values. In case of numbers
	  ## from the smallest to the biggest, in case of characters from A to Z. This 
	  ## function returns a vector of indexes with the ordered rows. 
	  ## > order(data[,1])
	  ## [1] 2 4 5 6 3 1
	  ## data[order(),] subsets the data frame using the indexes above
	  sort_by_column <- function (data, column){
		orderdata <- data[order(data[,column]),]
		return(orderdata)
	  }

Examples:

	  > sort_by_column (data,1)
			cities countries areakm2 populationk
	  2	   Beijing	   China	1368	   21500
	  4			LA		 USA	1302		3884
	  5		London		  UK	1737		9789
	  6 Manchester		  UK	 116		 255
	  3		   NYC		 USA	1214		8406
	  1	  Shanghai	   China	2643	   21766
	  > sort_by_column (data,3)
			cities countries areakm2 populationk
	  6 Manchester		  UK	 116		 255
	  3		   NYC		 USA	1214		8406
	  4			LA		 USA	1302		3884
	  2	   Beijing	   China	1368	   21500
	  5		London		  UK	1737		9789
	  1	  Shanghai	   China	2643	   21766

In case of tie, we might consider to give a second attribute to order() to give a second criteria

	  sort_by_columns <- function (data, col1, col2){
		orderdata <- data[order(data[,col1],data[,col2]),]
		return(orderdata)
	  }

Examples:

	  > sort_by_columns (data,2,3)
			cities countries areakm2 populationk
	  2    Beijing     China    1368       21500
	  1   Shanghai     China    2643       21766
	  6 Manchester        UK     116         255
	  5     London        UK    1737        9789
	  3        NYC       USA    1214        8406
	  4         LA       USA    1302        3884
	  > sort_by_columns (data,2,1)
			cities countries areakm2 populationk
	  2    Beijing     China    1368       21500
	  1   Shanghai     China    2643       21766
	  5     London        UK    1737        9789
	  6 Manchester        UK     116         255
	  4         LA       USA    1302        3884
	  3        NYC       USA    1214        8406
