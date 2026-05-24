# bookmyshow-lld-java

A Spring Boot backend implementation of a BookMyShow-style movie ticket booking system. The project focuses on low-level design for theatres, auditoriums, movies, shows, seats, show seats, users, and ticket booking.

## Portfolio Role

This repository is maintained by Mamani Kedarnath as a Java low-level design portfolio project focused on seat booking workflows, domain modeling, and transaction-aware service design.

## Tech Stack

- Java 21
- Spring Boot 3.4
- Spring Web
- Spring Data JPA
- PostgreSQL
- Maven
- Lombok

## Features

- Manage cities, theatres, auditoriums, movies, shows, and seats
- Create users and book tickets
- Track show-level seat availability separately from physical seats
- Lock selected seats during booking
- Use serializable transactions for safer concurrent seat selection
- Model ticket status, show status, seat status, seat type, and auditorium features
- Keep code organized into controller, service, repository, model, configuration, and exception layers

## Design Overview

```text
Controller Layer
  UserController
  MovieController
  TicketController

Service Layer
  UserService
  MovieService
  TheatreService
  AuditoriumService
  ShowService
  SeatService
  ShowSeatService
  TicketService

Repository Layer
  UserRepository
  MovieRepository
  TheatreRepository
  AuditoriumRepository
  ShowRepository
  SeatRepository
  ShowSeatRepository
  TicketRepository

Domain Model
  City
  Theatre
  Auditorium
  Movie
  Show
  Seat
  ShowSeat
  User
  Ticket
  Payment
```

## Booking Flow

```text
User selects show seats
        |
TicketService checks availability
        |
Seats are locked in a SERIALIZABLE transaction
        |
Payment flow can be added
        |
Show seats are marked as BOOKED
        |
Ticket is saved
```

## Key Design Choice

The project separates `Seat` from `ShowSeat`. A physical seat belongs to an auditorium, while a show seat represents the state of that seat for a specific show. This keeps seat availability accurate across different show timings.

## How to Run

1. Create a PostgreSQL database named `demo`.
2. Update database credentials in `src/main/resources/application.properties`.
3. Start the application:

```bash
./mvnw spring-boot:run
```

On Windows:

```bash
mvnw.cmd spring-boot:run
```

## What This Project Demonstrates

- Low-level design for a high-concurrency booking domain
- Entity modeling for movies, theatres, auditoriums, shows, and tickets
- Transaction handling for seat locking
- Layered Spring Boot backend architecture
- Exception-driven handling for unavailable seats and missing domain objects

## Future Improvements

- Add payment success/failure handling
- Add seat lock expiry
- Add pricing calculation by seat type and show
- Add REST request/response DTOs for all write APIs
- Add integration tests for concurrent booking scenarios
- Add Swagger/OpenAPI documentation
