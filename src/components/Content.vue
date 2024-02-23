<template>
  <div class="container">
    <!-- <h1>Latest News</h1> -->
    <div v-if="loading" class="skeleton-loader">
      <loading-component />
    </div>
    <div v-else class="ada">
      <div class="wrapper">
        <div
          v-for="(articles, index) in articles.slice(0, 5)"
          :key="index"
          class="grid"
        >
          <a :href="articles.url" @click="saveReadArticle(articles)">
            <div class="cardnya">
              <div class="card-image">
                <img :src="articles.urlToImage" alt="" />
                <div class="card-overlay">
                  <div class="card-overlay-content">
                    <div class="card-overlay-body">
                      <div class="card-meta">
                        <a href="#0" class="meta-source"
                          ><b-icon-person-check /> {{ articles.source.name }}</a
                        >
                        <p class="meta-date">
                          <b-icon-calendar />
                          {{ formatDate(articles.publishedAt) }}
                        </p>
                      </div>

                      <h2>
                        <a :href="articles.url" class="card-title">{{
                          articles.title
                        }}</a>
                      </h2>
                      <p class="desc">{{ articles.description }}</p>

                      <div class="card-meta-author">
                        <a href="#0"><b-icon-people /> {{ articles.author }}</a>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </a>
          <!-- </b-skeleton-wrapper> -->
        </div>
      </div>
      <div class="wrapper2 mt-5">
        <div
          v-for="(articles, index) in articles.slice(5, 10)"
          :key="index"
          class="grid2"
        >
          <a :href="articles.url" @click="saveReadArticle(articles)">
            <!-- <b-skeleton-wrapper :loading="loading"> -->
            <div class="cardnya2">
              <div class="card-image2">
                <div class="card-image-img">
                  <img :src="articles.urlToImage"  />
                <div class="card-overlay2">
                  <div class="card-meta">
                    <p>
                      {{ articles.source.name }}
                    </p>
                    <p>
                      {{ formatDate(articles.publishedAt) }}
                    </p>
                  </div>

                  <div class="card-meta-author">
                    {{ articles.author }}
                  </div>
                </div>
              </div>

                <div class="card__body">
                  <a :href="articles.url" class="card-title">
                    <h3>
                      {{ articles.title }}
                    </h3>
                  </a>
                  <p class="desc2">{{ articles.description }}</p>
                </div>
              </div>
            </div>
          </a>
        </div>
        <!-- </b-skeleton-wrapper> -->
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import LoadingComponent from "./Loading.vue";
export default {
  name: "ContentComponent",
  components: {
    LoadingComponent,
  },

  data() {
    return {
      api_key: "0510c037ec8c44519c617f42edb34598",
      articles: [],
      errors: [],
      loading: true,
      readArticles: [],
    };
  },
  methods: {
    formatDate(dateString) {
      const options = {
        year: "numeric",
        weekday: "short",
        month: "long",
        day: "numeric",
        hour12: false,
        hour: "numeric",
        minute: "numeric",
      };
      return new Date(dateString)
        .toLocaleDateString("id-ID", options)
        .replace(/\bpukul\b/, "");
    },
    saveReadArticle(article) {
      const isArticleExists = this.readArticles.some(
        (a) => a.url === article.url
      );

      if (!isArticleExists) {
        const newArticle = {
          title: article.title,
          imageUrl: article.urlToImage,
          url: article.url,
        };

        const uniqueArticlesSet = new Set([...this.readArticles, newArticle]);

        this.readArticles = Array.from(uniqueArticlesSet);

        localStorage.setItem("readArticles", JSON.stringify(this.readArticles));
      }
    },
  },
  created() {
    this.loading = true;
    const storedReadArticles = localStorage.getItem("readArticles");
    if (storedReadArticles) {
      this.readArticles = JSON.parse(storedReadArticles);
    }
    axios
      .get(
        "https://newsapi.org/v2/top-headlines?country=us&apiKey=" +
          this.api_key
      )
      .then((response) => {
        this.articles = response.data.articles;
        this.loading = false;
      })
      .catch((e) => {
        this.errors.push(e);
        this.loading = false;
      });
  },
};
</script>

<style></style>
