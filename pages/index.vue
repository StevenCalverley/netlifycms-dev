<template>
  <div class="mx-auto container">
    <header>Blog Index</header>
    <section>
      <ul>
      <li v-for="post of posts" :key="post.slug">
        <NuxtLink :to="{ name: 'slug', params: { slug: post.slug } }">
          <div>
            <h2>{{ post.title }}</h2>
          </div>
        </NuxtLink>
      </li>
    </ul>
    </section>
  </div>
</template>

<script>
export default {
  head() {
    return {
      script: [{ src: 'https://identity.netlify.com/v1/netlify-identity-widget.js' }],
    };
  },
  async asyncData({ $content, params }) {
      const posts = await $content('blog', params.slug)
        .only(['title', 'description', 'slug', 'author'])
        .sortBy('createdAt', 'asc')
        .fetch()
      console.log(posts);
      return {
        posts
      }
    }
};
</script>

<style>
</style>
