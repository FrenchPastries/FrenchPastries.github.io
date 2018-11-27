# French Pastries

> Build your stack from the ground up, customized to your needs.

French Pastries is not yet another framework in JavaScript, it's a new way to develop servers and applications in a functional programming way. It's a complete stack, built from the ground up in Node.js, in which you can take whatever you want. And because it's functional and pure most of the time, you're free to use what you want, and change easily each part if you need it. But we ensure everything we do is compatible with everything else.

## Uncoupled by design

In French Pastries, we rely only and exclusively on functions. We are not using objects or prototypes most of the time, because we don't want to. We want pure functions, like in mathematics, and we rarely want anything else.

Each package of the French Pastries stack is a standalone package you can use with every other package API-compatible. And that's how you can rewrite what you want: because you only have to comply with the API, you can drop the package you dislike and use your own!

# The stack

Composed by many parts, the core packages are made of MilleFeuille, Assemble and GraphQL.

## MilleFeuille

MilleFeuille is the core part. The ground on which we build everything else. MilleFeuille is a server, taking a bunch of options as parameters, and a handler returning a response, and starts a server. This could seem redundant when thinking about the core HTTP package or express.js, but it is the functional base we need to build great abstractions.

## Assemble

Assemble is our second core package. While MilleFeuille let you create a server, Assemble is focused on routing, and only routing! It allows you to define your routes and all of your handlers in a friendly and easy way. Completely compatible with MilleFeuille, it generates a handler function you can give to the server!

## GraphQL

We are actively working to support GraphQL in French Pastries, and we hope to release it soon, including support of GraphiQL.

# Who use it?

[Wolfox](https://wolfox.studio) and [BetaDigitis](http://www.betadigitis.com/) are actively using and maintaining the stack. They use it successfully in production, and build everything they can with it. You can contact [Wolfox](mailto:contact@wolfox.co) if you want support.

# Interested to join us?

Join us on Slack! We opened a special [French Pastries Slack](https://join.slack.com/t/frenchpastries/shared_invite/enQtNDg4NTYwNjYzNzc4LTJmOTI4MDYyZGY5YzVkOWJlMzViZTEwNzQ2NjgyYzI1NzE2MDA0NDI1NWYyZDBhZmUzYjZkODA0YjMyMzY2ZmM)! Come to talk with us!