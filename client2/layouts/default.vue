<template>
  <div>
    <Header />
    <nuxt class="router" />
    <Footer  />
  </div>
</template>
<style scoped>

.router{
   text-decoration: none;
  color: black;
}


</style>
<script>
import Header from "~/components/Header.vue";
import Footer from "~/components/Footer.vue";
export default {
  components: {
    Header,
    Footer
  }
};
</script>
