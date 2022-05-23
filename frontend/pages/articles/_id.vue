<template>
  <div>
    <div
      v-if="article.data.attributes.image.data"
      id="banner"
      class="uk-height-small uk-flex uk-flex-center uk-flex-middle uk-background-cover uk-light uk-padding"
      :data-src="api_url + article.data.attributes.image.data.attributes.url"
      uk-img
    >
      <h1>{{ article.data.attributes.title }}</h1>
    </div>

    <div class="uk-section">
      <div class="uk-container uk-container-small">
        <div v-if="article.data.attributes.content" id="editor" v-html="$md.render(article.data.attributes.content)"></div>
        <p v-if="article.data.publishedAt">
          {{ article.data.attributes.publishedAt }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import articleQuery from "~/apollo/queries/article/article";

export default {
  data() {
    return {
      article: {
        data: [],
      },
      api_url: process.env.strapiBaseUri,
    };
  },
  apollo: {
    article: {
      prefetch: true,
      query: articleQuery,
      variables() {
        return { id: parseInt(this.$route.params.id) };
      },
    },
  },
};
</script>
