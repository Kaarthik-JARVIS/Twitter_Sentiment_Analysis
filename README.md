# Twitter_Sentiment_Analysis
To analyze public tweets about a topic using python, tweepy, textblob and to generate a pie chart using matplotlib

Step 1: Installation of the required packages

        Tweepy: tweepy is the python client for the official Twitter API, install it using following pip command:
     
                pip install tweepy

        TextBlob: textblob is the python library for processing textual data, install it using following pip command:

                pip install textblob

        Also, we need to install some NLTK corpora using following command:

                python -m textblob.download_corpora

        (Corpora is nothing but a large and structured set of texts.)

Step 2: Authentication

In order to fetch tweets through Twitter API, one needs to register an App through their twitter account. Follow these steps for the same:

        Open this [link](https://developer.twitter.com/en/apps) and click the button: ‘Create New App’
        Fill the application details. You can leave the callback url field empty.
        Once the app is created, you will be redirected to the app page.
        Open the ‘Keys and Access Tokens’ tab.
        Copy ‘Consumer Key’, ‘Consumer Secret’, ‘Access token’ and ‘Access Token Secret’.
