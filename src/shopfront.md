# Vender shopfront

## Overview

Vender shopfront is the backend system behind Vender. It uses Drogon (C++) to serve static files and implement a RESTful API (CRUD).

MariaDB was chosen for the backend database due to personal familiarity with MySQL.

Redis was chosen as the backend cache for authentication because it is versatile and volatile.

## Performance and Efficiency

Drogon uses C++20 Coroutines and multi-threading capabilities, making it incredibly fast and efficient. Since shopfront is also stateless, it can easily scale horizontally.

When it comes to scaling to millions of users, the real cause for concern would be the databases. Without proper sharding or master/slave replication, the Redis and MariaDB instances would only be able to scale vertically. Luckily there are serverless solutions to account for that if this were to be deployed as an actual service.

## Security and Compatibility

Unfortunately, HTTP/2.0 (beta) and HTTP/3.0 (not planned) are not currently supported in Drogon. HTTP/2.0 and HTTP/3.0 both bring significant performance and security improvements.

However, HTTP/1.1 is still widely supported and TLSv2/v3 are both implemented by OpenSSL.

Alongside Drogon, web application security is also important. Tokens are uniquely generated and expire automatically, and authentication cookies are HttpOnly and Secure. Communications with the main database use Drogon's Object Relational Mapping (ORM) library to prevent SQL injection and communications with the Redis database are carefully structured to prevent this as well.

## Routing and Implementation

For optimal development, React builds as a single page application.

**There are problems with this.**

There are many things wrong with this in production. For starters, it breaks SEO. No SEO = No Business.

Secondly, it denies the user the ability to navigate directly to a specific page via the URL.

**How is this fixed?**

To fix this, the frontend React-Vite project implements React-Router. Each page is specified in both the routes.ts file and the React HTTP Controller file. It's not pretty, but it gets the job done.

This gives the benefit of both client-side routing and multi-page applications.

**One more problem.**

The frontend and backend are separated. That means that data cannot be shared 1:1 like normal in a Next.js project.

**How is that fixed?**

It's not. There's no fix. That is just an unfortunate reality of development. To make them both work, a REST API must be used as optimally as possible, and data replication needs to exist between both the client and server side.

## Deployment

Deploying shopfront is possible with Docker or Podman. Environment variable support was added to the YAML/JSON files to allow for more straightforward deployment.

The Containerfile is configured to grab the frontend automatically from GitHub.

