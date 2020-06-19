<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">nuxt01</h1>
      <ul>
        <li v-for="(post,index) in Posts" :key="index">
          <a :href="post.path" :title="post.title">{{post.title}}</a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";

export default {
  components: {
    Logo
  },
  data() {
    return {
      Posts: [],
      q: ""
    };
  },
  async fetch() {
    const posts = await this.$content("post")
      .only(["title", "published", "excerpt", "path"])
      .sortBy("publishdate", "desc")
      .limit(5)
      .fetch();
    this.Posts = posts;
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
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
