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
  margin: 0 auto;
  width: 100%;
  max-width: 1000px;
}
article {
  margin-bottom: 20px;
}
</style>
