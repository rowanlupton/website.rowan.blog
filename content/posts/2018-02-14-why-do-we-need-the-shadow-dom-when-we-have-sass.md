---
layout: post
title: "Why do we need the Shadow DOM when we have SASS?"
date: 2018-02-14 17:31:16 000Z
categories:
draft: true
---

n.b. if you're not a web developer and aren't interested in being one, this post may not be for you. lmk if you want a follow-up that'll try to explain things accessibly!
# Ghost dominatrixes? Isn't this a little personal?
The Shadow DOM is a concept in web development. It basically lets you make little capsules inside a web page, that have their own separate [DOM](https://css-tricks.com/dom/) (Document Object Model).

### If that flew over your head:
The DOM is, basically, everything in a webpage. Shadow DOM is kind of like having a separate webpage inside your webpage (yo dawg), which has all of its own elements, styles, etc. I don't think I can really do an explanation justice in this post, but if there's interest, I can try to write a shadow DOM for non-developers post in a bit.

# Honey, you gotta cut back on the SASS.
[SASS](https://css-tricks.com/sass-style-guide/) (Syntactically Awesome Style Sheets) is a tool for writing more semantic [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) (Cascading Style Sheets). If you've ever made a simple webpage, you've probably worked with CSS. And, unlike anything in CSS itself, it's outside the _scope_ of this piece.

# So what do they have to do with each other?
Honestly: I'm still trying to figure that out.

One of the biggest arguments for the Shadow DOM, CSS-in-JS, and a bunch of other things is that it solves the global scoping problem. That is, if you style your element `<div id="thing">`^[this is, of course, a bad idea to begin with! descriptive names, y'all]
```language-css
#thing {
    color: red;
    display: none;
}
```

for some reason, and then later somebody comes along and writes a new bit of the page (or if you forget) and it's about a different thing, but they make `<p id="thing">`, suddenly it's not gonna display, and everyone's going to be sad.

The first lesson here, unrelated to DOM black magic, is that you should ALWAYS NAME YOUR IDS DESCRIPTIVELY.

## SASS

The second can take two forms. One, that I've used up until now, is that you should always be as descriptive as you can about _which_ element you're styling — instead of `#thing {}`, try `header>#thing-wrapper>#thing {}` to be sure that you're keeping the style in the scope of #thing-wrapper in the scope of header.
It's a little clumsy to write all of that out each time, so sass lets you do e.g.
```language-css
// style.scss
// apologies for the syntax highlighting being wonky

header {
    /* some styles for the header */

    #thing-wrapper {
        /* some styles for #thing-wrapper inside the <header> block */

        #thing {
            /* this will apply only to this particular #thing */
            color: red;
            display: none;
        }
    }
}
```

Ahh. That's much nicer. Combined with SASS's import statements, you can easily write modules for CSS, and wrap each of them so that they only affect the selector you mean to write them for. Or you can write some global styles, like what color links should be, and overwrite them later if necessary! Cascading. Sheets. Nice.

## Shadow DOM

Or, you might say, "I'm writing a module and I don't want it to inherit ANY STYLES from the rest of the page!". I guess I just answered my question there, in a way — if you're e.g. writing a brand plugin (like a Twitter embed box), you probably want to be sure that any style that the user wrote won't affect your branding.
This is currently done by an `<iframe>`, which is clunky and old and Bad™. Shadow DOM is a more elegant solution.

So that's the "I'm a big brand and I want to be sure that everybody who uses any of my content is stuck with how I want it to look" scenario. Why would you want to use Shadow DOM for a component of your own?

This is where I'm stuck. I don't see why I would want to cut off a module of my page from the overall styling of the rest of it, just so that I can do what I could with a
```language-css
// '_module.scss'

module {
    /* all of my styles for this module */
}
```
SASS module.

Basically my same questions apply to CSS-in-JS, fwiw.

# Wrap-up
So. Where I am:

![Screen-Shot-2018-02-14-at-11.54.56-AM](/content/images/2018/02/Screen-Shot-2018-02-14-at-11.54.56-AM.png)
* Shadow DOM is HELLA COOL. Like, I've been staring at the document where I tried it out for 5 minutes and I'm still overwhelmed by how heckin' cool it is!
* I hate the idea of serving essential content on my site that won't render at all if JavaScript is disabled. Especially in the wake of Meltdown/Spectre, there is almost certainly a jump in people who disable JS by default when browsing.
* I still don't understand why, if I'm not a Big Evil Brand, I would want to use Shadow DOM, apart from:
    * it's cutting edge
    * it's conceptually incredible

Please help. I want to understand.
