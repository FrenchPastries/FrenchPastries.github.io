# Getting Started

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
