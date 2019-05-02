---
layout: post
title: "yet another explanation of Mastodon"
date: 2018-01-08
categories:
draft: false
image: "/images/cover_images/mastodon.jpg"
---

The situation: you've seen people talking about Mastodon. Maybe you're intrigued, maybe you're not. Either way, when they've tried to explain it to you, you've been confused, turned off, or maybe even a little angry that they won't shut up about it.

I'm going to try and undo some of that damage. This post is intended to start out with a non-technical general explanation and go from there to explain Mastodon in more and more detail. Don't feel obligated to read farther than you're interested to learn.
That being said, I've tried to keep from getting too far into the technical side (that'll come in a different post), so I think that it should be readable to anybody who's interested.

## basics of Mastodon
Mastodon is a microblogging^[blogging with a limited character number, to keep it short] service, similar in some ways to Twitter, but with some key differences:
1. it has a 500-character limit
2. it's not controlled by a for-profit company
3. anybody can run their own version of it, **and still talk to everyone else**

Point 3 gets at the bit that people tend to find confusing. Some simple comparisons that we can draw are email and telephones: your email might be from Apple, your employer, Protonmail or somebody else, and your telephone might be managed by O2, T-Mobile, or somebody else.
Behind the scenes, those services all *federate with*^[talk to] each other. Email does by looking up the *email domain*^[e.g. protonmail.com, the bit after the @ symbol] and then having that email service *route*^[send to the right place] from there to the addressee^[the bit before the @ symbol]. I don't know how telephones do it.

Mastodon also *federates*. Imagine if I could run a Twitter account on my own *domain*^[internet address, or url], example.com — I would then be known as @rowan@example.com, and you could follow me from your account on twitter.com.

So now, we're starting to envision a democratic system. Everybody has a choice about where to put their social presence, and can still follow their friends no matter where they are — same as you can visit any website from any internet service provider, web browser, location.^[unless your government blocks them]

Mastodon takes this utopian internet vision and puts it into practice. From my account on [toot.cafe](https://toot.cafe) I can follow my friend @ebeth on [witches.town](https://witches.town), or @shel on [cybre.space](https://cybre.space), or anybody else using Mastodon.

## communities
This leads into the next thing that makes Mastodon special: because anybody can create an *instance*^[a website that is Mastodon], and any user on that *instance* can follow anyone using Mastodon, you can have interest-specific Mastodon websites. To give a taste:
* [toot.cafe](https://toot.cafe): directed at web developers
* [mastodon.art](https://mastodon.art): as the name implies, a hub for artists. a few months ago there was a mass influx of comics people; a lot of them ended up here
* [social.coop](https://social.coop): run as a [platform cooperative](https://platform.coop/about). This is a great place for people who like to geek out about coops
* and thousands more! [instances.social](https://instances.social) and [joinmastodon.org](https://joinmastodon.org) exist to help you find what you're looking for.

Details of communities on Mastodon — and what they mean to me — are outside the scope of this post. If you're interested in learning about instances, why they build communities, and the ones that I'm on, check out my blog post [why I join Mastodon](https://blog.rowan.website/2017/12/23/why-i-join-mastodon/).

## step back: it's the fediverse
Except, wait! Mastodon doesn't only talk to Mastodon. The *federated social web*^[Mastodon is a part of this federation, as is any social website that *federates* with other social websites] has existed for years, with geeky things like [diaspora*](https://diasporafoundation.org/) and [identi.ca](https://identi.ca/) — not standard household names, by any means.
Mastodon is special in that it helped bring the *fediverse*^[federated social web] out of the shadows, and fostered a community that is excited about openness^[see recent hashtag #GetOnMyLawn] and sharing the *fediverse* with everyone, not just an artificially elevated "tech elite".

Since Mastodon started, there has been an explosion of excitement about the *fediverse*. [@puckipedia](https://puckipedia.com/) is writing [Kroeg](https://github.com/puckipedia/Kroeg), a group of people headed by [@BanjoFox](https://dev.glitch.social/@banjofox) are working on [Aardwolf](https://aardwolf.social/) (modeled off of a federated facebook), and even I am working on [pylodon](https://github.com/rowanlupton/pylodon) and its companion [smilodon](https://github.com/rowanlupton/smilodon), and there are many more *federated* projects.
Each of these will be able to *federate* with each other, contributing to a vision of a future where you can not only follow somebody on (heavy implicit metaphors ahead) Twitter from Twitter, but also from Facebook.

The *fediverse* imagines a future where there are no walls between social networks, blogs, and whatever springs up — you choose the one(s) that work(s) best for you, and just follow your friends. No thought required.

[This post is also published on Medium; if you enjoyed it, please consider clapping.](https://medium.com/@rowanlupton/yet-another-explanation-of-mastodon-8e40f9748788)