# COMMENTS

Below are code comments for each of the important functions, methods and logic throughout **My Favorite Albums**.

---

## Number One Albums

```r
album_data <- read.csv("data/album-rankings.csv")
number_one_album <- function(var.startyear, var.endyear){
    top_albums <- select(filter(album_data, Ranking ==1, Year >= var.startyear, Year <= var.endyear), Year, Album, Artist) 
}
```


## Bands and Artists

```r
album_data <- read.csv("data/album-rankings.csv")

all_bands <- sort(unique(album_data$Artist))

albums_by_bands <- function(band.var){
    band_albums <- select(filter(album_data[order(album_data$Year),], Artist==band.var), Album, Year, Rating)
}

band_mean_rating <- function(band.var){
    band_albums <- select(filter(album_data[order(album_data$Year),], Artist==band.var), Album, Year, Rating)
    avg_rating <- mean(band_albums$Rating)
    print(paste0("Average Rating: ", format(round(avg_rating, 2), nsmall =2)))
}

band_album_count <- function(band.var){
    band_albums <- select(filter(album_data[order(album_data$Year),], Artist==band.var), Album, Year, Rating)
    band_count <- count(band_albums)
    print(paste0("Number of Albums Ranked: ", band_count))
}
```

---

## Albums By Year

```r
album_data <- read.csv("data/album-rankings.csv")
all_years <- sort(unique(album_data$Year))
year_albums <- function(year.var){
    year_list <- select(filter(album_data[order(album_data$Ranking),], Year == year.var), Ranking, Album, Artist)
}
```

---

## Vinyl

```r
album_data <- read.csv("data/albums-rankings.csv")
missing_vinyl <- function(){
    buy_vinyl <- select(filter(album_data[order(-album_data$Rating),], Rating >= 9, Vinyl ==""), Album, Artist, Rating)
}
year_most_vinyl <-function(){
    most_vinyl <- select(filter(album_data, Vinyl == "v"), Year)
    most_vinyl_count <- filter(most_vinyl) %>% count(Year)
    most_vinyl_sort <- most_vinyl_count[order(-most_vinyl_count$n),] 
}
```

---

## Band Comparison

```r
band_album_comparison_chart <- function(var.artist1, var.artist2){
    band1_albums <- select(filter(album_data[order(album_data$Year),], Artist==var.artist1), Artist, Album, Year, Rating)
    band2_albums <- select(filter(album_data[order(album_data$Year),], Artist==var.artist2), Artist, Album, Year, Rating) 
    
    ggplot() +
        geom_line(data = band1_albums, aes(x = Year, y = Rating), color = "red") +
        geom_line(data = band2_albums, aes(x = Year, y = Rating), color = "blue") +
        geom_point(data = band1_albums, aes(x = Year, y = Rating)) +
        geom_point(data = band2_albums, aes(x = Year, y = Rating)) +
        xlab("Year")+
        ylab("Rating")+
        theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust=1))+
        ggtitle(paste0("Album Ratings for " , band1_albums$Artist, "(Red) and ", band2_albums$Artist, "(Blue)"))+ 
        scale_x_continuous(breaks=seq(1993,2024,1))+ 
        scale_y_continuous(breaks=seq(0,10,1))+
        expand_limits(x=c(1993,2024), y=c(0,10))
}
```

---

## App UI.R

```r
album_data <- read.csv("data/album-rankings.csv")
all_bands <- sort(unique(album_data$Artist))
all_years <- sort(unique(album_data$Year))
ui <- fluidPage(
        mainPanel(htmlOutput("title"),
            tabsetPanel(
                id = "tabset",
                tabPanel("Number One Albums",
                                 htmlOutput("text3"),
                                 sliderInput("rng", "Choose the Years", value = c(1993, 1998), min = 1993, max = 2024),
                                 tableOutput("number_one_table")),
                tabPanel("Bands and Artists",
                                 htmlOutput("text"),
                                 selectInput("band_name", "Choose a band or artist:", all_bands),
                                 actionButton("action_button", label = "Submit"),
                                 htmlOutput("text2"),
                                 tableOutput("album_table"),  
                                 textOutput("album_count"), 
                                 textOutput("avg_rating")),
                tabPanel("Top Albums by Year",
                                 htmlOutput("text4"),
                                 selectInput("year", "Choose a year:", all_years),
                                 actionButton("action_button2", label = "Submit"),
                                 htmlOutput("text5"),
                                 tableOutput("year_table")),
                tabPanel("Vinyl",
                                 htmlOutput("text6"),
                                 tableOutput("missing_vinyl_table"), 
                                 htmlOutput("text7"),
                                 tableOutput("most_vinyl_table")),
                tabPanel("Band Comparison",
                                 htmlOutput("text8"),
                                 selectInput("band_name_1", "First band or artist:", all_bands),
                                 selectInput("band_name_2", "Second band or artist:", all_bands),
                                 htmlOutput("text9"),
                                 plotOutput("compare_bands")) 
            )
        )
)
```

---

## Server.R

```r
server <- function(input, output) {
    output$title <- renderUI({
        HTML("<h1>My Favorite Albums</h1><br>")
    })   
    
    output$text3 <- renderUI({
        HTML("<br><br>")
    })  
    
    output$number_one_table <- renderTable({
        return(number_one_album(input$rng[1], input$rng[2]))
    })
    
    output$text <- renderUI({
        HTML("<br><br>")
    })
    
    output$text2 <- renderUI({
        HTML("<br><br>")
    })
    
    observeEvent(input$action_button,{
        output$album_table <- renderTable({
            return(albums_by_bands(input$band_name))
        })
        output$album_count <- renderText({
            return(band_album_count(input$band_name))
        })  
        output$avg_rating <- renderText({
            return(band_mean_rating(input$band_name))
        })  
    })  
    
    output$text4 <- renderUI({
        HTML("<br><br>")
    })
    
    output$text5 <- renderUI({
        HTML("<br><br>")
    })
    
    observeEvent(input$action_button2,{
        output$year_table <- renderTable({
            return(year_albums(input$year))
        })
    }) 

    output$text6 <- renderUI({
        HTML('<span style="color: green;">Reads in the album data from the album-rankings csv file</span><br>
        <code>album_data &lt;- read.csv("data/album-rankings.csv")</code><br>
        <span style="color: green;">Table that displays the top rated vinyls user does not own</span>')
    })

    output$missing_vinyl_table <- renderTable({
        return(missing_vinyl())
    })

    output$text7 <- renderUI({
        HTML("<h2>Years for which I own the most vinyl</h2><br>")
    })

    output$most_vinyl_table <- renderTable({
        return(year_most_vinyl())
    })
    
    output$text8 <- renderUI({
        HTML("<br><br>")
    })
    
    output$text9 <- renderUI({
        HTML("<br><br>")
    })

    output$compare_bands <- renderPlot({
        return(band_album_comparison_chart(input$band_name_1, input$band_name_2))
    })
}
```
