# Vender shopfront (API)

## Overview

Vender's API is implemented through the backend service shopfront.

## Technical Details

| CRUD | Users | Shops | Products |
| :--- | :---: | :---: | :---: |
| **Create** | Y | Y | Y |
| **Read** | Y | Y | Y |
| **Update** | N | N | N |
| **Delete** | N | N | N |

Dev-only routes:

- `/api/list-users` List all users in the database
- `/api/list-shops` List all shops in the database
- `/api/list-products` List all products in the database
- `/api/sha256` Hash a message to SHA-256

Authenticated routes:

- `/api/whoami` Get user information
- `/api/register-shop` Create a new shop
- `/api/my-shops` List all shops owned by a user
- `/api/register-product` Create a new product

Unauthenticated routes:

- `/api/register` Create a new user
- `/api/login` Login as a user
- `/api/logout` Sign out of a user
- `/api/products` List shop products

Last updated: 10/28/2026