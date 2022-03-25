<template>
  <header class="text-center py-4">
    <h1>Rick and Morty App</h1>
    <font-awesome-icon
      icon="spinner"
      pulse
    />
    <p>
      Questo contatore triggera il rendering del solo componente HeaderMorty ogni due secondi
    </p>
    <p class="h1">
      {{ contatoreInutile }}
    </p>
    <search-bar @ricerca="rilanciaRicerca" />
  </header>
</template>

<script>
import SearchBar from '@/components/SearchBar.vue';

export default {
  name: 'HeaderMorty',
  components: {
    SearchBar,
  },
  data() {
    return {
      contatoreInutile: 0,
    };
  },
  mounted() {
    setInterval(() => {
      this.contatoreInutile += 1;
    }, 2000);
  },
  methods: {
    rilanciaRicerca(argomentoEvento) {
      this.$emit('ricerca-rilanciata', argomentoEvento);
    },
  },
};
</script>

<style lang="scss" scoped>

</style>
