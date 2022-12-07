# CourseProject - FIFA World Cup Sentiment Analysis

Developer : Susovan Samanta

# Overview

The puprpose of this project to perform sentiment analysis for FIFA 2022 World Cup. The Project will take input parameter of both the team names and match date to start the process. It will do sentiment analysis for each player from both teams to understand how well it corelates with actual match performance.
As a reference it will analyze tweets related to that match and analyze all tweets for the players played in that match.

The process will also get data from https://fbref.com/en/ To fetch the match details and stats specifically all the players name who played that match.

# Team Members

I am working in this project alone.

# Code Documentation

First of all we need to install all the required libraries.
```
pip install tweepy

pip install BeautifulSoup4 
```
Below packages are also required

### tweepy
https://www.tweepy.org/

An easy-to-use Python library for accessing the Twitter API.

### beautifulsoap
https://beautiful-soup-4.readthedocs.io/en/latest/

Beautiful Soup is a Python library for pulling data out of HTML and XML files

### pandas
https://pandas.pydata.org/docs/index.html

pandas is an open source, BSD-licensed library providing high-performance, easy-to-use data structures and data analysis tools for the Python programming language.

### NumPy
https://numpy.org/

NumPy is an open source project aiming to enable numerical computing with Python

### Matplotlib
https://matplotlib.org/

Matplotlib is a comprehensive library for creating static, animated, and interactive visualizations in Python. Matplotlib makes easy things easy and hard things possible.

# Code Structure and Flow description

We can devide the processs in 4 parts

1. Get the initial details for mentioned FIFA 2022 World cup match from a webpage.
2. Twitter API authentication to search required tweets.
3. Using Textblob perform sentiment analysis for each team members.
4. Plotting the sentiment result into a bar chart for visual representation
5. Using BM25Okapi perform a positive sentiment Analysis for each players.
6. Plotting the sentiment result into a bar chart for visual representation

### 1. Get the initial details for mentioned FIFA 2022 World cup match from a webpage.

Fetch the initial FIFA 2022 world cup match details from "https://fbref.com/en/". 
```
fbref_url = "https://fbref.com/en/comps/1/World-Cup-Stats"
req = requests.get(fbref_url)
```
Using beautifulsoap parse the HTML
```
soup = BeautifulSoup(req.text, features="html.parser")
```
Then select players from the sepcific page.
```
req = requests.get(Match_url[0])
soup = BeautifulSoup(req.text, features="html.parser")
```
### 2. Twitter API authentication to search required tweets.

I have used my own API keys to fetch tweets.You need to suppy your own API keys to run the process.
```
consumer_key = ' '
consumer_secret = ' '
access_token = ' '
access_token_secret = ' '
bearer_token = ' '
```
### 3. Using Textblob perform sentiment analysis for each team members.

Fetch tweets for each players.
```
api = tweepy.API(auth, wait_on_rate_limit=True)
tweets = tweepy.Cursor(api.search_tweets,q= player or joint,until=date_until, result_type = "recent" ).items() # find tweets for each player
```
Perform sentiment analysis using textblob
```
players_sentiments.append(TextBlob(tweet.text).sentiment)  
```
### 4. Plotting the sentiment result into a bar chart for visual representation

Plot the sentiment result using Matplotlib in horizontal bar chart

![United States_senteminet](https://user-images.githubusercontent.com/112344802/206137601-2483140c-e4ef-4df0-8283-7ce2163fd451.png)

![Netherlands_senteminet](https://user-images.githubusercontent.com/112344802/206137523-bc2f0faa-5f28-44ae-948d-cca9d647e5dc.png)


### 5. Using BM25Okapi perform a positive sentiment Analysis for each players.

Using BM25Okapi perform sentiment analysis with positive terms.
```
positive_terms = "gols gol good score goal pass Assist assistência strike lead win bueno" 
tokenized_positive_term = positive_terms.split(" ")
```
BM25 implementatiom
```
bm25 = BM25Okapi(tokenized_corpus)
score = bm25.get_scores(terms)
```
### 6. Plotting the sentiment result into a bar chart for visual representation

Plot the BM25 sentiment result using Matplotlib in horizontal bar chart

![United States_BM25_Sentiment](https://user-images.githubusercontent.com/112344802/206138309-dd9731a3-fea3-4677-9c7a-cebb41594a0c.png)

![Netherlands_BM25_Sentiment](https://user-images.githubusercontent.com/112344802/206138353-c4021d25-4d8c-4213-a912-a7c8dcab2b17.png)

# Conclusion
This code gives a basic structure of sentiment analysis using Textblob and also use OkapiBM25 for positive sentiment analysis based on positive terms.

# Potential Improvements
The code can be more effecient in general. And potential imporvements are below.

We can implement negative sentiment also with given positive sentiment.
Language restriction was a challenge while implementing the sentiment analysis. As it is a world cup game, people are tweeting from across the globe and most of them in Spanish, Portuguese which should be implemented properly in the algorithm.

