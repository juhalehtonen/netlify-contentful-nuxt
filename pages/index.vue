<template>
  <section class="container">
    <article v-for="post in posts" :key="post.fields.articleTitle">
      <h3>{{post.fields.articleTitle}}</h3>
      <p>{{post.fields.articleBody}}</p>
    </article>
  </section>
</template>

<script>
import { createClient } from '~/plugins/contentful'
import Logo from '~/components/Logo.vue'

const client = createClient()

export default {
  components: {
    Logo
  },
  asyncData({ env }) {
    return Promise.all([
      client.getEntries({
        'content_type': env.CTF_BLOG_ARTICLE_TYPE_ID,
        order: '-sys.createdAt'
      })
    ]).then(([ posts ]) => {
      return {
        posts: posts.items
      }
    }).catch(console.error)
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
