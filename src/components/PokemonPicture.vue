<template>
  <div class="pokemon-container">
    <img :src="imgSrc" class="hidden-pokemon" />
    <img v-if="showPokemon" :src="imgSrc" class="fade-out" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      pokeid: this.pokemonId,
    };
  },
  props: {
    pokemonId: {
      type: Number,
      require: true,
    },
    showPokemon: {
      type: Boolean,
      require: true,
      default: false,
    },
  },
  computed: {
    imgSrc() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${this.pokeid}.svg`;
    },
  },
};
</script>

<style scoped>
/* Pokemon Picture */
.pokemon-container {
  display: flex;
  justify-content: center;
}
img {
  height: auto;
  width: 200px;
  user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-drag: none;
  -webkit-user-select: none;
}
.hidden-pokemon {
  filter: brightness(0);
}
</style>
