# Phase 1 Project Description

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


some of the data was clean and complette while others had missing values and other charracters .
### Importing the following libraries is important as they will be required in our data cleaning, data analysis and data visualization codes 
import pandas as pd
import sqlite
import numpy as np
import csv
import matplotlib.pyplot as plt 
% matplotlib inline
 
## BOM.MOVIE_GROSS.CSV

This is a dataset containing movie titles, their domestic gross, their foreign gross, the studio and the year as columns
 
 ##### filter the dataset and base our analysis on the data with a domestic gross of above $100000000
 df = df[df['domestic_gross'] > 100000000]
 df
 
##### since foreign gross is type object, we turn it to float and remove any letters or characters that might be present
df['foreign_gross'].replace('\W', '', regex=True, inplace= True)
df.foreign_gross = df.foreign_gross.astype(float)

##### We should create another column;box office which is a sum of domestic gross and foreign gross in every row

df['box_office'] =( df.domestic_gross) + (df.foreign_gross)
df 

### data cleaning
##### checking if there are any duplicates
df.duplicated().value_counts()

##### checking for null values.NaNs return true while valid data returns false
df.isna()
##### the sum of null values
df.isna().sum
#### fill the missing data from domestic gross with its median
median_domestic_gross = df['domestic_gross'].median()
df['domestic_gross'] = df['domestic_gross'].fillna(median_domestic_gross)

### data visualization
##### check for the most used studios
df.studio.value_counts()

##### create a histogram to compare the most used studio visually

fig, ax = plt.subplots(figsize = (20,8))
ax.hist(df.studio, bins = 80)
ax.set_xlabel('Names of studios')
ax.set_ylabel('Number of times the studios have been used.')
ax.set_title('Studio counts');



##### lets create a bar graph to see the relationship between studios and total film revenues
fig, ax = plt.subplots(figsize=(15,6))
plt.bar( x= df.studio, height= df.box_office)
plt.xlabel('Name of studios')
plt.ylabel('box office in millions')
plt.title('Relationship between Studios and total revenue from films')
plt.show()

## MOVIES.CSV

This dataset contains the genre_id,id ,original_language ,original_title , popularity ,release_date ,title ,vote_average and 	vote_count of the different movies in each row.

#### data cleaning

##### The data cleaning process included checking for duplicates and alco checking for the missing values in each column
  ##### and ensuring everything is fixed before its analysis
 

  ##### check for duplicate
  movies_df.duplicated().value_counts()
  
  #### data visualization
  after careful analysis, I declared English as the most used language by far abd to visualize that for my audience, I made a histogram to show the most used languages.
  ##### check for the most used languages
  movies_df.original_language.value_counts().head(15)
  
 ##### lets plot a histogram for the most used language
fig, ax = plt.subplots(figsize = (20,6))
ax.hist(movies_df.original_language, bins = 80)
ax.set_xlabel('languages')
ax.set_ylabel('count')
ax.set_title('most used languages');

##### lets plot a bargraph showing the avarage votes based on languages

fig, ax = plt.subplots(figsize=(20,8))
plt.bar( x= movies_df.original_language, height=movies_df.vote_average)
plt.xlabel('original languages')
plt.ylabel('vote average')
plt.title('average votes on different movie based on their languages')
plt.show()

  ## IM.DB
  
  ##### executing the query
cur.execute("""
SELECT name
FROM sqlite_master 
WHERE type = 'table';

""")
##### fetching the results in tables
table_names = cur.fetchall()
table_names
  This dataset is an SQL dataset that contained the following tables :
  [('movie_basics',),
 ('directors',),
 ('known_for',),
 ('movie_akas',),
 ('movie_ratings',),
 ('persons',),
 ('principals',),
 ('writers)
 

#### to check the higher rated movies and their genres
pd.DataFrame(
data=cur.execute("""SELECT original_title,genres,averagerating
FROM movie_basics
JOIN movie_ratings
ON movie_basics.movie_id = movie_ratings.movie_id
 WHERE averagerating == 10
 ORDER BY averagerating DESC
 ;""").fetchall(),
columns=[x[0] for x in cur.description]

#### lets plot two graphs, a scatter plot and a line plot to see the relationship between the avarage rating and number of votes

import pandas as pd
import matplotlib.pyplot as plt  
import seaborn as sns 
movie_rate_and_votes.columns
plt.figure(figsize=(10,6))
sns.regplot(x=movie_rate_and_votes['averagerating'] , y=movie_rate_and_votes['numvotes'])

movie_rate_and_votes.columns
plt.figure(figsize=(10,6))
sns.lineplot(x=movie_rate_and_votes['averagerating'] , y=movie_rate_and_votes['numvotes'])

##### we loaded the most rated movie genres and plotted graph of it
g="""SELECT original_title,genres,averagerating
FROM movie_basics
JOIN movie_ratings
ON movie_basics.movie_id = movie_ratings.movie_id
 WHERE averagerating == 10
 ORDER BY averagerating DESC"""
movie_rates=pd.read_sql(g,conn)

movie_rates.columns
plt.figure(figsize=(10,6))
sns.barplot(x=movie_rates['genres'] , y=movie_rates['averagerating'])

#### closing the connection
conn.close


## MOVIE BUDGETS
The csv file contained : the movie name , production budget,domestic gross and worldwide gross as their columns

### to ensure that the data is workablewith by removing all symbols and str

movie_budgets['worldwide_gross'] = movie_budgets['worldwide_gross'].str.replace('[$,]','')

movie_budgets['worldwide_gross'] = movie_budgets['worldwide_gross'].astype(float)

movie_budgets['production_budget'] = movie_budgets['production_budget'].str.replace('[$,]','')

movie_budgets['production_budget'] = movie_budgets['production_budget'].astype(float)
movie_budgets


### lets select the data whose worldwode gross is above 100000000 to work with
movie_budgets = movie_budgets[movie_budgets['worldwide_gross'] > 100000000]
movie_budgets.head(10)


### lets check the correlation between production budget and worldwide gross

correlation = movie_budgets.corr()
correlation. style. background_gradient (cmap = 'BrBG')

### lets plot a graph to show us the correlation

sns. heatmap (correlation, annot=True);


