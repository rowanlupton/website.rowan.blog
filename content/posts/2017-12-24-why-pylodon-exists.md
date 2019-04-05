---
layout: post
title: "why pylodon exists"
date: 2017-12-24 01:59:47 000Z
categories:
draft: true
---

first off: mastodon is amazing and i'm so impressed by [@gargon](https://mastodon.social/@gargron)'s tenacity and brilliance in bringing it to life

that being said, the biggest weakness that i see with mastodon is how intertwined the frontend and backend are. it has what i understand to be an excellent API, but i wanted to be able to fire up a mastodon server and write my own frontend, without mastodon's one taking up space and resources.
so i decided to write my own.

pylodon is meant to be purely server, so that anybody can take it, toss it up on the internet, and write their own frontend client to contribute. or, because it uses the [ActivityPub C2S API](), they could take a different AP frontend client and hook it up to pylodon.

i see this as the beginning of [@sivy](https://toot.cafe/@sivy)'s vision of 'blogodon', the federated macro-blogging platform — once the S2S bit is written, it should be trivial to write a blogging interface that can work with it, or write a wordpress plugin, or modify ghost (if somebody does that, i want to know!).

ActivityPub is beautiful. you can do anything with it, and with pylodon, i aim to make your federated vision one step closer.