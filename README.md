# Introduction

This code sample demonstrates accessing a PostgresSQL database with Spring Boot.

# Pre-requisites

The application configuration assumes you have created a PostgresSQL database named `demo`.  The `application.yaml` file contains the following datasource configuration

```
spring:
  datasource:
    url: "jdbc:postgresql://127.0.0.1:15432/demo"
    username: postgres
    password: password
```

A quick way to setup a PostgresSQL database supports this configuration is by installing and running the Tanzu Starter Service generator `tss` that will setup Docker containers for the database and also the pgAdmin GUI.


# Compiling and running the application

The application requires Java 11 by default.  If you want to change this, for example to Java 8, edit the `java.version` property in the pom to `1.8`.

To compile and run the application, execute

```
./mvnw spring-boot:run
```

# Data and Domain Model

The Domain model is a `Quote` that has an `id`, `author` and a `quote` property.
The data model is defined using Flyway, see `resources/db/migration` for the table structure and for the default quotes added to the table.  A Spring Data JPA Repository is used to implement the data access layer of the application.

# Endpoints

The `MessageController` provides three endpoints

* `/` - Returns a random quote
* `/quotes` - Returns all quotes
* `/quotes/{id}` - Returns the quote for the given `id`

A few curl commands exercise the API.

```json
$ curl -s localhost:8080 | jq
{
  "id": 1,
  "quote": "Never, never, never give up",
  "author": "Winston Churchill"
}
```

The `quotes` endpoint:

```json
$ curl -s localhost:8080/quotes | jq
[
  {
    "id": 1,
    "quote": "Never, never, never give up",
    "author": "Winston Churchill"
  },
  {
    "id": 2,
    "quote": "While there's life, there's hope",
    "author": "Marcus Tullius Cicero"
  },
  {
    "id": 3,
    "quote": "Failure is success in progress",
    "author": "Anonymous"
  },
  {
    "id": 4,
    "quote": "Success demands singleness of purpose",
    "author": "Vincent Lombardi"
  },
  {
    "id": 5,
    "quote": "The shortest answer is doing",
    "author": "Lord Herbert"
  }
]
```

The `quotes\{id}` endpoint.

```json
$ curl -s localhost:8080/quotes/5 | jq
{
  "id": 5,
  "quote": "The shortest answer is doing",
  "author": "Lord Herbert"
}
```


