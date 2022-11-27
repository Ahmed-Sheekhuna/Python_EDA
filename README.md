# Using python for data exploration and analysis

* For this project i used python for data exploration/analysis/visualisation of movie data.
* The purpose of this project is to provide answers for stake holders looking to get into the film making industry.
* Questions i will be exploring to paint a clearer picture for the stake holders:
1. When is the best time of the year to release a movie to gain maximum profits?
2. Which actors and directors to choose to maximise success of a movie?
3. Does the length of the movie and the rating have any impact on Net Profit, Profit Margins and IMDb ratings?
4. What type of movies are most profitable to produce and how much should you spend?

### Question 4
##### What type of movies are most profitable to produce and how much should you spend?

* For this question i will have to  make use of a budgets dataframe called imdb_budgets_df. My analysis requires that i use the data to calculate the profit and profit margin.

imdb_budgets_df['Profit'] = imdb_budgets_df['Worldwide Gross'] - imdb_budgets_df['Production Budget']

imdb_budgets_df['Profit_Margin'] = (imdb_budgets_df['Worldwide Gross'] - 
                                    imdb_budgets_df['Production Budget'])/imdb_budgets_df['Worldwide Gross']
                                    
* I created two columns named Adjusted_Budget and Adjusted_Profit where we calculate a movie's budget and profit to account for inflation and allow us to perform analysis based on the value of the dollar in the 2020 year to provide concise analysis.
                                    
                                    
