# Contentful + Netlify + Nuxt.js

This is a very quick demo application that uses [Netlify](https://www.netlify.com/) and [Contentful](https://www.contentful.com/).

Web app itself built with [Nuxt.js](https://nuxtjs.org/) and [nuxt-contentful-starter](https://github.com/yliaho/nuxt-contentful-starter).

## Deployment to Netlify
Publish directiry: dist
Build command: nuxt generate

Need to have these env vars:
```
{
  "CTF_BLOG_ARTICLE_TYPE_ID": "blogArticle",

  "CTF_SPACE_ID": "ID",
  "CTF_CDA_ACCESS_TOKEN": "TOKEN"
}
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
