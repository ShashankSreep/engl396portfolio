## Albums By Year

>**Note**: Comments are marked with a # in the code snippets
```r
# Reads in the album data from the album-rankings csv file
# @Params: 
# - data/album-rankings.csv  => File path to the csv storing album data
# album_data => Stores the csv file’s data into a dataframe
album_data <- read.csv("data/album-rankings.csv")

# Sorts all of the years in the albums dataset in numerical order (oldest, recent)
# This is used to populate the dropdown when selecting the year in order to view the top albums ranked for that year
all_years <- sort(unique(album_data$Year))

# Function: Lists the top albums for the given year sorted by ranking (highest, lowest) by rating
# @Params:
# - year.var => Represents the year that was chosen in the dropdown menu
# - Filters the album_data to get the albums specifically for this year
year_albums <- function(year.var){
    # Selects the albums in order by the ranking where the year = year.var (the year selected in the dropdown) and stores the (Ranking, Album, Artist) columns in a dataframe
    year_list <- select(filter(album_data[order(album_data$Ranking),], Year == year.var), Ranking, Album, Artist)
}
```