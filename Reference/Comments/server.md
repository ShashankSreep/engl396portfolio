<!-- _sidebar.md -->

## Server.R

>**Note**: Comments are marked with a # in the code snippets

```r
# When the user interacts with the UI, based on the user’s action, the server will execute the appropriate code in order to reflect the input
server <- function(input, output) {
    # Renders the title My Favorite Albums for the main page
    output$title <- renderUI({
        HTML("<h1>My Favorite Albums</h1><br>")
    })   
    # Renders a vertical line break
    output$text3 <- renderUI({
        HTML("<br><br>")
    })  
    
    # Renders a table showing the number one albums from the years (input$rng[1], input$rng[2])
    # @Params
    # - input$rng[1]: Start year in the slider in the first tab
    # - input$rng[2]: End year in the slider in the first tab
    # Calls the function number_one_album, which will return the number one albums for those years
    output$number_one_table <- renderTable({
        return(number_one_album(input$rng[1], input$rng[2]))
    })
    
    # Renders a vertical line break
    output$text <- renderUI({
        HTML("<br><br>")
    })
    
    # Renders a vertical line break
    output$text2 <- renderUI({
        HTML("<br><br>")
    })
    
    # When user clicks the submit button
    # Renders the albums by the particular band as a table
    # Renders the number of albums ranked in the dataset by that band as a text
    # Renders the mean rating for all albums by that band as a text
    observeEvent(input$action_button,{
         # Call the fucntion albums_by_band to get the all albums from the particular band
         # @Params
         # - input$band_name: The band name that the user selected in the dropdown men
        output$album_table <- renderTable({
            return(albums_by_bands(input$band_name))
        })

        # Call the function band_album_count to get the number of albums that have been ranked from the particular band
        # @Params 
        # input$band_name: Represents the band name the user selected in the dropdown menu
        output$album_count <- renderText({
            return(band_album_count(input$band_name))
        })

        # Call the function band_mean_rating to get the mean rating for all albums that have been ranked from this particular band
        # @Params 
        # input$band_name: Name of the band that the user selected in the dropdown menu
        output$avg_rating <- renderText({
            return(band_mean_rating(input$band_name))
        })  
    })  
    

    # Renders a vertical line break
    output$text4 <- renderUI({
        HTML("<br><br>")
    })
    

    # Renders a vertical line break
    output$text5 <- renderUI({
        HTML("<br><br>")
    })
    

    # Renders a table where each element in the table is an album
    # sorted from highest to lowest based on the album ranking 
    # @Params
    # - input$year: The year that the user selected in the dropdown menu
    observeEvent(input$action_button2,{
        output$year_table <- renderTable({
            return(year_albums(input$year))
        })
    }) 

    # Render the title to represent the top rated vinyls the user does not own
    output$text6 <- renderUI({
        HTML("<h2>Top-rated vinyl that I don't own</h2><br>")
    })

    # Renders a table of all of the top vinyls that the user does not own
    # Calls the function missing_vinyl() 
    output$missing_vinyl_table <- renderTable({
        return(missing_vinyl())
    })

    # Renders a title representing the years the user owns the most vinyl
    output$text7 <- renderUI({
        HTML("<h2>Years for which I own the most vinyl</h2><br>")
    })

    # Renders a table that represents the years which the user owns the most vinyl for
    # Calls the function year_most_vinyl()
    output$most_vinyl_table <- renderTable({
        return(year_most_vinyl())
    })
    
    # Renders a vertical line break
    output$text8 <- renderUI({
        HTML("<br><br>")
    })
    
    # Renders a vertical line break
    output$text9 <- renderUI({
        HTML("<br><br>")
    })


    # When the user selects the two bands they would like to compare, renders a plot
    # that compares the two bands’ album rankings over time based on the user’s album data
    # @Params
    # - input$band_name_1: The first band that the user selected in the dropdown menu
    # - input$band_name_2: The second band that the user selected in the dropdown menu
    # Calls the function band_album_comparison_chart() and renders this plot
    output$compare_bands <- renderPlot({
        return(band_album_comparison_chart(input$band_name_1, input$band_name_2))
    })
}
```r
