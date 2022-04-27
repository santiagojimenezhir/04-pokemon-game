<template>
  <h1 v-if="!pokemon">Espere</h1>
  <div v-else>
    <h1>¿Quíen es este pokemón?</h1>
    <PokemonPicture :pokemon-id="pokemon.id" :showPokemon="showPokemon" />
    <PokemonOptions :pokemons="pokemonsArr" @selection="checkSelection" />

    <template v-if="showAnswer">
      <h3>{{ message }}</h3>
      <button @click="newGame">Nuevo juego</button>
    </template>
  </div>
</template>

<script>
import { defineAsyncComponent } from "vue";
import getPokemonOptions from "../helpers/getPokemonOptions";

export default {
  data() {
    return {
      pokemonsArr: [],
      pokemon: null,
      showPokemon: false,
      showAnswer: false,
      message: null,
    };
  },
  mounted() {
    this.mixPokemonArray();
  },
  methods: {
    async mixPokemonArray() {
      this.pokemonsArr = await getPokemonOptions();
      const rndInt = Math.floor(Math.random() * 4);
      this.pokemon = this.pokemonsArr[rndInt];
    },
    checkSelection(pokemonId) {
      this.showPokemon = true;
      this.showAnswer = true;

      if (this.pokemon.id == pokemonId) {
        this.message = `Perfecto le atinaste ${this.pokemon.name}`;
      } else {
        this.message = `Lo siento erraste :( ${this.pokemon.name}`;
      }
    },
    newGame() {
      this.showPokemon = false;
      this.showAnswer = false;
      this.pokemonsArr = [];
      this.pokemon = null;
      this.mixPokemonArray();
    },
  },
  components: {
    PokemonPicture: defineAsyncComponent(() =>
      import(
        /*webpackChunkName:"PokemonPage" */ "@/components/PokemonPicture.vue"
      )
    ),
    PokemonOptions: defineAsyncComponent(() =>
      import(
        /*webpackChunkName:"PokemonOptions" */ "@/components/PokemonOptions.vue"
      )
    ),
  },
};
</script>

<style></style>
