# Contentful + Netlify + Nuxt.js

This is a very quick demo application that uses [Netlify](https://www.netlify.com/) and [Contentful](https://www.contentful.com/).

Web app itself built with [Nuxt.js](https://nuxtjs.org/) and [nuxt-contentful-starter](https://github.com/yliaho/nuxt-contentful-starter).

## Deployment to Netlify

Use the following settings on Netlify:

```
Publish directory: dist
Build command: nuxt generate
```

Additionally, you need to set up the following environment variables:

```
  "CTF_BLOG_ARTICLE_TYPE_ID": "blogArticle",
  "CTF_SPACE_ID": "ID",
  "CTF_CDA_ACCESS_TOKEN": "TOKEN"
```

## Cool things about Netlify

- Super easy deploys via git, one-click rollbacks
- Auto-preview PRs or branches in unique preview URLs
- A/B split testing with multiple branches
- Free one-click HTTPS via LetsEncrypt
- Free custom domains
- Simple form submission collection and management
- Access management (password protection, role-based control)
- Free tier has access to a bunch of good things
- Use all kinds of static site generators (Gatsby very popular), custom build commands
- Snippet injection (e.g. Google Analytics) without touching source code
- Optional asset optimization with customization options (pretty permalinks, css, js, img)
- Deploy notifications


## Cool things about Contentful

- Official SDKs for JavaScript, PHP, .NET, Ruby, iOS, Android, Python, Java
- Very simple (ACF-like) content modeling and content input tool
- Translations and versions for content


## Using Netlify and Contentful together

- Need to set up webhooks in Contentful that get triggered when content changes, have Netlify listen for these (via `build hooks`) and rebuild site


## Useful links

- https://dev.to/milkstarz/contentful-and-netlify-the-dynamic-duo-of-static-site-management-55i
- https://www.netlify.com/docs/webhooks/
- https://www.contentful.com/developers/docs/javascript/tutorials/

## Build & Setup

``` bash
# install dependencies
$ npm install # Or yarn install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, checkout the [Nuxt.js docs](https://github.com/nuxt/nuxt.js).

# Findings after one day of experience

## Contentful

**Contentful** is a headless CMS that gives you simple tools to manage content creation and data modeling. More specifically, a headless CMS is a content management system that has an UI for managing content on the admin side, but is decoupled (or should I say beheaded) from the visual representation of the content.

### Pros of Contentful
- API-first design allows versatile use of content on any platform (e.g. mobile apps), not just your website
- Improved security by not having an admin panel coupled to your site and served under the same domain

### Cons of Contentful
- Needs more initial work to setup fetching of the content
- Can lead to each implementation working slightly differently
- More limited content type fields than what you'd get with relatively similar effort using WordPress + ACF
- Pricing options are quite steep, needs a serious business reason to go with Contentful

## Netlify

**Netlify** is an all-in-one hosting solution for static websites that takes care of everything from HTTPS, HTTP2, git-based deploys, domain management and everything else one could want for a static hosting solution.

They also offer an open source NetlifyCMS, a content management system that uses git under the hood to manage content. This wasn't tried out in this example repo, but can be a worthy idea to use when you don't need an API for your content.

### Pros of Netlify
- Free from the feeling of a vendor lock-in, simply build your site elsewhere and you're golden
- Extensive free tier: custom domains, single-click HTTPS, rollbacks, A/B testing, pull request previews...
- Global CDN, supposedly gives good performance worldwide (didn't test this independently yet)

### Cons of Netlify
- Limited number of supported languages (while multiple are available, one could wish to be able to use a specific tool or language)
- Only for static websites or web apps that don't need any kind of long-running processes or other features often associated with self-hosted solutions

## Using Netlify and Contentful together
Both services allow setting up webhooks, and it is webhooks that allows us to have the two communicate with each other.

By creating a `deploy hook` in Netlify, we obtain a specific URL which can be POSTed to to initiate a new build. We can then use this URL as the destination of an outgoing webhook in Contentful, which can be triggered by content-edit-actions of our choosing. 

As the content from Contentful gets fetched and inserted to our web app at build time, our content gets refreshed by the means of rebuilding the entire web app.

The downside of this approach is that the content edit is not instant, as we need to wait for Netlify to rebuild the app from scratch. Depending on the build workflow that you use, this can take a couple of minutes to finish.

## When would I use these tools?
By providing hosting, continuous delivery, HTTPS & HTTP2 out of the box, Netlify takes a lot of setup work out of setting up a simple site or a web app. While similar-ish setups can be achieved fairly easily with tools like Terraform and CircleCI, not having to manage or configure those separately can be a win in projects where you want to just focus on the code. 

Due to the pricing options, Contentful needs a more defined business case to be worthwhile. Aside from the free tier that requires attribution, the pricing options are not very hobby-friendly (ranging between 250 - 900 euros per month for businesses). The major advantage of a solution like this is having a high-availability content API that can be used on a variety of systems and that can be worked on independently from actual code.

As with any hosted service, there's a certain degree of marriage that you enter when you choose to use their proprietary tooling. Netlify doesn't really dictate how you build your site and moving to other solutions is quite simple (as you get to choose your build tools pretty freely), but Contentful definitely obtains a firmer grip of you. While they do offer a tool to produce a JSON dump of your data, that data would still need to be converted into a different format manually to use a different content hosting solution.

