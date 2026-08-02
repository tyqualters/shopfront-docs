# Vender shopfront

## Overview

Vender shopfront is the backend service responsible for handling HTTP/S traffic, user authentication, and the RESTful API (CRUD) for functional communication between the User and Vender.

## Technical Details

- C++23 (Drogon Framework)
- MariaDB (Persistent Data)
- Redis (User Authentication)

## System Design Choices

*Nobody uses C++ for Web Dev, right?* Drogon Framework ("Drogon") is one of the fastest web frameworks on the market today. Rust has many great high performance options, and so does Go, *but does performance even matter?* Kind of.

I was designing this project with the mindset that I could have a million users tomorrow. Obviously being a beginner, I did not take every single consideration, but I had a very valid reasons for choosing Drogon:

1) I am most familiar with modern C++
2) Drogon has built-in concurrency (coroutines, threads)
3) Drogon has built-in database support (MySQL, PostgreSQL, Redis)

As long as the backend remains stateless, and it also serves the frontend, I can therefore maximize optimization and still scale horizontally (magnitudes cheaper than scaling vertically).

Now why did I choose MariaDB over PostgreSQL? Familiarity. There are definite pros/cons with each, but their differences are negligible here and having to learn the Postgres way would take much longer while I am actively working a full-time job and studying for certifications.

Redis is obvious here, with its data being stored in memory, thereby being incredibly quick to access; it saves a lot of database traffic.

## Security Concerns

There are a lot of potential security concerns:

- Encoding mismatches
- Supply chain attacks (big in 2026)
- CSRF/SSRF (token jacking)
- XSS
- Zero Days / Zero-Click RCEs
- SQL Injection (SQLi)
- Time of Check, Time of Use (TOCTOU) Race Conditions
- etc.

The Secure by Design principle helps mitigate most of these. For example, instead of directly making SQL calls, shopfront uses Drogon's Object Relational Mapping (ORM) thereby eliminating the possibility of SQLi.

TOCTOU is a system design problem, and must be mitigated by synchronization + queueing. 

Unfortunately, Zero Days and Supply Chain attacks cannot exactly be mitigated. SAST and SCA are feasible mitigating controls, and DAST and IAST can help uncover downstream vulnerabilities at runtime. Here, it mostly is an accepted risk. (Again, this is a portfolio project.)

TLSv1.2 and TLSv1.3 are implemented in OpenSSL.

## Performance/Scalability Concerns

As previously mentioned, Drogon has concurrency out of the box. It is fully capable of maximizing its current node's resources and still able to scale horizontally.

Drogon only currently supports HTTP/1.1. HTTP/2.0 support is in Beta, and HTTP/3.0 remains unsupported. This is not a security concern, but may affect compatibility and performance. As of the time of writing this, HTTP/1.1 is still widely supported and Drogon is still highly performant that the benefits of HTTP/2.0 are likely to be negligible.

## Deployment

Drogon uses Podman to build and deploy. Special accomodations have been added to support environment variables in the YAML configuration files.

