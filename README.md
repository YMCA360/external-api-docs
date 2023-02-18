Welcome to the YMCA360 Docs!

## Authentication

To make a successful request to our API we require the use of HTTP Basic Authentication, you must pass a valid email address and password combination as an authorization header for each request. The email and password combination can be found in your YMCA360 association dashboard.

When building a request using Basic Authentication, make sure you add the Authentication: Basic HTTP header with encoded credentials over HTTPS.

### API Host and Base URL

Production  `https://ymca360.org/api/external/v1`

Development `https://staging.ymca360.org/api/external/v1`

A well-formed request for the group class schedules would be: `https://ymca360.org/api/external/v1/schedules`

### Schedules

* [Group Class Schedules](docs/schedules.md) `GET /schedules`
