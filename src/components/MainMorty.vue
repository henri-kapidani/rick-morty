<template>
  <main class="py-4 bg-primary">
    <p class="text-center">
      Questo contatore triggera il rendering del solo componente MainMorty
      ogni secondo ma le computed properties non vengono ricalcolate
      se non quando cambia effettivamente una dipendenza della proprietà
    </p>
    <p class="pb-4 text-center h1">
      {{ contatoreInutile }}
    </p>
    <div class="container">
      <div v-if="arrCharacters == null">
        Dati in caricamento
      </div>
      <div
        v-else
        class="row g-3"
      >
        <card-character
          v-for="character in searchCharacter"
          :key="character.id"
          :character-data="character"
        />
      </div>
    </div>
  </main>
</template>

<script>
import CardCharacter from '@/components/CardCharacter.vue';
import axios from 'axios';

export default {
  name: 'MainMorty',
  components: {
    CardCharacter,
  },
  props: {
    stringaRicerca: String,
  },
  data() {
    return {
      baseUrl: 'https://rickandmortyapi.com/api',
      arrCharacters: null,
      contatoreInutile: 0,
    };
  },
  computed: {
    searchCharacter() {
      console.log('computed searchCharacter eseguito');
      // eslint-disable-next-line max-len
      return this.arrCharacters.filter((objCharacter) => objCharacter.name.toLowerCase().includes(this.stringaRicerca.toLowerCase()));
    },
  },
  created() {
    axios.get(`${this.baseUrl}/character`) // prendiamo 20 personaggi di Rick & Morty
      .then((response) => {
        this.arrCharacters = response.data.results.map((character) => ({
          name: character.name,
          origin: character.origin.name,
          species: character.species,
          image: character.image,
        }));
      })
      .then(() => axios.get('https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=1')) // generiamo un mazzo di carte
      .then((resMazzo) => axios.get(`https://deckofcardsapi.com/api/deck/${resMazzo.data.deck_id}/draw/?count=4`)) // estraiamo 4 carte e le aggiungiamo all'array dei personaggi
      .then((resCards) => {
        resCards.data.cards.forEach((card) => {
          this.arrCharacters.push({
            name: card.code,
            image: card.image,
          });
        });
      })
      .catch(() => {
        console.log('Errore');
      });
  },
  mounted() {
    setInterval(() => {
      this.contatoreInutile += 1;
    }, 1000);
  },
  methods: {
    // searchCharacter() {
    //   console.log('method searchCharacter eseguito');
    // eslint-disable-next-line max-len
    //   return this.arrCharacters.filter((objCharacter) => objCharacter.name.toLowerCase().includes(this.stringaRicerca.toLowerCase()));
    // },
  },
};
</script>

<style lang="scss" scoped>

</style>
