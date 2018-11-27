# Getting Started

> Learn everyting needed to jump in right away

Let's get started simply with a server responding "Hello French Pastries!" for every request.

## Setting up the environment

Let's start by setting the environment. Let's go into a new folder, and get the packages.

```bash
mkdir hello-french-pastries
cd hello-french-pastries
yarn init --yes
yarn add @frenchpastries/millefeuille @frenchpastries/assemble
```

## Your first response

Now, you should have a single `package.json` in `hello-french-pastries` folder, and you're ready to launch your first server! Creates an `src/main.js` file, and paste the following content inside. (We start to use `src` folder to store all your files. That's a good convention we're always using.)

```javascript
const MilleFeuille = require('@frenchpastries/millefeuille')

const server = MilleFeuille.create(request => ({
  statusCode: 200,
  headers: {},
  body: 'Hello French Pastries!'
}))
```

In the few lines below, you're launching a server, and defining an unique handler, sending a "Hello French Pastries!" to every request. Launch the server typing `node src/main.js`, and try it in your browser: reach any address at [http://localhost:8080/](http://localhost:8080/) and see what's happening!

## Going a little further

Okay, we defined a good handler. But we can go further. What if we would define different responses according to URL? Yes, let's do it! So, let's rewrite the `src/main.js`

```javascript
const MilleFeuille = require('@frenchpastries/millefeuille')

const handler = request => {
  if (request.url.pathname === '/') {
    return {
      statusCode: 200,
      headers: {},
      body: 'Hello French Pastries!'
    }
  } else if (request.url.pathname === '/say-hello') {
    return {
      statusCode: 200,
      headers: {},
      body: 'Hello From Say Hello!'
    }
  } else {
    return {
      statusCode: 404,
      headers: {},
      body: 'Not Found'
    }
  }
}

const server = MilleFeuille.create(handler)
```

Once again, type `node src/main.js`, and try to reach [http://localhost:8080](http://localhost:8080), [http://localhost:8080/say-hello](http://localhost:8080/say-hello), and any `localhost:8080` URL, and see what's happening.

Okay, so what do we got? Three responses, different according to URL path, and an URL directly parsed by the server. That's cool, but we could do better.

## Improving responses

Looks like the return are really similar right? Yes, because that's exactly how MilleFeuille is built: the server accepts a function, which accepts a request, and returns a response, composed by three fields: `statusCode`, `headers` and `body`. The first one is the exact status code from HTTP which will be sent to client. The headers are the headers the client will receive, and the body is the content as string the client will receive. You can omit headers and body safely, but a forgot in statusCode will end up in a 500 internal error. And because these patterns are so regular, we defined helpers to simplify responses generation!

What we wrote can be simplified.

```javascript
const MilleFeuille = require('@frenchpastries/millefeuille')
const { response } = require('@frenchpastries/millefeuille/response')

const helloResponse = response('Hello French Pastries!')

const handler = request => {
  if (request.url.pathname === '/') {
    return helloResponse
  } else if (request.url.pathname === 'say-hello') {
    return helloResponse
  } else {
    return {
      statusCode: 404
    }
  }
}

const server = MilleFeuille.create(handler)
```

Yes, that's much better! We can go on now and doing better yet!

## Improving routes

Ok, so what we did below is really similar to routing, but, let's be honest, that's clearly not usable. Imagine having to check all routes like this? Well, no. Fortunately, we got a package for this! It is called `Assemble`. It let you define your routes in a functional way too, and is fully compatible with MilleFeuille. Let's dive in!

Happily we already got the assemble package, so we can use it right away! Let's modify a bit our previous file, and change our handler to improve our routes handling.

```javascript
const MilleFeuille = require('@frenchpastries/millefeuille')
const { response } = require('@frenchpastries/millefeuille/response')
const { get, notFound, ...Assemble } = require('@frenchpastries/assemble')

const helloResponse = response('Hello French Pastries!')

const handler = Assemble.routes([
  get('/', request => helloResponse),
  get('/say-hello', request => helloResponse),
  notFound(request => ({ statusCode: 404 }))
])

const server = MilleFeuille.create(handler)
```

Okay, that looks better right? More clear, more precise, and more dense. Less code and more maintainability. Now, as usual, try to launch the server (still `node src/main.js`), and play at `localhost:8080` address. Play with the code to understand what's happening. You shouldn't be too much confused.

What's happening here is that `Assemble.routes` is generating a handler function, accepting a request, and returning a response. Its role is to route request to the correct handler. That's why all our paths are accepting a handler too, exactly like MilleFeuille. So you can safely reuse the same code, and that's cool.

What we define here is simple: we say that for all our routes, if the request is a GET, and the url is either `/` or `/say-hello`, we returns a "Hello French Pastries!" response. In *all other cases*, we return we didn't found the page. *Because that's exactly what's happening.* If your user is asking for an URL which does not exist, then he should see a 404 error, and that's exactly what we do. And because the answer we give is freeform, we can customize the 404 page as much as we want!

We could, of course, complicate the example, but right now, let's stay simpler. We will elaborate on complexity later in the tutorial. Just remember you can easily handle POST, OPTIONS, DELETE, and even ANY requests you want with the correct functions in Assemble, and that you can catch variables in URL, with `:` in front of the path segment. But for all of this, [refer to the GitHub Assemble documentation](https://github.com/FrenchPastries/assemble) which details all of possibilities of the package.

## Conclusion

Let's conclude the getting started here. If you followed all of this from start to end, you're now able to build a server from scratch, getting the packages, setting up a routes handler, returning responses. That's only the start of the journey, because a lot of things is still needed to build an entire, fully working application server! But the first step is there, and you can already build what you want and add the packages you need.

But the journey is not over, and you can now continue to the next section, where you will learn how to build a complete application, from backend to frontend, and setting up a database!
