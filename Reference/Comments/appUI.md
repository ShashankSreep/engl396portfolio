## App UI.R

>**Note**: Comments are marked with a # in the code snippets

```r
# Reads in the album data from the album-rankings csv file
# @Params: 
# - data/album-rankings.csv  => File path to the csv storing album data
# album_data => Stores the csv file’s data into a dataframe
album_data <- read.csv("data/album-rankings.csv")

# Sorts all of the artists in the album_data by alphabetical order
# This is used to populate the dropdown when selecting the artist
all_bands <- sort(unique(album_data$Artist))

# Sorts all of the years in the albums dataset in numerical order (oldest, recent)
# This is used to populate the dropdown when selecting the year
all_years <- sort(unique(album_data$Year))

# Represents the UI for the application
# Tabset panel contains tabPanel, where each tabPanel represents a specific tab in the application
# eg: Number One Albums and Bands And Artists
ui <- fluidPage(
        mainPanel(htmlOutput("title"),
            tabsetPanel(
                id = "tabset",

                # Tab that represents the Number One Albums page in the website
                # - Contains a sliderInput, which is the slider that the user can interact with in order to change the years range, and get the number one albums for those years
                tabPanel("Number One Albums",
                                 htmlOutput("text3"),
                                 # This slider input currently takes an input from 1993 - 2024
                                 # - Initially renders from (1993 - 1998) upon opening the application
                                 sliderInput("rng", "Choose the Years", value = c(1993, 1998), min = 1993, max = 2024),
                                 tableOutput("number_one_table")), # Displays top albums for the years in slider range
                
                # Tab that represents the Band and Artists page in the website
                tabPanel("Bands and Artists",
                                 htmlOutput("text"),
                                 # This is the dropdown menu to select the band/artist
                                 selectInput("band_name", "Choose a band or artist:", all_bands),
                                  # This represents the submit button, which when clicked will display
	                              # information about the albums ranked for that artist/band
                                 actionButton("action_button", label = "Submit"),
                                 htmlOutput("text2"),
                                 # Displays (Album, Year, Rating) for each album ranked from the artist/band in a table
                                 tableOutput("album_table"),
                                 # Displays the number of albums ranked by the artist/band
                                 textOutput("album_count"), 
                                 textOutput("avg_rating")), # Displays average rating for albums by this band/artist
                # Tab that represents the Top Albums By Year Page
                tabPanel("Top Albums by Year",
                                 htmlOutput("text4"),
                                 # This is the dropdown menu to select a year to get the ranking of top albums
                                 selectInput("year", "Choose a year:", all_years),
                                 # Represents the submit button, which when clicked will render the top album ranking 
                                 # for the particular year in increasing order (highest, lowest)
                                 actionButton("action_button2", label = "Submit"),
                                 htmlOutput("text5"),
                                 tableOutput("year_table")), # Displays the albums and artist ranked from (high, low)

                # Tab that represents the Vinyl Tab in the website
                tabPanel("Vinyl",
                                 htmlOutput("text6"),
                                 # Table that displays the top rated vinyls user does not own
                                 tableOutput("missing_vinyl_table"), 
                                 htmlOutput("text7"),
                                 # Table that displays the years for which the user owns the most vinyls
                                 tableOutput("most_vinyl_table")),
                # Tab that represents the Band Comparison Tab in the website
                tabPanel("Band Comparison",
                                 htmlOutput("text8"),
                                 # This is the dropdown where the user can select the first artist/band to compare
                                 selectInput("band_name_1", "First band or artist:", all_bands),
                                 # This is the dropdown where the user can select the second artist/band to compare
                                 selectInput("band_name_2", "Second band or artist:", all_bands),
                                 htmlOutput("text9"),
                                 # Plots the graph comparing the different bands’ album ratings
                                 plotOutput("compare_bands")) 
            )
        )
)
```