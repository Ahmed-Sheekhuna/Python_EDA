# Using python for data exploration and analysis

* For this project i used python,s pandas, numpy, seaborn, matplotlip and datetime libraries for data exploration/analysis/visualisation of movie data.
* The purpose of this project is to provide answers for stake holders looking to get into the film making industry.
* Questions i will be exploring to paint a clearer picture for the stake holders:
1. When is the best time of the year to release a movie to gain maximum profits?
2. Which actors and directors to choose to maximise success of a movie?
3. Does the length of the movie and the rating have any impact on Net Profit, Profit Margins and IMDb ratings?
4. What type of movies are most profitable to produce and how much should you spend?

### Question 1
#### When is the best time of the year to release a movie to gain maximum profits?

* To answer this question i begin by converting the dates from the imdb_budgets_df dataframe to a datetime object. I then perform a count by month to calculate the number of movies released within each month of our dataset.
* When grouping the data by month, I can select the Net Profit and Profit Margin columns so that we can see which months have the most finacial success. I visualised this data using the bar chart below to show the financialy performance of movies released per month.

![MarginByMonth](https://user-images.githubusercontent.com/33176824/204342548-63eaa39e-8609-4a62-a841-93abc9894e2a.png)

* I then plot the net profit by month for a few genres, we can see that there is a general trend amongst these genres for profit generated in each month.

![ProfitbyMonthbyGenre](https://user-images.githubusercontent.com/33176824/204342662-32db3c1c-548c-404a-9685-1577bbf6cb1b.png)



### Question 2
#### Which actors and directors to choose to maximise success of a movie?
* In this section I take a look at the average net profit across all movies. From there we want to determine which actors and directors consistently appear in movies where the net profit substantially exceeds the average. We will represent this in a field called Value Above Replacement(VAR). To further simplify this concept; if across all movies the average net profit is 100 dollars and the average net profit of movies from 'Actor: X' is 200 dollars he/she would have a VAR of 2. This number represents X times over the average. To eliminate outliers we will look at actors who appear in 10 or more movies and directors who work in 5 or more.
* We'll use the actors_df dataframe, adjust for inflation, and calculate profit as we did in Question 1. Then filter by actors who have starred in 10 or more movies.

actor_counts = actors_df['value'].value_counts()
actor_list = actor_counts[actor_counts >= 10].index.tolist()
actors_df = actors_df[actors_df['value'].isin(actor_list)]

* To calculate VAR:

actor_total = actors_df.groupby(['value'],  as_index=False)['Net Profit'].mean().sort_values(by='Net Profit', ascending=False)
actor_total['VAR'] = (actor_total['Net Profit']/actor_total['Net Profit'].mean())
We follow the same process with directors, except we filter by using 5 or more movies instead of 10.

![VARActor](https://user-images.githubusercontent.com/33176824/204340039-cf84feaf-507d-4a10-b67c-d83f6e5700c6.png)

![VARDirector](https://user-images.githubusercontent.com/33176824/204340023-aeba34bd-04f6-40db-bbfe-20bf524a990b.png)



### Question 3
#### Does the age rating of a movie have any impact on Net Profit margins?
* For this question i looked at the 4 ratings: G, PG, PG-13, and R. I then performed a count on the ratings to see how many movies there are in each category. From this point i can now examine the net profit of each genre and profit margins foreach rating to see which ones have most success. This will let stake holders make decisons on what ratings to choose for each genre to generate maximum profits. 
* To visualise the data i created a pivot table so that we can see the net profits of each rating in each genre.
![pivot](https://user-images.githubusercontent.com/33176824/204331446-2c92d0bd-bec2-41cd-a9e0-c454a73ae6ae.png)

### Question 4
##### What type of movies are most profitable to produce and how much should you spend?

* For this question i will have to  make use of a budgets dataframe called imdb_budgets_df. My analysis requires that i use the data to calculate the profit and profit margin.

imdb_budgets_df['Profit'] = imdb_budgets_df['Worldwide Gross'] - imdb_budgets_df['Production Budget']

imdb_budgets_df['Profit_Margin'] = (imdb_budgets_df['Worldwide Gross'] - 
                                    imdb_budgets_df['Production Budget'])/imdb_budgets_df['Worldwide Gross']
                                    
* I created two columns named Adjusted_Budget and Adjusted_Profit where we calculate a movie's budget and profit to account for inflation and allow us to perform analysis based on the value of the dollar in the 2020 year to provide concise analysis.
* To examine the correlation of the two columns i produced the scatter graph below.                                    
                                    
![scatter](https://user-images.githubusercontent.com/33176824/204325832-57e20328-6163-4212-a8a9-80183501f5ee.JPG)

* To explore the data further, i looked at the top 25 movies profits vs budgets and created a bar chart to provide detailed visalisation to viewers.
![gr](https://user-images.githubusercontent.com/33176824/204327992-0ba5ebde-29e0-4c48-9783-28180be79ab1.png)
