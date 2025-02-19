Welcome to the YMCA360 Docs!

## Authentication

To make a successful request to our API we require the use of HTTP Basic Authentication, you must pass a valid username and password combination as an authorization header for each request. The username and password combination will be provided by YMCA360.

When building a request using Basic Authentication, make sure you add the Authentication: Basic HTTP header with encoded credentials over HTTPS.

### API Host and Base URL

Production  `https://ymca360.org/api/external/v1`

Development `https://staging.ymca360.org/api/external/v1`

A well-formed request for the schedules would be: `https://ymca360.org/api/external/v1/schedules`

### Schedules

* [Schedules](docs/schedules.md) `GET /schedules`
