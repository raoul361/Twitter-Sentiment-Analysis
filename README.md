#Twitter Sentiment Analysis

One of the things I wanted to try was running **sentiment analysis** as a way of measuring **external risk** for an organisation. This could be many forms - public protest, user dissatisfaction or disaster response/early warning. 

My use cases revolve very much around taking this real time information into the context of a **Security Operations Centre** and using it as a leading indicator for potential malicious activity. Friends have suggested using this to measure failure of changes in DevOps environments; I'm sure there are plenty of others as we will see.


First thing is first; I'm using twitter, but this could easily be applied to any other text based digital channel - email, facebook, SMS. 

I've set up a twitter real time stream, filtering on **_"trump"._** Ahem. Anyway, [Adil Moujahid](http://adilmoujahid.com/) has some nice Python tutorials on this.


Next comes our langauge processing - this is done through the [**Natural Language ToolKit**](http://www.nltk.org/) (NLTK). This is a hefty install and comprises of loads of libraries and dictionaries, most of which we'll never use. 

My focus is on the **"Vader"** sentiment ananlysis classes.

```
from nltk.sentiment.vader import SentimentIntensityAnalyzer
```

I've got a few lines to strip links and neaten up the individual tweets. I tokensize the text of the tweet and generate a **_sentiment  score._** Then extract all the hashtags and dump the whole thing to stdout. 

![My image](/python code.jpg)

The following output is produced. I've not included the text of tweets, as some of these tweets were truly disturbing. Might be different if you work off a corporate twitter handle. 

In most of my analysis, I focus on meta-data alone.

![My image](/logs.jpg)


These then go into **Splunk**. A simple **regex parser** takes in values for Sentiment, Twitter name, Langauge and Hashtags. 

I can then easily craft searches to pull out trends, averages, top talkers, top (positive/negative) hashtags, the list is endless!

Whilst experimenting, I was able to see the **Hamilton** controversy hit real time - ***this stuff definitely works!***

![My image](/splunk.jpg)


Note: I haven't release the code - it is very basic and not really stable for production. I provide this as a demonstration only.

[**_@raoulendres_**](https://twitter.com/raoulendres)
