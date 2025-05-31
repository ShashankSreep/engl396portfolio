# Interact with the Website
There is a deployed version of **My Favorite Albums**, for users to visit. The website uses sample Album ratings and rankings, to showcase the key features of the application. To view the key features, users can cycle through the various tabs and interact with the sliders and dropdown menus to experiment with various albums, years, and artists. 


# Album Data Structure
All of the data in **My Favorite Albums** is contained in a single CSV file. A CSV (Comma Separated Values) file is a text-based format that stored data in a table-like structure, with each row representing a record entry, and the values within each record, separated by commas. 
Each of the analysis metrics, such as top albums, average ratings, and graphical analysis, process the data from this CSV file. 

Below is a sample structure of the CSV file, the application uses: 

**Year**: Year the album was released

**Ranking**: Users personal ranking for the album

**Album**: Name of the album

**Rating**: A rating from (1 - 10) for the particular album

**Vinyl**: Indicated if a user owns a vinyl for this particular album

**Live**: (Ask Chris)

```
Year, Ranking, Album, Artist, Rating, Vinyl, EP, Live
1993, 1, August and Everything After, Counting Crows, 10, v, ,
1993, 2, Siamese Dream, The Smashing Pumpkins, 9, v, ,
```

In a CSV file, to indicate no content or null content for a particular column, simply leave the column blank.

