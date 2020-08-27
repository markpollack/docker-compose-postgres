# Introduction

This code sample demonstrates accessing a PostgresSQL database with Spring Boot.

# Pre-requisites

The application configuration assumes you have created a PostgresSQL database named 'demo1'.  The `application.yaml` file contains the following datasource configuration

```
spring:
  datasource:
    url: "jdbc:postgresql://127.0.0.1:15432/demo1"
    username: postgres
    password: password
```

A quick way to setup a PostgresSQL database and pgAdmin GUI is by installing and running the Tanzu Starter Service generator `tss`.

```
tss generator install --go-getter-url=github.com/markpollack/generator-docker-compose-spring


# Data and Domain Model

The Domain model is a `Quote` that has an `id`, `author` and a `quote` property.
The data model is defined using Flyway, see `resources/db/migration` for the table structure and for the default quotes added to the table.  A Spring Data JPA Repository is used to implement the data access layer of the application.

# Endpoints

The `MessageController` provides three endpoints

* `/` - Returns a random quote
* `/quotes` - Returns all quotes
* `/quotes/{id}` - Returns the quote for the given `id`

# Running the application

Execute `./mvnw spring-boot:run` to compile and run the application.

A few curl commands exercise the UI.

```

```


