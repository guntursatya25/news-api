<template>
  <div class="history">
    <navbar-component />
    <div class="container-history">
      <h2 class="text-center">History</h2>
      <div v-if="historyArticles.length > 0">
        <div class="container-history-content mt-3">
          <div
            v-for="(article, index) in historyArticles"
            :key="index"
            class="content-history col-4"
          >
            <div class="history-image">
              <img :src="article.imageUrl" alt="History Image" />
            </div>
            <div class="history-detail">
              <h3>{{ article.title }}</h3>
            </div>
          </div>
        </div>
      </div>
      <div v-else class="no-data-history">
        <p class="text-center">No history found.</p>
      </div>
    </div>
  </div>
</template>

<script>
import NavbarComponent from "../components/Navbar.vue";

export default {
  name: "HistoryReadView",
  components: {
    NavbarComponent,
  },
  data() {
    return {
      historyArticles: [],
    };
  },
  mounted() {
    const storedHistoryArticles = localStorage.getItem("readArticles");
    if (storedHistoryArticles) {
      this.historyArticles = JSON.parse(storedHistoryArticles);
    }
  },
};
</script>

<style>
.no-data-history {
  display: flex;
  justify-content: center;
}
.container-history-content {
  display: flex;
  flex-wrap: wrap;
}
.container-history {
  margin: 0 auto;
  max-width: 800px;
  /* background: #F2F2F2; */
}
.history-image {
  width: 100%;
}
.history-image img {
  max-width: 100%;
  border-radius: 4px;
}
.history-detail {
  padding: 3px 5px;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}
.history-detail h3 {
  font-size: 13px !important;
}
</style>
