# Phase 1 Project Description
PHASE 1 PROJECT
Final Project Submission

    Student name: CYNTHIAH CHELIMO MULWO
    Student pace: FULL TIME
    Scheduled project review date/time:
    Instructor name:
    Blog post URL:


### Business Problem

Microsoft sees all the big companies creating original video content and they want to get in on the fun. They have decided to create a new movie studio, but they don’t know anything about creating movies. You are charged with exploring what types of films are currently doing the best at the box office. You must then translate those findings into actionable insights that the head of Microsoft's new movie studio can use to help decide what type of films to create.

### The Data

In the folder `zippedData` are movie datasets from:

* [Box Office Mojo](https://www.boxofficemojo.com/)
* [IMDB](https://www.imdb.com/)
* [Rotten Tomatoes](https://www.rottentomatoes.com/)
* [TheMovieDB](https://www.themoviedb.org/)
* [The Numbers](https://www.the-numbers.com/)

given the above data, I used some of it for analysis and finally giving my reccomendations to Microsoft.

### Tha data cleaning proccess

some of the data was clean and complette while others had missing values and other charracters .
 
## BOM.MOVIE_GROSS.CSV

This is a dataset containing movie titles, their domestic gross, their foreign gross, the studio and the year as columns
 
 since I wanted to use the foreign gross column , which wasnt written as integer as it had other characters, I had to ensure that it if in a numeric form, I added another column; Box office which was an addition of the domestic gross and foreign gross in each of the rows.
 #### data cleaning
  The data cleaning process included checking for duplicates in the data and checking if any of the rows had missing data, Which I found none of those
 
 #### data visualization
 
 I checked for the most used studio using the code :
 df.studio.value_counts()
 
 and I wanted my audience to visualize that data using a histogram . I therefore made one histogram for that, which showed BV as the most used studio.
 
 I created a bar graph to see the relationship between studios and total film revenues
From that i came to a conclusion that the most used studio, perfomed well in terms of giving a higher revenue than others

## MOVIES.CSV

This dataset contains the genre_id,id ,original_language ,original_title , popularity ,release_date ,title ,vote_average and 	vote_count of the different movies in each row.

#### data cleaning

 The data cleaning process included checking for duplicates and alco checking for the missing values in each column
  and ensuring everything is fixed before its analysis
  
  #### data visualization
  after careful analysis, I declared English as the most used language by far abd to visualize that for my audience, I made a histogram to show the most used languages.
  
  I also plotted a bar graphs to show the avarage votes in movies based on languages and several languages had good perfomance
  
  ## IM.DB
  This dataset is an SQL dataset that contained the following tables :
  [('movie_basics',),
 ('directors',),
 ('known_for',),
 ('movie_akas',),
 ('movie_ratings',),
 ('persons',),
 ('principals',),
 ('writers)
 
 I loaded the movie basics and the movie ratings as I was going to use them for my analysis
 
after loading and cleaning, I went ahead to plot two graphs, a scatter plot and a line plot to see the relationship between the avarage rating and number of votes
I came to a solition that they are related as the most number of votes were at the good rating.
I went ahead and loaded the genrws that were rated at 10 and plotted a graph of it . the documenraries had the best ratings

## MOVIE BUDGETS
The csv file contained : the movie name , production budget,domestic gross and worldwide gross as their columns

I loaded the data .
My data cleaning included : to ensure that the data is workable with by removing all symbols and str

I selected the data , whose worldwide gross was above $100000000 . 
I used the data to check the corelation between production budget and the worldwide gross.
The production budget and the worldwide gross has a very positive correltion: the more you spend on production, the more you get

