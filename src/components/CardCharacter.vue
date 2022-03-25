<template>
  <div class="col-6 col-md-4 col-lg-3 text-center">
    <div class="p-3 h-100 border">
      <img
        class="img-fluid rounded-circle"
        :src="characterData.image"
        :alt="characterData.name"
      >
      <h2 v-if="characterData.name">
        {{ characterData.name }}
      </h2>
      <h3 v-if="characterData.origin">
        {{ characterData.origin }}
      </h3>
      <h4 v-if="characterData.species">
        {{ characterData.species }}
      </h4>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardCharacter',
  props: {
    characterData: Object,
  },
};
</script>

<style lang="scss" scoped>
h2 {
  &::after {
    content: '';
    display: block;
    margin: .5rem auto;
    width: 50%;
    border-bottom: 2px solid black;
  }
}
</style>
