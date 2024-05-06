DS 202 Final Project
================

<!-- README.md is generated from README.Rmd. Please edit the README.Rmd file -->
<!--
This repository serves as a starter repo for your final project, and this Rmd is supposed to serve as a starter file for your project report.
&#10;## Part I: Repo Structure {.unnumbered}
&#10;The structure sketched out below is an idea of what your repository might look like. You can use it as a starting base and change according to your needs. But think about the changes that you make!
&#10;    -- code
    |   |   -- any R scripts you need but don't want to include directly in the write-up
    -- data
    |   |   -- csv files (cleaned data)
    -- data-raw
    |   |   -- raw data files 
    |   |   -- data description files, origin
    |   |   -- Codebook
    -- final-project.Rmd
    -- images  # only images that are not created by the Rmd
    -- LICENSE
    -- README.md
    -- README.Rmd
    -- README_files # folder with files created during the knitting process
&#10;## Part II: Project report {.unnumbered}
&#10;
-->

# Sleep Health and Lifestyle

Authors: Gabriel Getzinger, Michael Friedman

## Abstract (TL;DR)

In this project we will perform exploratory data analysis on a Kaggle
sourced
[dataset](https://www.kaggle.com/datasets/uom190346a/sleep-health-and-lifestyle-dataset/data?select=Sleep_health_and_lifestyle_dataset.csv)
with information regarding sleep quality along with various other
biometric factors. We will attempt to uncover any underlying patterns in
the data that may be helpful to know if one unfortunately suffers from a
sleep disorder. As the project progresses, new datasets may be
introduced as more questions arise.

<!--
&#10;-   what is the project about?
-   what is the motivation for doing it?
-   what data is your work based on? and where does it come from? = what are your main findings? (one sentence each)
&#10;-->

# Intro/Background/Motivation

According to the [Mayo
Clinic](https://www.mayoclinic.org/diseases-conditions/sleep-disorders/symptoms-causes/syc-20354018):

*“A sleep disorder can affect your overall health, safety and quality of
life. Sleep deprivation can affect your ability to drive safely and
increase your risk of other health problems.”*

<!--
&#10;At the end of the Intro, write a sentence describing what each of the (result) sections is about, e.g. in section [Results 1] we show the relationship between XXX and YYY,  section [Results 2] also considers the effect of variable ZZZ. ...
Finally we conclude with a quick summary of our findings and potential follow-up work in section [Conclusions].
&#10;Somewhere at the beginning of your project, include a code chunk that includes all of the R packages you are using throughout. In this document, the setup code chunk is called `setup` (see line 8) Also make sure to set defaults for the code chunks - like should they be visible? (probably not: echo=FALSE). Do you want to automatically include warnings? (probably yes, for creating the Rmd, to make sure that all warnings are accounted for)
&#10;-->

# Quick Data Summary

    ## function (x, df1, df2, ncp, log = FALSE)

| Person.ID | Gender | Age | Occupation           | Sleep.Duration | Quality.of.Sleep | Physical.Activity.Level | Stress.Level | BMI.Category | Blood.Pressure | Heart.Rate | Daily.Steps | Sleep.Disorder |
|----------:|:-------|----:|:---------------------|---------------:|-----------------:|------------------------:|-------------:|:-------------|:---------------|-----------:|------------:|:---------------|
|         1 | Male   |  27 | Software Engineer    |            6.1 |                6 |                      42 |            6 | Overweight   | 126/83         |         77 |        4200 | None           |
|         2 | Male   |  28 | Doctor               |            6.2 |                6 |                      60 |            8 | Normal       | 125/80         |         75 |       10000 | None           |
|         3 | Male   |  28 | Doctor               |            6.2 |                6 |                      60 |            8 | Normal       | 125/80         |         75 |       10000 | None           |
|         4 | Male   |  28 | Sales Representative |            5.9 |                4 |                      30 |            8 | Obese        | 140/90         |         85 |        3000 | Sleep Apnea    |
|         5 | Male   |  28 | Sales Representative |            5.9 |                4 |                      30 |            8 | Obese        | 140/90         |         85 |        3000 | Sleep Apnea    |

Upon our initial first glance at the dataset, we found one item we could
clean right away. The redundant category shown can be grouped together
with the other one with the similar name:

``` r
df[["BMI.Category"]] %>% unique()
```

    ## [1] "Overweight"    "Normal"        "Obese"         "Normal Weight"

``` r
df$BMI.Category[df$BMI.Category == "Normal Weight"] <- "Normal"
df[["BMI.Category"]] %>% unique()
```

    ## [1] "Overweight" "Normal"     "Obese"

An initial view of all subjects by…  

Weight category:  
![](README_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->  
Gender:  
![](README_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->  

Self-reported sleep quality grouped by occupation:  
![](README_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->  
Note that the nurses responses are bifurcated, likely due to a 12-hour
shift schedule. <!--

What are the variables that you will be using in the main part of the report? What are their ranges? You could include a table with variable names, a short explanation, and (very broad) summary statistics.

-->

# Results

<!--
Correlations between:
&#10;disorder and: stress level, gender, occupation
&#10;sleep quality and: heart rate, occupation
&#10;What occupation has the worst sleep quality? highest incidence of disorder?
&#10;which disorder is most prevalent among highest stressed?
-->
<!--
&#10;Each line of exploration is supposed to be featured in one of the Results sections. Make sure to change to more interesting section headers!
&#10;## Results 1
&#10;In your write-up, make sure to refer to all of the figures you create. You can include a hyperlink to the [scatterplot](#fig:scatterplot) by using the name of the code chunk (make sure, to give each code chunk a different name). In your markdown document you can create this link either by calling the function `chunkref` with the name of the code chunk in quotes, i.e. `` r chunkref("scatterplot") `` or by using the markdown expression `[scatterplot](#fig:scatterplot)`. Similarly, we can refer to the [2nd scatterplot](#fig:2nd scatterplot). Note that the figure captions appear above the figures - this saves us from having to scroll up after following the link.
&#10;<p><small><strong><a name='fig:scatterplot'>scatterplot</a></strong>: This is the figure caption. Make sure to use the description we practised in the homework: first sentence describes structure of the plot, second sentence describes main finding, third sentence describes outliers/follow-up.</small></p>![This is the figure caption. Make sure to use the description we practised in the homework: first sentence describes structure of the plot, second sentence describes main finding, third sentence describes outliers/follow-up.](README_files/figure-gfm/scatterplot-1.png)
&#10;<p><small><strong><a name='fig:2nd scatterplot'>2nd scatterplot</a></strong>: This is the figure caption. Make sure to use the description we practised in the homework: first sentence describes structure of the plot, second sentence describes main finding, third sentence describes outliers/follow-up.</small></p>![This is the figure caption. Make sure to use the description we practised in the homework: first sentence describes structure of the plot, second sentence describes main finding, third sentence describes outliers/follow-up.](README_files/figure-gfm/2nd scatterplot-1.png)
&#10;Additionally, you can also refer to different sections in your writeup by using anchors (links) to section headers. Here, we are referring to subsection [Results 3]. The code for that is `[Results 3]`.
&#10;## Results 2
&#10;## Results 3
&#10;...
&#10;# Conclusions
&#10;Give a quick summary of your work. Here is the place to be a bit critical and discuss potential limitations. Add a sentence on what else you would have liked to include in your data exploration if you had more time or more members in your team. 
&#10;## Data source {.unnumbered}
&#10;Where does the data come from, who owns the data? Where are all the scripts that you need to clean the data?
&#10;-->

## References

[Link to Kaggle
dataset](https://www.kaggle.com/datasets/uom190346a/sleep-health-and-lifestyle-dataset/data?select=Sleep_health_and_lifestyle_dataset.csv)
