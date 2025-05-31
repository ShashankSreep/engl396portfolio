# How to update the rating filter for Top-Rated albums you do not own vinyls for

1) Navigate to **vinyl.R** in RStudio

    a) You should see the function **missing_vinyl** with the **Rating** field set to be **>=9**

2) Update the rating field to your desired range (This means that all entries with no vinyls, and a rating vinyls of `>=<Rating>` will be displayed)

<!-- Show code snippet -->

<!-- Add a Note saying pick an integer value for Rating -->


# How to Update the Number of Years Returned For Most Vinyls Owned By Year

If you would like to limit the number of years returned, say top 10 years for which you own the most viyls from that year, follow the steps below:

1) Navigate to **vinyl.R** in RStudio

    a) You should see the function **year_most_vinyl**

2) Inside the function in most_vinyl_sort, wrap the **head** function around the existing code (Example below)

<!-- Add a note saying replace the '10' with their choice values !-->


- If done correctly, you should see the updated number of years returned when you rerun the application.