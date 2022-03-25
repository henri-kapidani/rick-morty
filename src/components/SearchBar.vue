<template>
  <form @submit.prevent="$emit('ricerca', strSeach)">
    <label for="search">
      <input
        id="search"
        v-model="strSeach"
        type="text"
        name="search"
      >
    </label>
    <button id="btn-search">
      Cerca
    </button>
    <button
      id="btn-clear"
      @click="strSeach = ''"
    >
      Cancella
    </button>
  </form>
</template>

<script>
export default {
  name: 'SearchBar',
  data() {
    return {
      strSeach: '',
    };
  },
};
</script>

<style>

</style>
