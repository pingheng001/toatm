It has been tested and approved for use in python2.7.9

#Twitter OAuth Access Token Manager for Python(ToAtmFp)
Twitter OAuth access token management tool for python twitter app developer.
You can easily use access token of user who did not create twitter API of the app that you are developing.

## Usage
### 0. Install Tweepy
If you want to install the latest Tweepy via pip:

```
pip install tweepy
```

You may also use Git to clone the repository from Github and install it manually:

```
git clone https://github.com/tweepy/tweepy.git
cd tweepy
python setup.py install
```

`

### 1. Run ToAtmFp app.

```
$ python toatm.py
```

### 2. Register your API key of your app.

```
Please select mode.
        1 Update API keys
        2 Update Access tokens
        3 Show access tokens
        q Exit

>> 1
CONSUMER KEY: ************
CONSUMER SECRET: *************
```

### 3. Fetch access token and access token secret.

```
Please select mode.
        1 Update API keys
        2 Update Access tokens
        3 Show access tokens
        q Exit

>> 2
Access: https://api.twitter.com/oauth/authorize?oauth_token=***************
Verifier: *******
Updated access token for @****** successfully.
```

### 4. Recall access tokens from your python app.

Example when username of twitter account is @hoge:
```
import shelve
# Open database file
d = shelve.open('keys.shelve')
print d["hoge"]
```

You can obtain the output shown below.
```
{'access_token': u'****', 'access_token_secret': u'****'}
```
API keys configured in Step 1 are also obtained:
```
print d["consumer_key"]
print d["consumer_secret"]
```

If you want to fetch tokens as "str",
```
str(d["hoge"])
```

## Basic Snippets

### download timeline
```
# -*- coding: utf-8 -*-

import shelve
import tweepy

# Configure screen name @~~~~
SCREEN_NAME = "~~~~"

# Open database file
d = shelve.open('keys.shelve')
consumer_key = d['consumer_key']
consumer_secret = d['consumer_secret']
access_token = d[SCREEN_NAME]['access_token']
access_token_secret = d[SCREEN_NAME]['access_token_secret']

# Setup tweepy
auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)
api = tweepy.API(auth)

# Main
public_tweets = api.home_timeline()
for tweet in public_tweets:
    print tweet.text
```

## Notice

Don't forget to except keys.shelve from a viewpoint of security if you will upload your application with ToAtmFp.
For instance, when you want to push app to public repository, write "keys.shelve" in .gitignore.
