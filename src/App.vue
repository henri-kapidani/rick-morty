<template>
  <div id="app">
    <header-morty />
    <main-morty />
    <footer-morty />
  </div>
</template>

<script>
import HeaderMorty from '@/components/HeaderMorty.vue';
import MainMorty from '@/components/MainMorty.vue';
import FooterMorty from '@/components/FooterMorty.vue';

export default {
  name: 'App',
  components: {
    HeaderMorty,
    MainMorty,
    FooterMorty,
  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
</style>
