# Twitter Analysis of #NG30DaysOfLearning

<img align="right" alt="Tweets" width="1000" height = "400" src="https://user-images.githubusercontent.com/106287208/184046148-d4e111a6-8eb7-40cb-a830-ed3fd2a507e3.png">

---


# Table of Contents

- [Introduction](https://github.com/globalsmile/Twitter-Analysis#introduction)
- [Problem Statement](https://github.com/globalsmile/Twitter-Analysis#Problem-Statement)
- [Data Sourcing](https://github.com/globalsmile/Twitter-Analysis#Data-Sourcing)
- [Data Transformation](https://github.com/globalsmile/Twitter-Analysis#Data-Transformation)
- [Data Modeling](https://github.com/globalsmile/Twitter-Analysis#Data-Modeling)
- [Data Visualization](https://github.com/globalsmile/Twitter-Analysis#Data-Visualization)
- [Data Analysis](https://github.com/globalsmile/Twitter-Analysis#Data-Analysis)
- [Insights](https://github.com/globalsmile/Twitter-Analysis#Insights)
- [Shareable link](https://github.com/globalsmile/Twitter-Analysis#Shareable-Link)


---

# Introduction


The 30Days of Learning programme is organized by the team at Microsoft to help students upkill with Microsoft technologies by learning and building solutions 
across these knowledge areas; Data Analysis Using Power BI, Low-code/No-Code Application Development using Power Platform, and Data Science and Machine Learning with Azure..

[Learn More](https://techcommunity.microsoft.com/t5/educator-developer-blog/onboarding-guide-for-30days-of-learning-participants/ba-p/3485136)


---

# Problem Statement

The purpose of this analysis is to analyze the number of engagements of the #NG30DaysofLearning has on twitter.

For this study we examined a variety of categories: the number of tweets, number of users, the most active users, the most mentioned tools e.t.c

---

# Data Sourcing

The dataset used in this analysis was scrapped from twitter using the python code below on jupyter notebook:


    
     
     
      import pandas as pd
      import snscrape.modules.twitter as sntwitter
      query = "(#30DaysOfLearning OR #NG30DaysOfLearning) until:2022-06-26 since:2022-05-01"
      tweets = []
      limit = 30000


      for tweet in sntwitter.TwitterHashtagScraper(query).get_items():
    
             if len(tweets) == limit:
                     break
             else:
                     tweets.append([tweet.date, tweet.url, tweet.user.username, tweet.sourceLabel, tweet.user.location, tweet.content,                        tweet.likeCount, tweet.retweetCount,  tweet.quoteCount, tweet.replyCount])
        
      df = pd.DataFrame(tweets, columns=["Date", "TweetURL","User", "Source", "Location", "Tweet", "Likes_Count","Retweet_Count",               "Quote_Count", "Reply_Count"])

      df.to_csv("30DLTweets.csv")
      df.head()
      
     

- The dataset is also available at [30DLTweets](https://github.com/theoyinbooke/30Days-of-Learning-Data-Analysis-Using-Power-BI-for-Students/blob/main/Twitter%20Data%20Web%20Scrape/30DLTweets.csv)

---

# Data Transformation

Data transformation was done in Power Query and the dataset was loaded into Microsoft Power BI Desktop for modeling.

The dataset contains a table named `Tweet_Analysis` :

- `Tweet_Analysis` has `11 columns and 680 rows` of observation


The tabulation below shows the `Tweet_Analysis` table with its column names and their description:
| Column Name | Description |
| ----------- | ----------- |
| Serial No | Represents the count of the tweet |
| Date | Represents the date and time of tweet |
| TweetURL | Describes the tweet url |
| User | Describes the username of the user |
| Source| Descibes the device type of the user  |
| Location | describes the location of the user |
| Tweet | Describes the content of the tweet |
| Likes_Count | Represents the count of likes of the tweet |
| Retweet_Count | Represents the count of retweets of the tweet |
| Quote_Count | Represents the count of quote tweets on the tweet |
| Reply_Count | Represents the count of reply on the tweet |

Data Cleaning for the dataset was done in power query as follows:

- The `Location` column was filtered to remove empty rows and values
- Date only was extracted from the `Date` column
- The extracted column was renamed to `Date ` 
- Unnecessary column (` Serial No`)  was removed

To ensure the accuracy of the dates in the `Date` column each of the tables, a date table was created for referencing using the M-formula:

`{Number.From(List.Min(Transactions[Date]))..Number.From(List.Max(Transactions[Date]))}`

Here is a breakdown of what the formula does:

For the dataset, we want the start date to reflect the earliest to latest date that we have in the data: May 9, 2022 - June 25, 2022.

`Day Name` column was inserted into the date table and renamed to ` DayOfTheWeek` 

The date table was named `Calender`.

---

# Data Modeling

After the dataset was cleaned and transformed, it was ready to be modeled.

- The `Calender` table was marked as the official date table in the dataset.
- A `one-to-many (*:1) relationship` was created between the `Tweet_Analysis` and the `Calender` tables using the `date` column in each of the tables 
- The realtioships formed in the data model is shown below:

---

# Data Visualization

Data visualization for the datasets was done in 3 folds using Microsoft Power BI Desktop:

- The `Content Analysis`: Shows the tools by mention, word cloud, Top active users, etc.
-  The `Summary`: Shows the total number of tweets, total number of users, Tweet by day of the week, etc.
-  The `Dashboard`: Shows visualization from `Content Analysis` and `Summary` to provide answer to the [Problem Statement](https://github.com/globalsmile/Twitter-Analysis#Problem-Statement).


Figure 1 shows visualizations from `Content Analysis` worksheet

| Figure 1 |
| ----------- |
| ![image](https://user-images.githubusercontent.com/106287208/184047582-a51ce75a-ccb9-4157-a42f-3dd7f86a0748.png) |

Figure 2 shows visualizations from `Summary` worksheet

| Figure 2 |
| ----------- |
| ![image](https://user-images.githubusercontent.com/106287208/184047639-6a4fe424-b0e2-4f4f-a7e7-1fb79c33afa6.png) |

Figure 3 shows visualizations from `Dashboard` worksheet

| Figure 3 |
| ----------- |
| ![image](https://user-images.githubusercontent.com/106287208/184047713-78bcfb2c-a8b1-4066-ac09-69b095a4a056.png) |

---

# Data Analysis

Measures used in visualization are:

- Total Tweets = `SUM(Tweet_Analysis[Tweet])`
- Total Users = `SUM(Tweet_Analysis[user])`
- Number of Days = `SUM(Tweet_Analysis[Date])`


As shown from [Data Visualization](https://github.com/globalsmile/Twitter-Analysis#Data-Visualization), It can be deducted that:

- The were `480` tweets for the #NG30DaysOfLearning
- The were about `148` users
- The observation lasted  for `23` days

---

# Insights

As shown by [Data Visualization](https://github.com/globalsmile/Client-Finacial-Analysis#Data-Visualization), It can be deducted that:

- The most active user of the #NG30DaysOfLearning is [theoyinbooke](https://techcommunity.microsoft.com/t5/user/viewprofilepage/user-id/1379718)
- The most mentioned tool is Github

---

# Shareable Link

You can interact with the dashboard here: 

https://app.powerbi.com/view?r=eyJrIjoiMTUyNWU1NGMtODI1ZS00ZGVmLWFlYzEtYWI1NWE1YWUzOGYxIiwidCI6IjQ5ODY4YWYzLWNjNWYtNDIxNC04YjdmLTQwZjM3NDY0OWEwOSJ9
