<!-- _sidebar.md -->

# How to Update the Slider Input For Number One Albums Tab

Currently, the slider defaults to years from 1993 - 2024

If you would like to update the range, follow the steps below:

1) Navigate to **app_ui.R** in RStudio, in the same directory you ran the program

2) In the tabPanel named **Number One Albums**, update the **min** and **max** values to reflect your desired range

<!-- Add code snippets below -->
```
tabPanel("Number One Albums", 
         htmlOutput("text3")
         sliderInput("rng", "Choose the Years", value = c(1993, 1998), min = 1990, max = 2020)),
```
a) If done correctly, when you rerun the application and navigate to the **Number One Albums** tab, the min and max range for the slider should be updated.


# How to Update the Default Slider Range
Currently, the range defaults to 1993 - 1998

To modify this range (increase/decrease), follow the steps below:

1) Navigate to **app_ui.R** in RStudio

2) Navigate to the tabPanel labeled **Number One Albums**

3) In the sliderInput for this tabPanel, update the value range from `c(1993, 1998)` to `(c<low>, <high>)`, where low and high represent the years in the range.

```
tabPanel("Number One Albums", 
         htmlOutput("text3")
         sliderInput("rng", "Choose the Years", value = c(1990, 1998), min = 1990, max = 2020)),
```
a) If done correctly, you should see the updated default range, when you rerun the application