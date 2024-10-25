<div align="center">

[![ScyllaDB Unnoficial Discord Server](https://img.shields.io/badge/ScyllaDB_Developers-Discord_Server-4C388C)](https://discord.gg/8Preg7PfTY)

</div>

# Go Programming Assignment: ScyllaDB Rate Limiter Application

## Objective

The goal of this assignment is to create a Go command-line application that inserts random data into ScyllaDB while rate-limiting the number of requests. This exercise will help you understand how to interact with databases using Go, manage concurrency, and implement rate limiting.

## Task Description

You are required to develop a Go application that:

- **Data Insertion**: Inserts random data into ScyllaDB using the `gocql` driver.
- **Parallel Execution**: Performs queries in parallel with a customizable maximum parallelism.
- **Rate Limiting**: Implements rate limiting to control the number of requests per second.
- **Configurability**: Accepts command-line arguments to set:
    - `--parallelism N`: Specifies that N queries should be performed concurrently.
    - `--rate-limit M`: Specifies that at most M requests per second should be performed.
- **Metrics Reporting**: Periodically prints statistics, including the number of requests performed, average latencies, and the P99 latency metric.

## Requirements

- **Language**: Go (Golang)
- **Dependencies**:
    - Use only the standard library (`stdlib`), the `gocql` driver, and/or supplementary repositories (`golang.org/x/*`).
    - **gocql driver repository**: [https://github.com/scylladb/gocql](https://github.com/scylladb/gocql)

## Suggested Data Model

You may define your own data model, but here's a simplified example inspired by [Discord's data storage for messages](https://discord.com/blog/how-discord-stores-trillions-of-messages):

```cql
CREATE TABLE messages (
   channel_id bigint,
   bucket int,
   message_id bigint,
   author_id bigint,
   content text,
   PRIMARY KEY ((channel_id, bucket), message_id)
) WITH CLUSTERING ORDER BY (message_id DESC);
```

You can configure the cluster size and other keyspace-related settings as needed.
## Instructions

You can run ScyllaDB locally using Docker with the following command:

```
docker run --name scylla -d \
  -p 9042:9042 \
  -p 9160:9160 \
  scylladb/scylla:6.1.2
```

## Running the application

You should let us be able to run the app using the current command line arguments:
```
go run main.go --parallelism 50 --rate-limit 500
```


## Submission Guidelines

1. **Submit via Pull Request**: Create a Pull Request with your solution. Document your approach, any difficulties encountered, and how they were addressed.
2. **Documentation**: Update the README file to include a description of data types used and provide detailed instructions on how to run your application.
3. **Do Not Reference Other Solutions**: Avoid checking out other implementations until you have completed your submission.


## Additional Resources

To help you along the way, here are some useful resources:

- [🇺🇸 S101: ScyllaDB Essentials (with Certificate)](https://university.scylladb.com/courses/scylla-essentials-overview/)
- [🇺🇸 The 7 Database Paradigms](https://www.youtube.com/watch?v=W2Z7fbCLSTw)
- [🇺🇸 Exploring and Implementing the Leaky Bucket Rate Limiting Algorithm](https://www.rdiachenko.com/posts/arch/rate-limiting/leaky-bucket-algorithm/)
- [🇺🇸 Carnegie University - Intro to Database Systems](https://www.youtube.com/watch?v=otE2WvX3XdQ&list=PLSE8ODhjZXjYDBpQnSymaectKjxCy6BYq)

## Disclaimer

This assignment is for learning purposes and is not an official ScyllaDB test. If you find this exercise interesting, consider exploring career opportunities with us: [ScyllaDB Careers](https://www.scylladb.com/company/careers/).
