## How to Update the Number Of Albums Shown for Top Albums By Year

Currently, the application returns all of the albums ranked from top to bottom for the particular year: 

To place a filter on that range to return the top *n* albums for that particular year, follow the steps below.

1) Navigate to **albums_by_year.R** in RStudio.

You should see a function called **year_albums**.

2) In the **year_list** field, surround the existing code with the `head()` function as shown below:

<!-- Add a Note below -->