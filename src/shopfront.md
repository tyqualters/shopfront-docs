# Vender shopfront

## Overview

Vender shopfront is the backend service component that is built using C++23 and the Drogon Framework.

## Technical Details

Drogon is a C++20 Web Framework that supports HTTP/1.1, TLSv1.2/v1.3, Object Relational Mapping (ORM), Coroutines, and more.

This project only targets Ubuntu Linux for production deployment. Limiting platforms makes a project as big as this one a little more manageable for a single developer.

Unfortunately, despite Drogon being an amazing framework to use, there are still a lot of technical concerns to address.

First, configuration needs to be properly managed. Drogon only natively supports having a JSON or YAML configuration file to read from, and cannot use environment variables. To resolve this, manual implementation for environment variables had to be added.

Second, package management is always a huge headache in C++. Instead of adding vcpkg and Conan, or vendoring the packages directly, packages are simply fetched from their respective GitHub repositories.

Third, Drogon's documentation is a little less than ideal to use for beginners. Unfortunately here, as a single developer, I had to use Gemini and read through Drogon's source code to figure out how to correctly use its C++20 Coroutines in place of the standard callback implementations.

Fourth, the frontend and backend are split. Unlike Next.js which makes the difference seamless, the process of serving a React site with its own CSR had to be figured out. Luckily, it is not difficult. Simply duplicating the URL in the HTTP Controller and serving the same index file works just fine.

A Containerfile and compose.yaml file were added to build a container image for easy deployment. Some concerns still need to be addressed, such as with unique configuration, SSL certificates, and CMake package differences. (At this point in time, it is not recommended to use the container image just yet.) 

Secrets Scanning is configured directly through GitHub Actions. It is set up to prevent any leaked secrets from being pushed.

CI is also set up through GitHub Actions. The pipeline runs CodeQL &rarr; CMake CI &rarr; AWS ECS ❌. (At this point in time, CD and DAST still have not been fully added.)
