<template>
  <b-navbar toggleable="lg">
    <div class="container">
      <router-link to="/">
      <b-navbar-brand>
        <img src="/assets/img/newsin.png" alt="News" />
      </b-navbar-brand>
      </router-link>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <!-- <b-navbar-nav>
          <b-nav-item href="#">About</b-nav-item>
          <b-nav-item href="#" disabled>Disabled</b-nav-item>
        </b-navbar-nav> -->

        <!-- <b-navbar-nav class="ml-auto"> -->
          <div class="ml-auto">

            <router-link to="/history" class="btn btn-outline-dark history"><b-icon-book/></router-link>
            <router-link to="/search" class="btn btn-outline-dark search-atas"><b-icon-search/></router-link>
          </div>
        <!-- </b-navbar-nav> -->

      </b-collapse>
    </div>
  </b-navbar>
</template>

<script>
export default {
  name: "NavbarComponent",
};
</script>

<style>
.navbar-brand img {
  max-width: 65px;
}
.navbar-brand {
  min-height: 75px;
  max-height: 20vh;
}
.btn-outline-dark.history{
  margin-right: 10px;
}
</style>
