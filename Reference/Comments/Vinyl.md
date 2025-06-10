## Vinyl

```r
# Reads in the album data from the album-rankings csv file
# @Params: 
# - data/album-rankings.csv  => File path to the csv storing album data
# album_data => Stores the csv file’s data into a dataframe
album_data <- read.csv("data/albums-rankings.csv")
# Function: Retrieves the top rated vinyls that the user does not own
missing_vinyl <- function(){
    # Select albums, in non-increasing order from (high, low), where the album rating >= 9
    buy_vinyl <- select(filter(album_data[order(-album_data$Rating),], Rating >= 9, Vinyl ==""), Album, Artist, Rating)
}
# Function: Returns the years, sorted from (highest, lowest), based on vinyl count
# - Vinyl Count: Represents the number of vinyls the user owns from that particular year
year_most_vinyl <-function(){
    # For each of the years, filter, such that the user owns vinyls for the albums
    most_vinyl <- select(filter(album_data, Vinyl == "v"), Year)
    # For each year, count how many vinyl albums the user owns
    most_vinyl_count <- filter(most_vinyl) %>% count(Year)
    # Based on how many vinyl albums the user owns for a particular year, return in descending order : (Year, count) => (Highest, lowest)
    most_vinyl_sort <- most_vinyl_count[order(-most_vinyl_count$n),] 
}
```
