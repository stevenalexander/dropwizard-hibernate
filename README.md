# Dropwizard Hibernate

Sample project using [Dropwizard 7.1](http://dropwizard.io/) with [Hibernate](http://hibernate.org/).
Requires [Gradle](http://www.gradle.org/) to build.

Hibernate was quite easy to use and didn't require much additional code compared to JDBI. I like the fact that the DAO
doesn't need any inline SQL and it can be DB agnostic. Session and transaction management is handled by the UnitOfWork
annotation, which is both good and bad, as it will automatically create a session and transaction and rollback if an
exception occurs in the resource method. This however prevents you from committing anything to the DB in error scenarios
unless you explicitly call to the SessionFactory, which makes using WebApplicationException tricky.

Also using Flyway and H2 to create an in memory DB with test data for integration testing. Flyway solution can be
expanded to create a fully featured Database Migration process using any JBDC compatible Database you can connect to.

## Setup H2 DB

Creates an H2 DB populated with the migration scripts in src/main/resources/db/migration

```
gradle flywayMigrate -i
```

## Run

```
./go
```

## Test

```
gradle test --info
```