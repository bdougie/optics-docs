---
title: Get Started
order: 0
---

# What is Apollo Optics?

Apollo Optics is a tool that provides usage and performance insights for your GraphQL API. While GraphQL lets you write any queries you want, Optics helps you to optimize them.

It is a cloud-based, software-as-a-service application that uses an open source agent to instrument your GraphQL servers.

You can use Apollo Optics to trace how your queries run, identify performance trends, understand how your API is used, and find the time to resolution, among other things.

# Get Started in minutes!

If you have a GraphQL server, it only takes a few minutes to instrument your schema and see your data in Optics. The quick directions below are for instrumenting a Node.js Express server. If you’re using a different server technology, check out the docs for [JavaScript]((https://github.com/apollostack/optics-agent-js/blob/master/README.md)) and [Ruby](https://github.com/apollostack/optics-agent-ruby/blob/master/README.md).

## 1. Install

Simple enough:

`npm install optics-agent --save`

## 2. Import

In the file which connects your GraphQL schema to your Express server, add an import at the top:

```
import OpticsAgent from 'optics-agent';
```

## 3. Instrument the schema, middleware and context

The Optics agent relies on a variety of data points, which are available at different stages in the execution cycle. Currently, you need to add code in three places.

First, wrap your GraphQL Schema object with `instrumentSchema`:

```
// Before: graphqlExpress({ schema: schema })
graphqlExpress((req) => {
  // other options...
  schema: OpticsAgent.instrumentSchema(schema)
})
```

Second, add the HTTP middleware _before_ your GraphQL middleware:

```
expressServer.use(OpticsAgent.middleware());
```

Third, add an opticsContext field to your GraphQL context:

```
graphqlExpress((req) => {
  // other options...
  context: {
    // other context fields...
    opticsContext: OpticsAgent.context(req),
  }
})
```

That’s all the code we have to add. You’re almost done!

## 4. Sign into Optics and set the API key

Go to optics.apollodata.com and create an endpoint to get an API key. Restart your server and pass your API key with an environment variable, like so:

`OPTICS_API_KEY=<my_key> npm start`

The agent will automatically pick it up from there. Now, open up GraphiQL, run a query, and in a few seconds you’ll see data starting to show up in your Optics dashboard. You’re all set up!
