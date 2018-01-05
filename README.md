# GA-w04d05-lesson

# Serving Static Assets in Express + Middleware

### Objectives
1. Learn to serve static assets like HTML, CSS, JS files and images. (Yes JS files are static. They cause other things to change, but they themselves do not change.)
1. Understand what middleware is in Express

## Static Assets

A static asset is something that doesn't change. It's the opposite of a dynamic asset. The main point behind Express is to serve dynamic assets, but before we get fancy with EJS this afternoon, we are going to serve up some plain old HTML, CSS and images. One cool thing about this, is it allows us to host images ourselves, and not rely on others!

Even the most complex Express applications are going to need to serve static assets. We're always going to need CSS and images right! 

#### Where do they go?

Best practices is to store static assets in a folder in the root directory called `public`. 

Inside that folder we could have `css` and `images` folders, and possibly more. 

#### How do we send them using app.get()?

To do this we need to use something called **middleware**. 

## Middleware

Middleware is just some code that runs "in the middle" of every request. 

There's middleware for enabling CORS, middleware for checking if a user is logged in, and middleware for error handling. There is also middleware for pointing our express app to where our static assets live. 

Middleware isn't scary. It's added using the `app.use()` function. We pass to it the middleware we want 'used'. 

## Serving static assets

For serving static assests we use a middleware called `express.static`, which itself is a function, and takes an argument of what folder our static assets will be in. 

```js
app.use(express.static('public'))
```

#### CODE ALONG: Let's build an Express App from scratch again for practice and clarity: 

- make a folder and create a js file in it called server.js
- Then run npm init and install express.

```bash
mkdir static-assets
cd static-assets
touch server.js
npm init
npm install express
```

Now let's add our Express boilerplate: 

```js
const express = require('express'); 
const app = express();

app.listen(3000, () => {
    console.log("I am listening");
});
```

And add our Middleware!

```js
const express = require('express'); 
const app = express();

app.use(express.static('public'))

app.listen(3000, () => {
    console.log("I am listening");
});
```

Next we are going to add a public folder, and put a css and js folder in that. Then put HTML, CSS and JS file in there appropriate places. Let's also create an images folder and download a fun image or gif from the internet, and put that in there too. (You can do that using Finder)

&#x1F535; **Activity**

```bash
mkdir public
touch public/index.html
mkdir public/css
mkdir public/js
touch public/css/style.css
touch public/js/app.js
mkdir public/images

5 minutes, thumbs up when done
```

OK, now to test our middleware we can go to `localhost:3000/images/the-filename-of-your-image.jpg` and see if our middleware is working! 

Before we dive in there, let's install one more example of middleware, so we really feel like we get it. 

#### Another Middleware Example: Morgan

Morgan is a simple middleware for logging each HTTP request to the console. This can be super helpful for debugging and developing our apps! 

Express Static is just like an extention of Express, so we just need to do `app.use` to make it work. Morgan, however is a third party module, so we need to first install it within our express project:

```bash
npm install morgan
```

Then require it:

```js
  const morgan = require('morgan');
```

And tell our app to use it!

```js
 app.use(morgan('tiny'))
```

Morgan can take some parameters of what we want to log. Tiny logs a small amount of info, but pretty much everything I'd want to see, so we can go with that for now. 

OK! You are now using two kinds of middleware! No big deal right?

Here's [a list](https://expressjs.com/en/resources/middleware.html) of handy expressjs.com approved middleware!

## Let's Build something! 
Let's open up our other static files and do some good old fashion Front End Development in there! 

&#x1F535; **Activity**
```
* Add boilerplate HTML and add whatever you want!
* Style it in the CSS (you will have to link it to the HTML as usual)
* Add JS to make it interactive if you like! 
* BONUS: Add your 404 pages to the public folder and make them get sent when you hit a path that has no route or file! 
* Until end of Lesson 
```

<details>
<summary>Want a hint for the bonus? </summary>
<br>
    <code>app.get('*', ...</code> is a catch all for ALL paths.
</details>
  
<details>
<summary>Want another hint? </summary>
<br>
Here's how you can add a 404 status to the response, and send a file from your public folder that isn't specifically asked for: 
<code>
  res.status(404).sendFile('error.html', {root: 'public'});
</code>
</details>

<details>
<summary>Want another hint? </summary>
<br>
You are going to need to put that "catch all" route at the bottom! Express checks for routes that match from top to bottom. 
</details>
