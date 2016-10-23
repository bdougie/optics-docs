---
title: Troubleshooting
order: 0
---

The Optics agent is designed to allow your application to continue working, even if the agent is not configured properly.

## No data in Optics

If there is no data being sent to Optics, check your application logs to look for the following messages:

### Message: Please check the API key in the Optics agent configuration.

Solution: Get a valid API key from Optics and configure it in your GraphQL server.

### Message: no API key specified. Set the apiKey option or set the OPTICS_API_KEY environment variable

Solution: Check the API key provided for this endpoint in Optics, and set it in your GraphQL server configuration

### Message: schema not instrumented. Make sure instrumentSchema is called

Solution: In your server code, call instrumentSchema on the schema object you pass to the graphql function from graphql-js.
`OpticsAgent.instrumentSchema(executableSchema);`

### Message: Optics context not found. Make sure optics middleware is installed.

Solution: In your server code, set up the Optics middleware.
`app.use(OpticsAgent.middleware())`
