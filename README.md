# python-spark-example

kafkaTweetProducer.py streams in tweets via the tweepy API, pushes those tweets to a Kafka topic.

tweetSentimentCount.py reads in the twitter kafka stream, for every stream of tweets that is streamed in, the Afinn API performs a sentiment anaysis on the tweet. The resulting DataFrame groups the tweets into either positive, negative or neutral scored tweets and they get counted per batch.

example of 3 positive, 1 negative, and 12 neutral tweets on a query track for "2018"


+--------+-----+<br>
|grade   |count|<br>
+--------+-----+<br>
|POSITIVE|3    |<br>
|NEGATIVE|1    |<br>
|NEUTRAL |12   |<br>
+--------+-----+<br>

set of commands needed to run

start zookeeper and kafka: <br>
bin/zookeeper-server-start.sh config/zookeeper.properties & bin/kafka-server-start.sh config/server.properties

create new kafka topic<br>
bin/kafka-topics.sh --create --zookeeper localhost:2181 \
--replication-factor 1 \
--partitions 1 \
--topic first_kafka_topic

view messages being consumed on topic<br>
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first_kafka_topic --from-beginning

twitter client that produces the stream of tweets with tracks t0 the kafka topic<br>
python3 kafkaTweetProducer.py localhost 9092 first_kafka_topic "world cup"

spark data job that finds the tweets sentiment analysis<br>
spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.2.0 tweetSentiment.py localhost 9092 first_kafka_topic

