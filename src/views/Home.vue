<template>
  <div class="container">
    <figure class="image is-128x128 item-image">
      <img
        width="120px"
        src="@/assets/pokemon-logo.png"
        alt="Placeholder image"
      />
    </figure>
    <div class="">
      <div class="columns">
        <div class="field column">
          <div class="control">
            <input
              v-model="busca"
              class="input is-primary"
              type="text"
              placeholder="Buscar pokemon"
            />
          </div>
        </div>
        <div class="column">
          <button class="button is-primary is-block" @click="buscar">
            Buscar
          </button>
        </div>
      </div>

      <div class="columns is-desktop is-multiline">
        <div
          class="column is-one-third

"
          v-for="poke in filteredPokemons"
          :key="poke.url"
        >
          <Pokemon :pokemon="poke" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Pokemon from "@/components/Pokemon.vue";
import axios from "axios";

export default {
  name: "Home",
  components: {
    Pokemon,
  },
  created() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon/?limit=151&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      });
  },
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: "",
    };
  },
  computed: {},
  methods: {
    buscar() {
      this.filteredPokemons = this.pokemons;
      if (this.busca == "" || this.busca == "  ") {
        this.filteredPokemons = this.pfilteredPokemonsokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(
          (pokemon) => pokemon.name == this.busca
        );
      }
    },
  },
};
</script>
<style>
.item-image {
  margin-top: 2%;
}
</style>
