---
layout: post
title: "What the shit is the Shadow DOM, anyway?"
date: 2018-02-15
categories:
draft: false
---

Shadow DOM: the next frontier in web development.

Or something. Or not.

Let's get y'all up to speed. To start with:
# What the shit is the DOM anyway?

It stands for Document Object Model. It's the result of all of the HTML and Javascript that renders a webpage, and it's what Javascript and CSS interact with.

Yikes. Let's back up a bit.

To start, we'll take a stupidly simple HTML file.
```language-markup
// index.html

<!DOCTYPE html>
<html>
    <head>
        <title>A Simple Webpage</title>
    </head>
    <body>
        <div class="full">
            <p>Hello world!</p>
            <p>Goodbye world!</p>
        </div>
        <div class="empty"></div>
    </body>
</html>
```

This file is rendered by your web browser to become the DOM. This is a tree of objects.
```
html
 | -> head
    | -> title
       | -> "A Simple Webpage"
 | -> body
    | -> div.full
      | -> p
         | -> "Hello world!"
      | -> p
         | -> "Goodbye world!"
    | -> div.empty
```

![Screen-Shot-2018-02-15-at-8.44.53-AM](/content/images/2018/02/Screen-Shot-2018-02-15-at-8.44.53-AM.png)

"But Rowan," you're saying, "what's the difference between that tree and the HTML file?"

We're going to make a few changes.

```language-markup
// index.html

<!DOCTYPE html>
<html>
    <head>
        <title>A Simple Webpage</title>
        <script defer src="script.js"></script>
    </head>
    <body>
        <div class="full">
            <p>Hello world!</p>
            <p>Goodbye world!</p>
        </div>
        <div class="empty"></div>
    </body>
</html>
```

```language-js
// script.js

document.querySelector('.full').innerHTML = '';
document.querySelector('.empty').innerHTML = '<p>surprise!</p>';
```

Now, the DOM looks like this:
```
html
 | -> head
    | -> title
       | -> "A Simple Webpage"
 | -> body
    | -> div.full
    | -> div.empty
       | -> p
          | -> "surprise!"
```
because the Javascript removed the content from our `.full` div and added text to our `.empty` one.

![A page that says just "surprise!"](/content/images/2018/02/Screen-Shot-2018-02-15-at-8.45.57-AM.png)
<small>Please ignore the `<script>` tag in there, I didn't want to fuss with separate files.</small>

The point of this was to illustrate: the DOM is the page _as it is rendered_, not as it is written in the HTML file.

The DOM is the page as it exists in the browser.

