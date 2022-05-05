# Introduction to Stream Processing

## Course Overview

In this course, you will learn how stream processing and streaming data are changing the way that data teams throughout our industry operate. Streaming data and stream processing represents a paradigm shift in how data teams conceptualize their data problems and the speed at which they can react.

By the end of this course, you will be fluent in the most well-known data streaming tool in the market today - Kafka - and its ecosystem. Beyond that, you will also learn how to use stream processing tools like Faust and KSQL to find real-time insights from your data streams.

The course is split into two parts. The first part focuses on Data Streaming via Kafka and its extended ecosystem. The second part focuses on performing Stream Processing on streaming data sources already in Kafka.

With these skills, you will be well on your way to having the knowledge you need to build a world-class stream processing application.

## Lesson Overview

In this lesson we will discuss:

* Processing Data in Stream and in Batches
* Using Kafka for Stream Processing
* Using the Kafka Command Line Interface (CLI)
* Differentiating between Kafka Topics, Producers and Consumers

A deep understanding of these concepts will provide a strong foundation for building stream processing applications.

## Glossary of Key Terms You’ll Learn in this Lesson

* **Stream** - An unbounded sequence of ordered, immutable data
* **Stream Processing** - Continual calculations performed on one or more Streams
* **Immutable Data** - Data that cannot be changed once it has been created
* **Event** - An immutable fact regarding something that has occurred in our system.
* **Batch Processing** - Scheduled, periodic analysis of one or more groups of related data.
* **Data Store** - A generic place that holds data of some kind, like a message queue or data store
* **Stream Processing Application** - An application which is downstream of one or more data streams and performs some kind of calculation on incoming data, typically producing one or more output data streams
* **Stream Processing Framework** - A set of tools, typically bundled as a library, used to construct a Stream Processing Application
* **Real-time** - In relation to processing, this implies that a piece of data, or an event, is processed almost as soon as it is produced. Strict time-based definitions of real-time are controversial in the industry and vary widely between applications. For example, a Computer Vision application may consider real-time to be 1 millisecond or less, whereas a data engineering team may consider it to be 30 seconds or less. In this class when the term "real-time" is used, the time-frame we have in mind is seconds.
* **Append-only Log** - files in which incoming events are written to the end of the file as they are received
* **Change Data Capture (CDC)** - The process of capturing change events, typically in SQL database systems, in order to accurately communicate and synchronize changes from primary to replica nodes in a clustered system.
* **Log-Structured Storage** - Systems built on Append-Only Logs, in which system data is stored in log format.
* **Merge (Log Files)** - When two or more log files are joined together into a single output log file
* **Compact (Log Files)** - When data from one or more files is deleted, typically based on the age of data
* **Source (Kafka)** - A term sometimes used to refer to Kafka clients which are producing data into Kafka, typically in reference to another data store
* **Sink (Kafka)** - A term sometimes used to refer to Kafka clients which are extracting data from Kafka, typically in reference to another data store
* **Topic (Kafka)** - A logical construct used to organize and segment datasets within Kafka, similar to how SQL databases use tables
* **Producer (Kafka)** - An application which is sending data to one or more Kafka Topics.
* **Consumer (Kafka)** - An application which is receiving data from one or more Kafka Topics.

## Understanding Stream Processing

In computing, a _stream_ is typically thought of as a potentially unbounded sequence.

_Stream Processing_ is the act of performing continual calculations on a potentially endless and constantly evolving source of data.

Stream Processing applications perform calculations on Data Streams. Data Streams consist of a potentially endless stream of _immutable_ data.

Immutable data does not change -- once the data has been placed in the data stream it can never be updated. Another data entry can be placed in the stream that supersedes the previous data entry if necessary.

Data sent to data streams is typically _small, less than 1MB in size_.

The data throughput to data streams is highly variable. Some streams will receive thousands or tens of thousands of records per second, and some will receive one or two records per hour.

