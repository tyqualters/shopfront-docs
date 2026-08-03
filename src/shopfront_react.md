# Vender shopfront-react

## Overview

Vender shopfront-react is the frontend side of Vender. It is built using React, Vite, and React-Router.

## Design

The design and UI/UX were carefully thought out and planned. One misplaced button can make an entire website look bad.

The layout was drawn by hand and then recreated and customized in Figma.

The design follows the standard 60-30-10 color rule and the 8-pt grid system.

There are many other considerations that went into the design, but those will not be documented here.

## Inconsistent Integration

As mentioned in the Vender shopfront documentation page, the frontend and backend are separate. Each React page must be added to both React-Router and the backend HTTP Controller.

This can create inconsistent navigation and page display when not carefully constructed. For example, `<Link href="/admin">Admin Page</Link>` may be on a page, but the /admin page is blocked by the backend. What can happen is the page displays when a user clicks on the link, but if the user refreshes the page, they get the HTTP 403 Forbidden page. This could be fixed by removing client side rendering and force a page load by replacing `<Link>` with `<a>`, but that is bad UX.

Instead, careful precautions are taken to avoid this as much as possible in the UI. Only if a user is suspected to have access, then React will show the link. The frontend and backend are separated, which means that this must be lazily processed from the REST API.

This is still not feasible all around, so data is intentionally duplicated to maintain at least some level of consistency with the backend. For instance, the authentication key is stored in an HTTP cookie, but a normal cookie holds the key expiration date and user ID. This can help avoid unnecessary processing.