[You can read more about it here.](https://css-tricks.com/dom/)

# CSS
Cascading Style Sheets — the last of the holy trinity. If we had added a stylesheet to the simple webpage we made earlier, like so:
```language-css
.full {
    background-color: red;
}
p {
    color: blue;
}
```
the background color of "Hello world!" and "Goodbye world!" would have been red, and all of the text on the page would have been blue (regardless of which text it was).

![Webpage saying "surprise!" in blue](/content/images/2018/02/Screen-Shot-2018-02-15-at-8.56.27-AM.png)

This is important. Because we styled `<p>` elements to be blue, _every_ `<p>` element on the page is blue (unless styled otherwise).

This can be useful! It allows for consistency among elements on the page — for example, if you style
```language-css
// style.css

input[type='button'] {
    background-color: red;
    color: white;
    border-radius: 100%;
    overflow: hidden;
}
```
then every input with a button type on your website will have a red background, white text, and be a circle (or oval, more likely).

Cool.

But what if you want to have a section (or _module_) of your page that has a _different type_ of button?

One way to achieve this is by making files like these:
```language-markup
// index.html

<!DOCTYPE html>
<html>
    <head>
        <title>This page is styled!</title>
        <link rel="stylesheet" src="style.css" />
    </head>
    <body>
        <input type="button" />
        <div id="module">
            <input type="button" />
        </div>
    </body>
</html>
```
```language-css
// style.css

input[type='button'] {
    background-color: red;
    color: white;
    border-radius: 100%;
    overflow: hidden;
}
#module>input[type='button'] {
    background-color: white;
    color: red;
    border-radius: 0;
    overflow: scroll;
}
```

![Two buttons on a page; one is a red circle.](/content/images/2018/02/Screen-Shot-2018-02-15-at-8.48.36-AM.png)
<small>Look at those cute li'l buttons. Cute as two buttons.</small>

This feels a little clunky, but at least it works. There are some ways you can make this better (e.g. SASS), and you could definitely be smarter (for example, if you gave _every_ button a class, you could have completely independent styles — at the cost, of course, that you would be deciding styling in the markup.)

We don't like style and markup mixing. Separation of concerns, and all that!

# Enter Shadow DOM
Imagine if you could, instead, prevent document styles from entering a part of your document. If the `input[type='button']` styling didn't creep into the `#module` div.

Well, now you can manage that!^[Well, you might have to use a polyfill (a bit of Javascript that replicates functionality that hasn't been implemented in the user's browser).]

Shadow DOM lets you create a new DOM, which exists inside the existing DOM. It's sort of like a snowglobe, or a closed terrarium. I don't like snowglobes, so we'll stick with the closed terrarium example.

![A spherical terrarium housing small succulents on a white computer desk](https://images.unsplash.com/photo-1496678518751-46244eef08c4?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=1080&fit=max&ixid=eyJhcHBfaWQiOjExNzczfQ&s=99e60e510a12cf3af8cc9b2cdf941871)
<small>Sort of like this, but without a big honkin' hole. | Photo by [Nielsen Ramon](https://unsplash.com/@nielsenramon?utm_source=ghost&utm_medium=referral&utm_campaign=api-credit) / [Unsplash](https://unsplash.com/?utm_source=ghost&utm_medium=referral&utm_campaign=api-credit)</small>

A closed terrarium is (almost) entirely self-sufficient. There's some stuff inside it, and that all makes up an ecosystem. If you put your terrarium in a rainforest, the terrarium wouldn't change from if it was in a desert, or the arctic. The analogy falls down a little bit because temperatures fluctuate.

The point remains, though: wherever you put your little Shadow DOM, it exists independently, by its own rules.

Instead of ecosystem, that means its lexical scope, styles, everything.

When you attach a Shadow DOM to an element, you're creating a little terrarium in your webpage.

```language-markup
// index.html

<!DOCTYPE html>
<html>
    <head>
        <title>This page has texture, and overhead lighting</title>
        <link rel="stylesheet" src="style.css" />
        <script defer src="script.js"></script>
    </head>
    <body>
        <input type="button" />
        <div id="terrarium"></div>
    </body>
</html>
```
```language-css
// style.css

input[type='button'] {
    background-color: red;
    color: white;
    border-radius: 100%;
    overflow: hidden;
}
```
```language-javascript
// script.js

terrarium = document.querySelector('#terrarium');

// set up the button to insert
let button = document.createElement("input");
button.type = 'button';

// attach a Shadow DOM. Ignore the mode for now.
terrarium.attachShadow({mode: 'open'})
         .appendChild(button);
```

Now we have two DOMs, each with their own button. If you create this on your own computer, you'll see something like this:
![Two buttons on a page; one is a red circle.](/content/images/2018/02/Screen-Shot-2018-02-15-at-8.31.21-AM.png)
<small>"Haven't we seen this before?" Check out the inspector!</small>

Starting from the top: you've got a round red button, and an unstyled basic button coming after it, without doing any fuckery in the markup and styling. That's pretty cool on its own.

Then we'll look at the Inspect view. You can see `#shadow-root (open)` inside of our `#terrarium` div.

There's the root of our Shadow DOM. Everything inside it (in this case, just the `<input type='button'>` element) exists outside the normal DOM.^[Well, sort of. You can apply styles to the Shadow DOM using outside CSS files, but it's much more idiomatic, and useful, to do it from inside, so that you can create a fully self-contained module.]

# Beyond Shadow DOM
![The Thunderdome, from Mad Max](/content/images/2018/02/thunderdome_flickr.jpg)
There's so much more! But not here, not today. If you want to get into the gory details, you'll want to look at things like [HTML imports](https://www.html5rocks.com/en/tutorials/webcomponents/imports/)^[Well, this is extrmely poorly supported across browsers at this point. You'll want to [use a polyfill](https://www.webcomponents.org/polyfills/).] and the [`:host` CSS selector](https://developers.google.com/web/fundamentals/web-components/shadowdom#styling) and really, just read [that whole page](https://developers.google.com/web/fundamentals/web-components/shadowdom).

It's cool stuff! [I'm still not convinced that it's broadly useful, but am coming around after writing this post.](https://blog.rowan.website/2018/02/14/why-do-we-need-the-shadow-dom-when-we-have-sass/) I just had to get over associating Shadow DOM with CSS in JS.
