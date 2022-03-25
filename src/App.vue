<template>
  <div id="app">
    <header-morty @ricerca-rilanciata="setStrSearch" />
    <main-morty :stringa-ricerca="strSearch" />
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
  data() {
    return {
      strSearch: '',
    };
  },
  methods: {
    setStrSearch(argomentoEvento) {
      this.strSearch = argomentoEvento;
    },
  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
</style>
