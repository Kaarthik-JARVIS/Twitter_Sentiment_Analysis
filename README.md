# Twitter_Sentiment_Analysis
To analyze public tweets about a topic using python, tweepy, textblob and to generate a pie chart using matplotlib

# Step 1: Installation of the required packages

Tweepy: tweepy is the python client for the official Twitter API, install it using following pip command:
     
        pip install tweepy

TextBlob: textblob is the python library for processing textual data, install it using following pip command:

        pip install textblob

Also, we need to install some NLTK corpora using following command:

        python -m textblob.download_corpora

(Corpora is nothing but a large and structured set of texts.)

# Step 2: Authentication

In order to fetch tweets through Twitter API, one needs to register an App through their twitter account. Follow these steps for the same:

Open this [link](https://developer.twitter.com/en/apps) and click the button: ‘Create New App’

Fill the application details. You can leave the callback url field empty.

Once the app is created, you will be redirected to the app page.

Open the ‘Keys and Access Tokens’ tab.

Copy ‘Consumer Key’, ‘Consumer Secret’, ‘Access token’ and ‘Access Token Secret’.

# Step 3: Implementation

Import the required packages as following

     import re 
     import tweepy 
     from tweepy import OAuthHandler 
     from textblob import TextBlob 
     import matplotlib.pyplot as plt

Create a constructor for the class which authenticates the twitter client

     class TwitterClient(object): 
         ''' 
         Generic Twitter Class for sentiment analysis. 
         '''
         def __init__(self): 
             ''' 
             Class constructor or initialization method. 
             '''
             # keys and tokens from the Twitter Dev Console 
             consumer_key = 'XXXXXXXXXXXXXXXXXXXXXXX'
             consumer_secret = 'XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX'
             access_token = 'XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX'
             access_token_secret = 'XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX'

             # attempt authentication 
             try: 
                 # create OAuthHandler object 
                 self.auth = OAuthHandler(consumer_key, consumer_secret) 
                 # set access token and secret 
                 self.auth.set_access_token(access_token, access_token_secret) 
                 # create tweepy API object to fetch tweets 
                 self.api = tweepy.API(self.auth) 
             except: 
                 print("Error: Authentication Failed")
                 
Create a method which fetches the tweet inside the 'TwitterClient' class

     def get_tweets(self, query, count = 10): 
             ''' 
             Main function to fetch tweets and parse them. 
             '''
             # empty list to store parsed tweets 
             tweets = [] 

             try: 
                 # call twitter api to fetch tweets 
                 fetched_tweets = self.api.search(q = query, count = count) 

                 # parsing tweets one by one 
                 for tweet in fetched_tweets: 
                     # empty dictionary to store required params of a tweet 
                     parsed_tweet = {} 

                     # saving text of tweet 
                     parsed_tweet['text'] = tweet.text 
                     # saving sentiment of tweet 
                     parsed_tweet['sentiment'] = self.get_tweet_sentiment(tweet.text) 

                     # appending parsed tweet to tweets list 
                     if tweet.retweet_count > 0: 
                         # if tweet has retweets, ensure that it is appended only once 
                         if parsed_tweet not in tweets: 
                             tweets.append(parsed_tweet) 
                     else: 
                         tweets.append(parsed_tweet) 

                 # return parsed tweets 
                 return tweets 

             except tweepy.TweepError as e: 
                 # print error (if any) 
                 print("Error : " + str(e)) 

The below piece of code in the same class is to classify the tweets whether it is positive or negative using 'textblob'

     def get_tweet_sentiment(self, tweet): 
             ''' 
             Utility function to classify sentiment of passed tweet 
             using textblob's sentiment method 
             '''
             # create TextBlob object of passed tweet text 
             analysis = TextBlob(self.clean_tweet(tweet)) 
             # set sentiment 
             if analysis.sentiment.polarity > 0: 
                 return 'positive'
             elif analysis.sentiment.polarity == 0: 
                 return 'neutral'
             else: 
                 return 'negative'
  
