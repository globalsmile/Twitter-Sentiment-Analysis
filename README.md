# Twitter Analysis of #NG30DaysOfLearning

<img align="right" alt="Tweets" width="1000" height = "400" src="https://user-images.githubusercontent.com/106287208/187567112-ec593f73-7afe-4ef3-8c80-822591b89038.png">

---


# Table of Contents

- [Introduction](https://github.com/globalsmile/Twitter-Sentiment-Analysis#introduction)
- [Problem Statement](https://github.com/globalsmile/Twitter-Sentiment-Analysis#Problem-Statement)
- [Data Sourcing](https://github.com/globalsmile/Twitter-Sentiment-Analysis#Data-Sourcing)
- [Data Preparation](https://github.com/globalsmile/Twitter-Sentiment-Analysis#Data-Preparation)
- [Data Modeling](https://github.com/globalsmile/Twitter-Sentiment-Analysis#Data-Modeling)
- [Data Visualization](https://github.com/globalsmile/Twitter-Sentiment-Analysis#Data-Visualization)
- [Data Analysis](https://github.com/globalsmile/Twitter-Sentiment-Analysis#Data-Analysis)
- [Insights](https://github.com/globalsmile/Twitter-Sentiment-Analysis#Insights)
- [Shareable link](https://github.com/globalsmile/Twitter-Sentiment-Analysis#Shareable-Link)


---

# Introduction


The 30Days of Learning programme is organized by the team at Microsoft to help students upkill with Microsoft technologies by learning and building solutions 
across these knowledge areas; Data Analysis Using Power BI, Low-code/No-Code Application Development using Power Platform, and Data Science and Machine Learning with Azure..

[Learn More](https://techcommunity.microsoft.com/t5/educator-developer-blog/onboarding-guide-for-30days-of-learning-participants/ba-p/3485136)


---

# Problem Statement

The purpose of this analysis is to gain insights into the number of engagements the #NG30DaysofLearning has on twitter.

For this study we examined a variety of categories: the number of tweets, number of users, the most active users, the most mentioned tools e.t.c

---

# Data Sourcing

- The dataset used for this analysis was scrapped from twitter using python and jupyter notebook
- The preview of the dataset and python code is shown below:


```python
!pip install snscrape
```

    Requirement already satisfied: snscrape in c:\users\user\anaconda3\lib\site-packages (0.4.3.20220106)
    Requirement already satisfied: lxml in c:\users\user\anaconda3\lib\site-packages (from snscrape) (4.8.0)
    Requirement already satisfied: beautifulsoup4 in c:\users\user\anaconda3\lib\site-packages (from snscrape) (4.11.1)
    Requirement already satisfied: requests[socks] in c:\users\user\anaconda3\lib\site-packages (from snscrape) (2.27.1)
    Requirement already satisfied: filelock in c:\users\user\anaconda3\lib\site-packages (from snscrape) (3.6.0)
    Requirement already satisfied: soupsieve>1.2 in c:\users\user\anaconda3\lib\site-packages (from beautifulsoup4->snscrape) (2.3.1)
    Requirement already satisfied: idna<4,>=2.5 in c:\users\user\anaconda3\lib\site-packages (from requests[socks]->snscrape) (3.3)
    Requirement already satisfied: charset-normalizer~=2.0.0 in c:\users\user\anaconda3\lib\site-packages (from requests[socks]->snscrape) (2.0.4)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in c:\users\user\anaconda3\lib\site-packages (from requests[socks]->snscrape) (1.26.9)
    Requirement already satisfied: certifi>=2017.4.17 in c:\users\user\anaconda3\lib\site-packages (from requests[socks]->snscrape) (2021.10.8)
    Requirement already satisfied: PySocks!=1.5.7,>=1.5.6 in c:\users\user\anaconda3\lib\site-packages (from requests[socks]->snscrape) (1.7.1)
    


```python
import pandas as pd
import snscrape.modules.twitter as sntwitter
```


```python
query = "(#30DaysOfLearning OR #NG30DaysOfLearning) until:2022-06-26 since:2022-05-05"
tweets = []
limit = 30000


for tweet in sntwitter.TwitterHashtagScraper(query).get_items():
    
    if len(tweets) == limit:
        break
    else:
        tweets.append([tweet.date, tweet.url, tweet.user.username, tweet.sourceLabel, tweet.user.location, tweet.content, tweet.likeCount, tweet.retweetCount,  tweet.quoteCount, tweet.replyCount])
        
df = pd.DataFrame(tweets, columns=['Date', 'TweetURL','User', 'Source', 'Location', 'Tweet', 'Likes_Count','Retweet_Count', 'Quote_Count', 'Reply_Count'])

df.to_csv('30DLTweets.csv')
```


```python
df.head()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>TweetURL</th>
      <th>User</th>
      <th>Source</th>
      <th>Location</th>
      <th>Tweet</th>
      <th>Likes_Count</th>
      <th>Retweet_Count</th>
      <th>Quote_Count</th>
      <th>Reply_Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2022-06-25 22:51:18+00:00</td>
      <td>https://twitter.com/poetrineer/status/15408300...</td>
      <td>poetrineer</td>
      <td>Twitter for Android</td>
      <td>Oyo, Nigeria</td>
      <td>So as one of my commitment to document my lear...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-06-25 22:44:10+00:00</td>
      <td>https://twitter.com/poetrineer/status/15408282...</td>
      <td>poetrineer</td>
      <td>Twitter for Android</td>
      <td>Oyo, Nigeria</td>
      <td>Finally, here is my updated COVID-19 Data Anal...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2022-06-25 19:25:58+00:00</td>
      <td>https://twitter.com/MichealOjuri/status/154077...</td>
      <td>MichealOjuri</td>
      <td>Twitter Web App</td>
      <td>Oyo, Nigeria</td>
      <td>#30NGDaysOfLearning\n#30daysoflearning \n#micr...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2022-06-25 16:44:36+00:00</td>
      <td>https://twitter.com/oye__aashu/status/15407377...</td>
      <td>oye__aashu</td>
      <td>Twitter for Android</td>
      <td>Nainital, India</td>
      <td>Day 4/ #30daysoflearning learned all about arr...</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2022-06-25 12:49:02+00:00</td>
      <td>https://twitter.com/hsb_data/status/1540678455...</td>
      <td>hsb_data</td>
      <td>Twitter Web App</td>
      <td>New Jersey</td>
      <td>Learning about sub queries on @DataCamp (SQL) ...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.describe()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Likes_Count</th>
      <th>Retweet_Count</th>
      <th>Quote_Count</th>
      <th>Reply_Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>683.000000</td>
      <td>683.000000</td>
      <td>683.000000</td>
      <td>683.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>15.780381</td>
      <td>3.812592</td>
      <td>0.185944</td>
      <td>1.166911</td>
    </tr>
    <tr>
      <th>std</th>
      <td>41.164555</td>
      <td>12.665561</td>
      <td>0.737938</td>
      <td>2.626554</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>8.000000</td>
      <td>2.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>549.000000</td>
      <td>248.000000</td>
      <td>9.000000</td>
      <td>29.000000</td>
    </tr>
  </tbody>
</table>
</div>




The dataset is also available at [30DLTweets](https://github.com/globalsmile/Twitter-Sentiment-Analysis/blob/main/30DLTweets.csv)

---

# Data Preparation

Data transformation was done in Power Query and the dataset was loaded into Microsoft Power BI Desktop for modeling.

The dataset contains a table named `30DLTweets` :

- `30DLTweets` has `10 columns and 680 rows` of observation


The tabulation below shows the `30DLTweets` table with its column names and their description:
| Column Name | Description |
| ----------- | ----------- |
| Date | Represents the date and time of tweet |
| TweetURL | Describes the tweet url |
| User | Describes the username of the user |
| Source| Descibes the device type of the user  |
| Location | Describes the location of the user |
| Tweet | Describes the content of the tweet |
| Likes_Count | Represents the count of likes of the tweet |
| Retweet_Count | Represents the count of retweets of the tweet |
| Quote_Count | Represents the count of quote tweets on the tweet |
| Reply_Count | Represents the count of reply on the tweet |

Data Cleaning for the dataset was done in power query as follows:

- The `30DLTweets` table was split into a dimension and  2 fact tables respectively, hence called:
1. `UserProfile`
2. `TweetStats`
3. `TweetProfile`

- A calculated column `UserID` was created in each of the tables using the M-formula `UserID = [User] & "_" & [Source]`
- Unnecessary columns were removed in each of the tables
- Each of the columns in the tables were validated to have the correct data type


To ensure the accuracy of the dates in the `Date` column of `TweetStats` and `TweetProfile` tables, a date table was created for referencing using the M-formula:

`{Number.From(List.Min(TweetProfile[Date]))..Number.From(List.Max(TweetProfile[Date]))}`

Here is a breakdown of what the formula does:

For the dataset, we want the start date to reflect the earliest to latest date that we have in the data: May 9, 2022 - June 25, 2022.

`Day Name` column was inserted into the date table and renamed to ` DayOfTheWeek` 

The date table was named `Calender`.

---

# Data Modeling

After the dataset was cleaned and transformed, it was ready to be modeled.

- The `Calender` table was marked as the official date table in the dataset.
- A `one-to-many (*:1) relationship` was created between the `TweetStats` and the `Calender` tables using the `date` column in each of the tables 
- A `one-to-many (*:1) relationship` was created between the `TweetProfile` and the `Calender` tables using the `date` column in each of the tables 
- A `one-to-many (*:1) relationship` was created between the `UserProfile` and the `TweetStats` tables using the `UserID` column in each of the tables 
- A `one-to-many (*:1) relationship` was created between the `UserProfile` and the `TweetProfile` tables using the `UserID` column in each of the tables 
- The realtioships formed in the data model is a `Star Schema` and is shown below:

<img align="right" alt="Data Model" width="1000" height = "400" src="https://user-images.githubusercontent.com/106287208/187106255-bd25a422-fd74-4f5e-a529-7a9052915252.png">


---

# Data Visualization

Data visualization for the datasets was done in 3 folds using Microsoft Power BI Desktop:

- The `Content Analysis`: Shows the tools by mention, word cloud, Top active users, etc.
-  The `Summary`: Shows the total number of tweets, total number of users, Tweet by day of the week, etc.
-  The `Dashboard`: Shows visualization from `Content Analysis` and `Summary` to provide answer to the [Problem Statement](https://github.com/globalsmile/Twitter-Sentiment-Analysis#Problem-Statement).


Figure 1 shows visualizations from `Content Analysis` page

| Figure 1 |
| ----------- |
| ![image](https://user-images.githubusercontent.com/106287208/187567316-46bc6332-7507-4f11-b3c7-a18a52ed8e14.png) |

Figure 2 shows visualizations from `Summary` page

| Figure 2 |
| ----------- |
| ![image](https://user-images.githubusercontent.com/106287208/187567503-2db262f6-c7f2-449d-9b11-01ff7e084022.png) |

Figure 3 shows visualizations from `Dashboard` page

| Figure 3 |
| ----------- |
| ![image](https://user-images.githubusercontent.com/106287208/187677655-9bbd0398-f0fe-4af0-870f-f9e090633f13.png) |

---

# Data Analysis

Measures used in visualization are:

- Total No. of Tweets = `COUNT(TweetProfile[Tweet])`
- Total No. of Users = `COUNT(UserProfile[user])`
- Total No. of Sources = `COUNT(UserProfile[Source])`
- Average Engagement Rate = `DIVIDE(Total No. of Users, Total No. of Tweets)`


As shown from [Data Visualization](https://github.com/globalsmile/Twitter-Sentiment-Analysis#Data-Visualization), It can be deducted that:

- The were `680` tweets for the #NG30DaysOfLearning
- The were about `234` users
- The average engagement rate is `34%` 

---

# Insights

As shown by [Data Visualization](https://github.com/globalsmile/Twitter-Sentiment-Analysis#Data-Visualization), It can be deducted that:

- The most active user of the #NG30DaysOfLearning is [theoyinbooke](https://techcommunity.microsoft.com/t5/user/viewprofilepage/user-id/1379718) with 110 tweets
- The most mentioned tool is Github

---

# Shareable Link

You can interact with the report here: 

[Report](https://app.powerbi.com/view?r=eyJrIjoiZjMzMjk1ZDAtYzBjYy00OTZjLTk1YzQtMzI1MjE0NWFkOGYxIiwidCI6IjQ5ODY4YWYzLWNjNWYtNDIxNC04YjdmLTQwZjM3NDY0OWEwOSJ9)
