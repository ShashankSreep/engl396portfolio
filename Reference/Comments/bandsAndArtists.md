## Bands and Artists

```r
# Reads in the album data from the album-rankings csv file
# @Params: 
# - data/album-rankings.csv  => File path to the csv storing album data
# album_data => Stores the csv file’s data into a dataframe

album_data <- read.csv("data/album-rankings.csv")

# Sorts all of the artists in the album_data by alphabetical order
# This is used to populate the dropdown when selecting the artist
all_bands <- sort(unique(album_data$Artist))

# Function: Based on the artist/band, retrieves all of the albums from that artist including the (Album, Year, Rating) columns
# @Params
# - band.var => Stores the artist/band name that was selected in the dropdown menu
albums_by_bands <- function(band.var){
    band_albums <- select(filter(album_data[order(album_data$Year),], Artist==band.var), Album, Year, Rating)
}

# Function: Based on the artist/band, retrieves all of the albums present in the dataset from that artist, and gets the average rating for those albums
# @Params:
# - band.var => Stores the artist/band name that was selected in the dropdown menu
band_mean_rating <- function(band.var){
    # For each album retrieved, stores the (Album, Year, Rating) columns in a dataframe
    band_albums <- select(filter(album_data[order(album_data$Year),], Artist==band.var), Album, Year, Rating)
     # Gets the average rating among each album in band_albums
    avg_rating <- mean(band_albums$Rating)
    # Prints the Average rating, rounded to 2 decimal places to the console
    print(paste0("Average Rating: ", format(round(avg_rating, 2), nsmall =2)))
}

# Function: Based on the artist/band, retrieves the number of albums present in the dataset by that artist
# @Params
# - band.var => The artist.band name that was selected in the dropdown menu
band_album_count <- function(band.var){
    # For each album retrieved stores (Album, Year, Rating) columns in a dataframe
    band_albums <- select(filter(album_data[order(album_data$Year),], Artist==band.var), Album, Year, Rating)
    # band_count: stores the number of albums in band_albums (the number of albums present in the dataset by the artist)
    band_count <- count(band_albums)
    # Prints the number of albums that are ranked from that artist to the console
    print(paste0("Number of Albums Ranked: ", band_count))
}
```