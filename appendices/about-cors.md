# About CORS

> **\[danger\] You may encounter a failure**
>
> Your world or images loaded from a site other than [Reeborg's World](http://reeborg.ca) may fail.

For security reasons, in some cases, browsers refuse to load some content under a [same-origin policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy). This is something I encountered when I attempted to dynamically load images or worlds hosted on outside sites.

The [Cross-Origin Resource Sharing \(CORS\)](https://enable-cors.org/) is a specification to allow loading resources across domain boundaries. In order for Reeborg's World to make use of this, I currently have to [use a third party server as a bridge](https://github.com/Rob--W/cors-anywhere/).  This is a service provided as a courtesy to the general public by Rob Wu, with no warranty that it will accept requests from sites like mine.

So far, based on my site's traffic, I suspect that the requests made to that server are simply lost in the noise. However, if the traffic picks up, it could happen that requests from my site would be blocked.

There are at least two solutions:

1. I pay to set up a special server to handle such requests. 
2. When you develop interesting worlds or images to use in worlds, you give me a copy so that I can host them on my current site and bypass the need for CORS.

Since the second solution is free, I will not look further into the first one until further notice.

