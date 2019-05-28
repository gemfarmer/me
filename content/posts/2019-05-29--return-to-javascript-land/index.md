---
title: My return to JavaScript
subTitle: Why I miss JS
cover: react.png
category: "code"
---

A few years ago I was caught in the SPA frenzy that took over the JS world. MVC frameworks like Angular and Backbone had solved all sorts of problems that had plagued front end developers for years. As a JS dev, fullstack JS made a lot of sense to me – and I had fun building SPA or SPA-like apps for a time.

This changed for me with the arrival of ES6 in 2015. Don't get me wrong, I really loved a lot of the improvements over ES5. The arrival of modules (and being able to abandon AMD loaders like RequireJS), class syntax, and the shift towards promises have been huge! But I didn't like the JS ecosystem at the time.

But in some ways it felt like the arrival of ES6 made apps a bit more complicated to maintain without adding much substance. Every application required a whole suite of `babel-` packages just to transpile your ES6 code to ES5. I found myself frequently reverting to ES5 in sections just to avoid unfixed transpiler bugs.

I was also becoming more annoyed with the ways that browser-side code was hijacking default browser functionality like routing and semantic HTML. Fancy Angular apps would fail if a user disabled JS. When they failed, they would often look like a poorly made 90s site, because all tenants of progressive enhancement had been thrown out the window in favor of a more app-like feel.

### Enter Web Components and Custom Elements

HTML was created to excel at being a web document, not a web application. The promise of web frameworks like Angular was a shift towards componentization of the web. Some components have existed for awhile. `input`, `button`, etc. encapsulate a lot of advanced functionality and allow developers to build sites semantically. But modern apps require so many more components than the W3C have vetted. What if I want an accordian list?

In Angular v1 you could use custom directives to create an app-specific component to address this.

Attribute directives like `accordian-list` below were amazing because they allowed you to piggyback on an existing HTML element and insert more complex functionality.
```html

<div accordian-list></div>
```

This solution was portable between Angular apps, but what happened when the web shifted to Angular v2? Or what if an app didn't use Angular at all?

I began experimenting with [Custom Elements](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_custom_elements), the HTML5-native web component solution.

You could now use native JS to create custom elements as JS classes (or use ES5-era prototypical inheritance).
```js

customElements.define('accordian-list', AccordianList);

...

class AccordianList extends HTMLElement {
  constructor() {
    super();

    // Element functionality written in here

    ...
  }
}

...

document.createElement("accordian-list")
```

#### What about React??
Custom Elements weren't really catching on in the way I was hoping for. Instead, the JS dev world seemed more interested in library solutions like React and Polymer.

Despite fully embracing Custom Elements, I was weirdly resistant to React. Possibly because tutorials and ToDo MVP examples made it seem to easy. It couldn't be _that easy_, could it?

So, I decided to take a brief haitus from JS and dive into Ruby more fully.

### How I felt about Ruby in 2016

I had worked with Rails before, but I hadn't really had much interest in exploring it fully. In fact, two of my recent projects were migration projects – Rails to Node.js. Compared to the JS community, the Rails community felt outdated and stale. As a framework, Rails often felt overly-opinionated. `rails new` generated a fairly fleshed out application compared to express or koa. Also the "convention over configuration" paradigm bothered me. What if I didn't want to structure my application that way? Ironically, my favorite MVC framework was Angular, which followed a similar doctrine.

But I was ready for a change.

### Sprowt Labs on Rails

For the last two years I have been working on a set of Rails application for Sprowt Labs. Coupled with an (unnamed) IoT PaaS company, the apps form the backbone of the company's IoT infrastructure, directly interacting with companies and a fleet of devices in the field.

Despite having more experience with Node and JS frameworks at the time, I chose to use Rails for a few reasons:

1. **My coding time would be limited.** The JS ecosystem was moving too fast for my confort. The more compelling technologies like React were too bleeding edge to rely on and many of the year old technologies were being abandoned for React and other shiny things.
1. **Rails is robust.** Whatever beef you have with Rails, you cannot deny that it is full-service. There truly is a gem for most things, and many of them are well-tested and battle-worn.
1. **A lot of people know Rails.** The JS world was (and still is) quite splintered compared ot the Ruby world. Sure, some rubyists use Sinatra or write plain scripts, but most use Rails. If Sprowt needed to hire more engineers, we likely could find someone in our area.

#### Upsides, in practice
1. **There has been a gem for almost anything.** I've only had to make one gem to supplement our app needs, and even then I was able to piggy-back on an existing gem.
1. **I've been able to solve most perfomance issues quickly.** Most of the issues that I've experienced – memory and throughput issues on Heroku, aren't internet firsts. I've been able to clear up most issues by more thoroughly reading docs or with a short searches on stackoverflow.


#### Downsides, in practice
Rails performance isn't an issue you should be worrying about according to [DHH, co-creator of Rails](https://dhh.dk/). To paraphrase:
  > "Do you even have 400 requests a second? No? - Then who cares? Yes? - Buy another CPU. Hardware is cheap, programmer time and suffering is expensive. If you really, really, really need performance later, worry about it then."
1. **Rails is syncronyous, and can't fully utilize subscibe events.** The problem here is that with our devices out in the field we sometimes do get **200+ requests a second** for hours on end. I've handled most of these surges with Redis and Sidekiq, but the basic pain point still remains. In the absence of subscribe events, I've had to deploy a host of web hooks. These work well, but are tedious, as failures can lead to duplicate events.
1. **SQL has been annoying with a constantly changing schema.** I like Postgres. I prefer SQL databases. But our project has been constantly evolving and I've been making waaay to many DB migrations as a result. It would be nice if Rails could more easily pair with NoSQL databases like MongoDB.

### How I feel about Ruby

I love writing ruby code. It is syntactically elegant. It is consistent and well thought out – I love that everything is an object, for instance.

Rails conventions keep your code sane. Conventions keep you writing down the road most travelled, which is a good thing most of the time.

The Ruby on Rails ecosystem is conservative, which is great for what it is. I'm glad it exists and I look forward to it steadily moving along, incrementally incorporating new best practices as they come along.

The nice thing about this kind of conservatism is that I know that I can put it on the backburner for a bit and I can pick back up pretty much where I left off. [Rails 6.0-rc1 was just released in April](https://weblog.rubyonrails.org/2019/4/24/Rails-6-0-rc1-released/), and will probably be fully fleshed out a year from now. And if I want to upgrade an app from Rails 5 --> Rails 6, doing so will likely be straightforward.

### Why I miss JS – and why I'm back

I shifted away from JS in part because of the library churn. But after taking a sojourn in ruby land, I miss the churn. The community moves quickly, and that's why it is fun – you have to keep up!

React has matured. Angular has progressed. Node.js has more fully supported frameworks for quickly scaling apps. npm and yarn are quite a bite more robust.

In general, it seems like the JS world has been shifting more towards tenants of progressive enhancement, with server-side rendering and a renewed emphasis on static sites, led by projects like [Gatsby](https://gastbyjs.org). The JS world is uniquely positioned to make full use of service workers to make more sites available offline.

I also miss making things move. While Node is certainly a force, the JS world is still frontend heavy. I miss it. I miss building interactivity.

#### What I'm playing around with now:
* [React + Firebase](https://github.com/gemfarmer/primary-draft-2020-firebase/)
* [Gatsby](https://github.com/gemfarmer/me)
