<template>
  <div>
    <navbar-component />
    <div class="container-search">
      <div class="search">
        <input
          v-model="searchTerm"
          type="text"
          class="searchTerm"
          placeholder="What are you looking for?"
        />
        <button @click="searchNews" type="submit" class="searchButton">
          Search
        </button>
      </div>
      <div v-if="searchResults.length > 0" class="container-searchResults">
        <div
          v-for="(result, index) in paginatedResults"
          :key="index"
          class="searchResult"
        >
          <div class="card__content">
            <div class="s-image">
              <img :src="result.urlToImage" />
            </div>
            <div class="content">
              <h2>{{ result.title }}</h2>
              <p>
                {{ result.description }}
              </p>
            </div>
          </div>
        </div>

        <!-- Pagination -->
        <div class="pagination">
          <button @click="prevPage" :disabled="currentPage === 1">
            Previous
          </button>
          <span>Page {{ currentPage }} of {{ totalPages }}</span>
          <button @click="nextPage" :disabled="currentPage === totalPages">
            Next
          </button>
        </div>
      </div>
      <div v-if="loading" class="loading-effect">
        <loading-search/>
        <loading-search class="mt-2"/>
        <loading-search class="mt-2"/>
        <loading-search class="mt-2"/>
        <loading-search class="mt-2"/>

        
      </div>
    </div>
  </div>
</template>

<script>
import NavbarComponent from "../components/Navbar.vue";
import LoadingSearch from "../components/LoadingSearch.vue";
import axios from "axios";

export default {
  name: "SearchView",
  components: {
    NavbarComponent,
    LoadingSearch
  },
  data() {
    return {
      searchTerm: "",
      searchResults: [],
      currentPage: 1,
      itemsPerPage: 5,
      loading: false,
    };
  },
  computed: {
    totalPages() {
      return Math.ceil(this.searchResults.length / this.itemsPerPage);
    },
    paginatedResults() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.searchResults.slice(startIndex, endIndex);
    },
  },
  methods: {
    searchNews() {
      this.loading = true;
      const apiKey = "0510c037ec8c44519c617f42edb34598"; // Ganti dengan API key News API Anda
      const endpoint = `https://newsapi.org/v2/everything?q=${this.searchTerm}&apiKey=${apiKey}`;
      this.searchResults = [];
      this.currentPage = 1;

      axios
        .get(endpoint)
        .then((response) => {
          this.searchResults = response.data.articles;
          this.currentPage = 1;
        })
        .catch((error) => {
          console.error("Error fetching search results:", error);
        })
        .finally(() => {
          this.loading = false;
        });
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
  },
};
</script>

<style>
.container-search {
  margin: 0 auto;
  max-width: 700px;
}
.search {
  width: 100%;
  position: relative;
  display: flex;
  height: 50px;
}

.searchTerm {
  width: 100%;
  border: 3px solid #f6f6f6;
  border-right: none;
  padding: 5px;
  height: 100%;
  background: #f2f2f2;
  border-radius: 5px 0 0 5px;
  outline: none;
  color: #000;
}

.searchTerm:hover {
  border: 3px solid #000;
}
.searchTerm:focus {
  color: #000;
}

.searchButton {
  display: flex;
  border: 1px solid #f6f6f6;
  background: #727f81;
  text-align: center;
  color: #fff;
  border-radius: 0 5px 5px 0;
  cursor: pointer;
  font-size: 20px;
  align-content: center;
  padding: 0 21px;
  justify-content: center;
  align-items: center;
}
.searchButton:hover {
  background: #ff2768;
}
.searchButton:active {
  background: #bc204f;
}
.searchResults {
  margin-top: 20px;
}
.card__content {
  display: flex;
  /* background: #f2f2f2; */
}
.card__content .content,
.card__content .s-image {
  width: 50%;
}
.card__content .content {
  padding: 0 1em;
}
.container-searchResults {
  margin-top: 20px;
  margin-bottom: 40px;
  /* border: 1px solid #ddd; */
  border-radius: 5px;
}

.searchResult {
  margin-top: 23px;
}
.searchResult:first-child {
  margin-top: 0;
}
.searchResult img {
  max-width: 100%;
  height: auto;
}

.searchResult a {
  color: #007bff;
  text-decoration: none;
}

.pagination {
  margin-top: 10px;
  display: flex;
  justify-content: space-between;
}

.pagination button {
  padding: 5px 10px;
  cursor: pointer;
}

.loading-effect {
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
</style>
