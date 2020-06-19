<template>
  <div class="container">
    <h1>{{ page.title }}</h1>
    <!-- <p>Description: {{ page.description }}</p> -->
    <nuxt-content :document="page" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      categories: [],
      category: null,
      q: ""
    };
  },
  async asyncData({ $content, params, error }) {
    //const Events = await this.$content("events").fetch();

    const slug = params.slug || "index";
    //await this.$content("events").fetch();
    console.log("$content");
    console.log($content);
    console.log("params", params);
    console.log("slug", slug);
    const page = await $content("/post/" + slug)
      .fetch()
      .catch(err => {
        error({ statusCode: 404, message: "Page not found" });
      });
    console.log("page:", page);
    return {
      page
    };
  }
};
</script>
