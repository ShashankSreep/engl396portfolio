<!-- _sidebar.md -->

## Number One Albums

>**Note**: Comments are marked with a # in the code snippets

```r
# Reads in the album data from the album-rankings csv file
# @Params: 
# - data/album-rankings.csv  => File path to the csv storing album data
# album_data => Stores the csv file’s data into a dataframe

album_data <- read.csv("data/album-rankings.csv")

# Function: For the indicated range between (start, end), returns the albums that were ranked number 1 in those years
# @Params:
# - var.startyear => In the slider  range (start, end), represents the start value
# - var.endyear => In the slider  range (start, end), represents the end value
# top_albums => For each of the top albums we choose, stores the (Year, Album, Artist) columns in a dataframe

number_one_album <- function(var.startyear, var.endyear){
     # Selects albums, with Ranking = 1, meaning the top album for each year among the years in the desired range (var.startyear, var.endyear)
    top_albums <- select(filter(album_data, Ranking ==1, Year >= var.startyear, Year <= var.endyear), Year, Album, Artist) 
}
```
