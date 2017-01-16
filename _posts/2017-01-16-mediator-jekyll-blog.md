---
layout: post
title: Updating Jekyll Formats
published: true
category: hack
tags: [hack, jekyll, mediator]
image: /assets/article_images/2017-01-16-mediator-jekyll-blog/typewriter_1920.jpg
---
_It's 2017; my site needed to stop looking so 2013._

# Thank you, Andrew
Three and a half years ago, my buddy who is into design, [Andrew](https://capshaw.me/), had a pretty swanky personal website. I thought it looked nice, so with his permission, I forked it, and pretty much took out his content and added my own.

![This is what swank looks like.](/assets/article_images/2017-01-16-mediator-jekyll-blog/old-jekyll-setup-1920.jpg)

At first I was proud of it, and tried to add content to it. I even wrote a post on [how to change the keyboard icon](/hack/customizing-mac-input-source-icon/) which still gets most of the traffic to this site.

![I don't know what sharebutton.to is, but robots like it.](/assets/article_images/2017-01-16-mediator-jekyll-blog/google-analytics.png)

Eventually, I lost interest and stopped paying attention to the site. Side projects that I had finished or abandoned were still featured front and center. Two and a half years after I graduated, [it still said I was a Senior in college](https://web.archive.org/web/20150525014515/http://saltesta.com/).

# Enter, Mediator
All the cool kids use the publishing platform, Medium, these days, or they were until Medium started getting a bit more flack for [laying-off a third of their company](https://www.bloomberg.com/view/articles/2017-01-05/why-medium-failed-to-disrupt-the-media). I don't know if it's still cool, but I'm hoping someone will tell me. Regardless, a few of my friends started exporting their work from the site and started looking for a new place to play ball. This made me wonder if it would be feasible to make something that looked as polished (cool) as Medium but hosted easily.

![This is what cool looks like.](/assets/article_images/2017-01-16-mediator-jekyll-blog/medium-screenshot-1920.jpg)

I was already using [Jekyll](https://jekyllrb.com/) (site building) on [GitHub Pages](https://pages.github.com/) (free hosting if you know how to use `git`) because that's what Andrew used; I wanted my site to look more like Medium because that's the new standard for what looks good; and I wanted to exert minimal effort because I've demonstrated to myself that I spend much time on this kind of thing (yet).

![It's the top two results!](/assets/article_images/2017-01-16-mediator-jekyll-blog/google-search-result.jpg)

The top results were [Mediator](https://github.com/dirkfabisch/mediator), and [a copy of Mediator](https://github.com/ageitgey/amplify) that used [Google's fancy new caching thing-a-ma-bob](https://www.ampproject.org/). I could do almost no work and use the first option, so we had a winner!

![This is what winners look like.](/assets/article_images/2017-01-16-mediator-jekyll-blog/df-screenshot.jpg)

# Mostly Seamless
For the most part, moving between Jekyll projects went off without a hitch. There were a few minor problems: the URL structure was different and I didn't want to make links to my site break (if they exist), and images in posts weren't centered by default. Five minutes of work later, one scare with CNAMES on GitHub pages, and I was all setup.

My knee-jerk reaction is that this is a pretty good configuration, and I hope it inspires me to write more posts this year.
