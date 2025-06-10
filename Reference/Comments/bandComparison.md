## Band Comparison

```r
# Function: Plots and compares any 2 bands/artists and their album ratings over time
# - @Params
# - var.artist1: Represents the first artist selected in the dropdown menu
# - var.artist2: Represents the second artist selected in the dropdown menu
# For each of the bands/artists selected, the plot displays the ratings of their albums ranked over time
band_album_comparison_chart <- function(var.artist1, var.artist2){
    # Retrieve all the ranked albums by the band/artist corresponding to var.artist1
    # store the columns (Artist, Album, Year, Rating) for each that successfully passes the filter into the dataframe band1_albums

    band1_albums <- select(filter(album_data[order(album_data$Year),], Artist==var.artist1), Artist, Album, Year, Rating)

    # Retrieve all the ranked albums by the band/artist corresponding to var.artist2
    # store the columns (Artist, Album, Year, Rating) for each that successfully passes the filter into the dataframe band2_albums

    band2_albums <- select(filter(album_data[order(album_data$Year),], Artist==var.artist2), Artist, Album, Year, Rating) 
    
    # Plots the points that represent the rating for the albums by each artist (band1, band2)
    # Draw a line connecting these points
    # red: band_1
    # blue: band_2
    ggplot() +
        geom_line(data = band1_albums, aes(x = Year, y = Rating), color = "red") +
        geom_line(data = band2_albums, aes(x = Year, y = Rating), color = "blue") +
        geom_point(data = band1_albums, aes(x = Year, y = Rating)) +
        geom_point(data = band2_albums, aes(x = Year, y = Rating)) +
        xlab("Year")+ # Label for the X-Axis in the plot
        ylab("Rating")+ # Label for the Y-Axis in the plot
        # Adjusts the layout appearance, title, and x/y axis ticks for the graph
        theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust=1))+
        # Represents the title for the graph, where the first band/artist is in red and the second band/artist is in blue
        ggtitle(paste0("Album Ratings for " , band1_albums$Artist, "(Red) and ", band2_albums$Artist, "(Blue)"))+ 
        # Represents the x-axis ticks (1993 - 2024), in increments of 1
        scale_x_continuous(breaks=seq(1993,2024,1))+ 
        # Represents the y-axis ticks (0, 10), in increments of 1
        scale_y_continuous(breaks=seq(0,10,1))+
        expand_limits(x=c(1993,2024), y=c(0,10))
}
```