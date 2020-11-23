<template>
  <div id="pokemon">
    <div class="card">
      <div class="columns">
        <div class="card-image">
          <figure class="image is-128x128">
            <img :src="currentImg" alt="Placeholder image" />
          </figure>
        </div>

        <div class="card-content">
          <div class="media">
            <div class="media-content">
              <p class="title is-4">{{ pokemon.name | upper }}</p>
              <p class="subtitle is-6">{{ pokemonUnit.type }}</p>
            </div>
          </div>
          <div class="content">
            <button class="button " @click="mudarSprite">
              Mudar sprite
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Pokemons",
  props: {
    pokemon: Object,
  },
  created() {
    axios.get(this.pokemon.url).then((resp) => {
      this.pokemonUnit.type = resp.data.types[0].type.name;
      this.pokemonUnit.front = resp.data.sprites.front_default;
      this.pokemonUnit.back = resp.data.sprites.back_default;
      this.currentImg = this.pokemonUnit.front;
    });
  },
  filters: {
    upper(value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
  data() {
    return {
      isFront: true,
      currentImg: "",
      pokemonUnit: {
        type: "",
        front: "",
        back: "",
      },
    };
  },
  methods: {
    mudarSprite() {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemonUnit.back;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemonUnit.front;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#pokemon {
  margin-top: 2%;
}
</style>
