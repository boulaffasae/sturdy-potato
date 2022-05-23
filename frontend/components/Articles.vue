<template>
  <div>
    <div class="uk-child-width-1-2" uk-grid>
      <div>
        <router-link
          v-for="article in leftArticles"
          :to="{ name: 'articles-id', params: { id: article.id } }"
          class="uk-link-reset"
          :key="article.id"
        >
          <div class="uk-card uk-card-muted">
            <div v-if="article.attributes.image.data" class="uk-card-media-top">
              <img
                :src="api_url + article.attributes.image.data.attributes.url"
                alt=""
                height="100"
              />
            </div>
            <div class="uk-card-body">
              <p
                id="category"
                v-if="article.attributes.category.data"
                class="uk-text-uppercase"
              >
                {{ article.attributes.category.data.attributes.name }}
              </p>
              <p id="title" class="uk-text-large">
                {{ article.attributes.title }}
              </p>
            </div>
          </div>
        </router-link>
      </div>
      <div>
        <div class="uk-child-width-1-2@m uk-grid-match" uk-grid>
          <router-link
            v-for="article in rightArticles"
            :to="{ name: 'articles-id', params: { id: article.id } }"
            class="uk-link-reset"
            :key="article.id"
          >
            <div class="uk-card uk-card-muted">
              <div
                v-if="article.attributes.image.data"
                class="uk-card-media-top"
              >
                <img
                  :src="api_url + article.attributes.image.data.attributes.url"
                  alt=""
                  height="100"
                />
              </div>
              <div class="uk-card-body">
                <p
                  id="category"
                  v-if="article.attributes.category.data"
                  class="uk-text-uppercase"
                >
                  {{ article.attributes.category.data.attributes.name }}
                </p>
                <p id="title" class="uk-text-large">
                  {{ article.attributes.title }}
                </p>
              </div>
            </div>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      api_url: process.env.strapiBaseUri,
    };
  },
  props: {
    articles: Object,
  },
  computed: {
    leftArticlesCount() {
      return Math.ceil(this.articles.data.length / 5);
    },
    leftArticles() {
      return this.articles.data.slice(0, this.leftArticlesCount);
    },
    rightArticles() {
      return this.articles.data.slice(
        this.leftArticlesCount,
        this.articles.length
      );
    },
  },
};
</script>