[![What Is Stream Processing](https://img.youtube.com/vi/jjE9YDcX8Ps/0.jpg)](https://www.youtube.com/watch?v=jjE9YDcX8Ps)

### Stream Processing

* Stream Processing acts on potentially endless and constantly evolving immutable data contained in data streams.
* Once data have been placed in a data stream, they cannot be modified. We must place a new record in the stream to override the existing data.
* Finally, data in data streams is typically less than 1MB in size and the data volume may vary from a few records an hour to thousands of requests per second.

[![What Is An Event](https://img.youtube.com/vi/jI7PhkgOYHk/0.jpg)](https://www.youtube.com/watch?v=jI7PhkgOYHk)

* **Event** – an immutable fact regarding something that occurred within a system. It can not be changed, once created. Data records in the context of data streaming are events.
* In many SQL databases, it is uncommon to track the history of what values were used for a particular user in the past.
* **Message Queues** – typically communicate commands to perform an action
* **Invented Systems** – react to the facts that are indirectly communicated to them, for example, via user clicks

#### QUESTION 1 OF 2

What is an event?

- [ ] A command to a downstream system to perform an action

- [x] An immutable fact regarding something that occurred within our software system

- [ ] An aggregated representation of the current state of the system

- [ ] A user click on a button

#### QUESTION 2 OF 2

Which of the following statements about stream processing is true? (may be multiple answers)

- [x] Stream processing acts on potentially endless and constantly evolving data

- [ ] The individual events in the data stream are typically larger than 1MB in size

- [x] The data in the stream is immutable

- [ ] Streaming data is always in the thousands of events per second

- [x] To update an event in a stream, a new record is placed in the stream to override the existing data

## Stream Processing Examples

[![Examples Of Stream Processing](https://img.youtube.com/vi/DhO1Dcm5VoQ/0.jpg)](https://www.youtube.com/watch?v=DhO1Dcm5VoQ)

### Stream Processing Examples

#### Log Analysis

One of the first places many companies use stream processing is in log analysis. Companies often run microservices that constantly produce logs that are full of information that can be mined for:

* User behavior patterns
* Failure prediction
* Debugging

These logs generate a tremendous amount of data on an ongoing basis, which can be difficult to then analyze. To solve this issue, each log produced by a microservice becomes an event in a data stream.

Companies then build programs that can analyze and join on the events in these data streams to find insights into the data.

![Log Analysis condenses logs from many servers into a single ordered stream](https://video.udacity-data.com/topher/2019/September/5d6ed1b1_screen-shot-2019-09-03-at-1.48.39-pm/screen-shot-2019-09-03-at-1.48.39-pm.png)

#### Web Analytics

Modern web applications measure almost every action a user takes on their site, for example:

* button clicks
* Page load times
* Session duration

The volume of these actions can quickly overwhelm a traditional **data store** (any place you keep data). Ingesting and analyzing this data can be difficult and companies use stream processing to analyze the data as it is generated.

The benefits of this process are:

* it lessens the long-term processing burden for companies because of the smaller dataset
* provides real-time analysis instead of long-running bath analyses that may only be updated periodically

![Analyzing streaming user events for web analytics](https://video.udacity-data.com/topher/2019/September/5d6f1243_screen-shot-2019-09-03-at-6.23.37-pm/screen-shot-2019-09-03-at-6.23.37-pm.png)

#### Real-Time Pricing

Ride-sharing applications are a great example of data streaming for real-time analysis. They use real-time pricing that adjusts with environmental factors and instantaneous demand.

![Determining ride-share pricing on streaming real-time event data](https://video.udacity-data.com/topher/2019/September/5d6f12a1_screen-shot-2019-09-03-at-6.25.45-pm/screen-shot-2019-09-03-at-6.25.45-pm.png)

#### Stream Processing Examples Recap

Stream Processing is a critical component in a number of familiar technology applications:

* Finding patterns and meaningful data in disparate log messages in a microservices architecture
* Tracking user engagement in real-time with streaming website analytics
* Real-time pricing in ride-sharing applications based on demand and environmental conditions
* Stock buying/selling based on price, news, and social media sentiment

## Stream vs. Batch Processing

[![Contrasting Stream And Batch Processing](https://img.youtube.com/vi/lHPQDWSw7IE/0.jpg)](https://www.youtube.com/watch?v=lHPQDWSw7IE)

### Batch Processing

* Runs on a scheduled basis
* May run for a longer period of time and write results to a SQL-like store
* May analyze all historical data at once
* Typically works with mutable data and data stores

### Stream Processing

* Runs at whatever frequency events are generated
* Typically runs quickly, updating in-memory aggregates
* Stream Processing applications may simply emit events themselves, rather than write to an event store
* Typically analyzes trends over a limited period of time due to data volume
* Typically analyzes immutable data and data stores

_Batch and Stream processing are not mutually exclusive_. Batch systems can create events to feed into stream processing applications, and similarly, stream processing applications can be part of batch processing analyses.

### Components of a Stream Processing Solution

[![Components Of A Stream Processing Solution](https://img.youtube.com/vi/u8yl2PRXrEg/0.jpg)](https://www.youtube.com/watch?v=u8yl2PRXrEg)

### Streaming Data Store

* May look like a message queue, as is the case with Apache Kafka
* May look like a SQL store, as is the case with Apache Cassandra
* Responsible for holding all of the immutable event data in the system
* Provides guarantee that data is stored ordered according to the time it was produced
* Provides guarantee that data is produced to consumers in the order it was received
* Provides guarantee that the events it stores are immutable and unchangeable

### Stream Processing Application and Framework

* Stream Processing applications sit downstream of the data store
* Stream Processing applications ingest real-time event data from one or more data streams
* Stream Processing applications aggregate, join, and find differences in data from these streams
* Common Stream Processing Application Frameworks in use today include:

    * Confluent KSQL
    * Kafka Streams
    * Apache Flink
    * Apache Samza
    * Apache Spark Structure Streaming
    * Faust Python Library

### Further Optional Reading on Message Queues

[RabbitMQ](https://www.rabbitmq.com/)
[ActiveMQ](https://activemq.apache.org/)

### Benefits of Stream Processing

[![The Benefits Of Stream Processing](https://img.youtube.com/vi/HuqHnCAGWEQ/0.jpg)](https://www.youtube.com/watch?v=HuqHnCAGWEQ)

* Faster for scenarios where a limited set of recent data is needed
* More scalable due to distributed nature of storage
* Provides a useful abstraction that decouples applications from each other
* Allows one set of data to satisfy many use-cases which may not have been predictable when the dataset was originally created
* Built-in ability to replay events and observe exactly what occurred, and in what order, provides more opportunities to recover from error states or dig into how a particular result was arrived at

## Review: Stream Processing

### QUESTION 1 OF 5

Which of the following is a stream processing solution? (may be more than one answer)

- [ ] A process which runs once a day and aggregates order data by regional market.

- [x] A process that sends a receipt to a customer as soon as it receives a purchase event

- [x] A process that calculates the total page visits in the last 15 minutes

- [x] A process that raises an alert if a certain number of error logs are produced by an application in the last 5 minutes

- [ ] A process that creates a summary of user activity of the last hour, every hour

### QUESTION 2 OF 5

Which of the following is a batch processing solution? (may be more than one answer)

- [x] A daily process which runs sentiment analysis on customer reviews

- [ ] An asynchronous process that performs fraud detection on customer transactions as they occur

- [ ] A process which keeps a running tally of all orders by department for a rolling window of the past 15 minutes

- [x] A process which pulls metrics from all microservices every 10 seconds and aggregate these metrics into a centralized view

- [ ] A process that calculates an aggregated view of metrics across microservices based on real-time events

### QUESTION 3 OF 5

What are the two components of every stream processing solution?

- [ ] Apache Kafka

- [x] Streaming Data Store

- [ ] Spark Structured Streaming

- [x] Stream Processing Application Framework

### QUESTION 4 OF 5

Which of the following is a benefit of stream processing? (may be more than one answer)

- [x] Faster for scenarios where a limited set of recent data is needed

- [ ] Runs on a scheduled basis

- [x] More scalable due to distributed nature of storage

- [ ] Work directly with SQL stores such as PostgreSQL, Redshift, and MySQL

- [x] Provides a useful abstraction that decouples applications from each other

- [ ] Typically has access to all historical data in summarized form for historical analysis

- [x] Allows one set of data to satisfy many use-cases which may not have been predictable when the dataset was originally created

- [x] The built-in ability to replay events and observe exactly what occurred in order provides more opportunities to recover from error states or dig into how a particular result was arrived at

### QUESTION 5 OF 5

- [ ] Which of the following scenarios are better suited to a traditional SQL Database? (may be more than one answer)

- [x] Performing a calculation across a full historical representation of a dataset

- [ ] Updating a calculation as soon as an event occurs in a system

- [x] Storing mutable data in its most up-to-date form

- [x] Running on-demand exploratory queries from business users

### Key concepts to remember about stream processing

* Stream processing applications consist of a stream data store and a stream processing application framework
* Stream processing solutions do not operate on a scheduled basis
* Stream processing solutions provide real-time insights based on event data
* Stream processing solutions are built around generic data events, allowing for flexibility in data processing and highly scalable applications
* Batch and stream processing solutions can coexist and feed into each other


