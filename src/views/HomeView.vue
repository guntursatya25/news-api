<template>
  <div class="app">
  <navbar-component />
  <content-component/>
  <footer-component/>
  </div>
</template>

<script>
  import NavbarComponent from '../components/Navbar.vue'
  import ContentComponent from '../components/Content.vue'
  import FooterComponent from '../components/Footer.vue'
  import '../assets/app.css'
  import '../assets/responsive.css'

  export default {
    name: 'HomeView',

    components: {
      NavbarComponent,
      ContentComponent,
      FooterComponent
    },
  }
</script>