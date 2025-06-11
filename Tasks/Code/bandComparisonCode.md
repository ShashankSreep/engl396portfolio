<!-- _sidebar.md -->

# How to Add More Bands To Compare For Band Comparison

Note: To complete this, multiple files will need to be changed (We will go file by file):

**compare_bands.R**
1) Navigate to **compare_bands.R** in RStudio

You should see the function **band_album_comparison_chart** taking the parameters
`var.artist1, var.artist2`

2) Modify the function, so that it takes 3 parameters as shown below:

```
band_album_comparison_chart <- function(var.artist1, var.artist2, var.artist3)
```

3) Inside the function, you will see band1_albums and band2_albums as parameters: Add band3_albums, following the exact same logic as the previous assignments, except modify `Artist==var.artist3`

```
band3_albums <- select(filter(album_data[order(album_data$Year),], Artist==var.artist3), Artist, Album, Year, Rating)

```

4) Add a **geom_point** field for band3_albums as shown below:

```
geom_line(data = band3_albums, aes(x = Year, y = Rating), color = 'orange')
```

Note: For the color, you can choose anything, so long as it is a valid color in R and different from the other two **geom_line** objects

5) Add a **geom_point** filed for band3_albums as shown below:

```
geom_point(data = band3_albums, aes(x = Year, y = Rating))
```

6) In the **ggtitle** object, update the title to reflect the new album

```
ggtitle(paste0("Album Ratings for ", band_1)) 
```
<!-- Update the code to reflect this when you get on your machine -->


**app_ui.R**
1) Navigate to the tabPanel object named **Band Comparison**

2) Add a new selectInput element for selecting the third band/artists as shown below:
```
selectInput("band_name_3", "Third band or artist:", all_bands),
```
**app_server.R**
1) Navigate to the output element, which returns the band_album_comparison_chart

2) Add a field input$band_name_3

```
output$compare_bands <- renderPlot({
    return(band_album_comparison_chart(input$band_name_1, input$band_name_2, input$band_name_3))
})
```

Run **app.R** to run the application locally, and you should see the changes reflected

