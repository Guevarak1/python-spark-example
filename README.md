# python-spark-example

kafkaTweetProducer.py streams in tweets via the tweepy API, pushes those tweets to a Kafka topic.

tweetSentimentCount.py reads in the twitter kafka stream, for every stream of tweets that is streamed in, the Afinn API performs a sentiment anaysis on the tweet. The resulting DataFrame groups the tweets into either positive, negative or neutral scored tweets and they get counted per batch.

example of 3 positive, 1 negative, and 12 neutral tweets on a query track for "2018"


+--------+-----+

|grade   |count|

+--------+-----+

|POSITIVE|3    |

|NEGATIVE|1    |

|NEUTRAL |12   |

+--------+-----+

