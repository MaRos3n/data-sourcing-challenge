# data-sourcing-challenge
Module 6 Challenge

# Challenge README

## Instructions

This Challenge has three parts, and must be completed in order:

### Part 1: Access the New York Times API

- The base URL is included in the starter code, along with the search string and query dates. Consult the [New York Times Article Search API documentation](https://developer.nytimes.com/docs/articlesearch-product/1/overview) to help you build your query_url using these variables.

- Create an empty list called `reviews_list` to store the reviews you retrieve from the API.

- Loop through 20 pages (starting from page 0) to retrieve 200 reviews.

- Write a try-except clause to handle exceptions and print appropriate messages.

- Preview the first five results in JSON format.

- Convert `reviews_list` to a Pandas DataFrame and perform data cleaning.

- Extract the movie title from the "headline.main" column and save it to a new column "title". To do this, you will use the Pandas apply() method and the following lambda function:

```
    lambda st: st[st.find("\u2018")+1:st.find("\u2019 Review")]
```

- This code takes the string in the cell and extracts the characters between the unicode quotation marks, as long as a space and the word "Review" follows the closing quotation mark.

### Part 2: Access The Movie Database API

- Consult the [Search & Query for Details documentation](https://developers.themoviedb.org/3/search/search-movies) to build your query URLs.

    - The search query is used to find the movie ID from the search by title. Most of this query is included in your starter code, as follows, but you will need to include the movie title in the query.

    ```
    # Prepare The Movie Database query
        url = "https://api.themoviedb.org/3/search/movie?query="
        tmdb_key_string = "&api_key=" + tmdb_api_key
    ``` 

- You will use the titles list created in Part 1 to perform your queries with The Movie Database.

- Create an empty list called `tmdb_movies_list` to store the results from your API requests.

- Create a variable called `request_counter` and initialize it with the value of `1`.

- This counter should do the following:

    - Increment by one every time you iterate through the titles list.
    - Use time.sleep(1) when it reaches a multiple of 50.
    - Print a message to indicate that the application is sleeping.

- Loop through the titles list created from the movie reviews DataFrame, and perform the following actions:

    - Perform the actions outlined in Step 2.

    - Perform a GET request that sends the title to The Movie Database search and retrieves the JSON results.

    - Use a try clause that performs the following actions:

        - Collect the movie ID from the first result.

        - Make a GET request using the movie query (starting with https://api.themoviedb.org/3/movie/) and movie ID to retrieve the full movie details in JSON format.

        - Extract the genre names from the results into a list called genres.

        - Extract the spoken_languages' English name from the results into a list called spoken_languages.

        - Extract the production_countries' name from the results into a list called production_countries.

        - Create a dictionary with the following results: title, original_title, budget, original_language, homepage, overview, popularity, runtime, revenue, release_date, vote_average, vote_count, as well as the genres, spoken_languages, and production_countries lists you just created.

        - Append this dictionary to tmdb_movies_list.

        - Print out the name of the movie and a message to indicate that the title was found.

    - Use the except clause to print out a statement if a movie is not found.

- Preview the first five results in JSON format using json.dumps with the argument indent=4 to format the data.

- Convert the results to a DataFrame called tmdb_df with pd.DataFrame(). You don't need to use json_normalize() this time because we don't have nested objects.

### Part 3: Merge and Clean the Data for Export

- Merge the New York Times reviews and TMDB DataFrames on the title column.

- Clean the data and fix columns containing lists.

- Delete any duplicate rows and reset the index.

- Export data to a CSV file without the DataFrame's index.

## Resources:
chatgpt
ryan norman - UNC bootcamp instructor
https://developer.nytimes.com/docs/articlesearch-product/1/overview
https://www.themoviedb.org/