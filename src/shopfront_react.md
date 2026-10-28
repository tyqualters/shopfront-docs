# Vender shopfront-react

## Overview

Vender shopfront-react is the frontend component using React, React-Router, and Vite.

## Technical Details

Since Vender is a multi-component service, the backend and frontend components are split. This ultimately means every link between the frontend and backend must be matched manually.

This project builds as a Single Page Application (SPA) using Client Side Rendering (CSR) implemented through React-Router.

React-Router was initially configured in Framework mode, but had to be changed to Data mode due to technical limitations with displaying different pages based on the URI. Furthermore, an `<AuthWrapper />` component had to be added because client-side navigation and server-side navigation had access discrepancies. This was not a security concern, but still was a User Experience (UX) / Quality of Service (QoS) concern that needed to be addressed.

Communication between the frontend and backend is handled through Cookies and the API.
