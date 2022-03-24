<template>
  <main>
    <div class="container">
      <div v-if="arrCharacters == null">Dati in caricamento</div>
      <div v-else class="row g-3">
        <card-character
          v-for="character in arrCharacters"
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
  data() {
    return {
      baseUrl: 'https://rickandmortyapi.com/api',
      arrCharacters: null,
    };
  },
  components: {
    CardCharacter,
  },
  created() {
    /* ************************************************************* */
    /* METODO VISTO A LEZIONE (FUNZIONA MA NON SI USA SCRIVERE COSì) */
    /* ************************************************************* */
    // prendiamo 20 personaggi di Rick & Morty
    axios.get(`${this.baseUrl}/character`)
      .then((response) => {
        this.arrCharacters = response.data.results.map((character) => ({
          name: character.name,
          origin: character.origin.name,
          species: character.species,
          image: character.image,
        }));
      })
      .then(() => {
        // generiamo un mazzo di carte
        axios.get('https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=1')
          .then((resMazzo) => {
            // estraiamo 4 carte e le aggiungiamo all'array dei personaggi
            axios.get(`https://deckofcardsapi.com/api/deck/${resMazzo.data.deck_id}/draw/?count=4`)
              .then((resCards) => {
                resCards.data.cards.forEach((card) => {
                  this.arrCharacters.push({
                    name: card.code,
                    image: card.image,
                  });
                });
              });
          });
      })
      .catch(() => {
        console.log('Errore');
      });
    /* *************************** */
    /* FINE METODO VISTO A LEZIONE */
    /* *************************** */

    /* *********************************************** */
    /* MODO MIGLIORE DI CONCATENARE LE RICHIESTE AXIOS */
    /* *********************************************** */
    // axios.get(`${this.baseUrl}/character`) // prendiamo 20 personaggi di Rick & Morty
    //   .then((response) => {
    //     this.arrCharacters = response.data.results.map((character) => ({
    //       name: character.name,
    //       origin: character.origin.name,
    //       species: character.species,
    //       image: character.image,
    //     }));
    //   })
    //   .then(() => axios.get('https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=1')) // generiamo un mazzo di carte
    //   .then((resMazzo) => axios.get(`https://deckofcardsapi.com/api/deck/${resMazzo.data.deck_id}/draw/?count=4`)) // estraiamo 4 carte e le aggiungiamo all'array dei personaggi
    //   .then((resCards) => {
    //     resCards.data.cards.forEach((card) => {
    //       this.arrCharacters.push({
    //         name: card.code,
    //         image: card.image,
    //       });
    //     });
    //   })
    //   .catch(() => {
    //     console.log('Errore');
    //   });
    /* **************************************************** */
    /* FINE MODO MIGLIORE DI CONCATENARE LE RICHIESTE AXIOS */
    /* **************************************************** */
  },
};
</script>

<style lang="scss" scoped>

</style>
