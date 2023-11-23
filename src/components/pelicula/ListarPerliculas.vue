<template>
  <h6>Lista de Peliculas</h6>
  <div class="pelicula-list">
    <div class="pelicula-grid">
      <div
        class="pelicula-item"
        v-for="pelicula in peliculas"
        :key="pelicula.id"
      >
        <PeliculaItem :pelicula="pelicula" />
      </div>
    </div>
  </div>
</template>
<style>
.pelicula-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 30px;
}
</style>

<script>
import axios from "axios";

import PeliculaItem from "components/pelicula/PeliculaItem.vue";

export default {
  name: "ListarPeliculas",
  components: {
    PeliculaItem,
  },
  props: {
    ListarPeliculas: {
      type: Object,
      required: true,
    },
  },
  mounted() {
    this.getPeliculas();
  },
  methods: {
    async getPeliculas() {
      var url = "https://api.themoviedb.org/3/discover/movie";

      const params = {
        api_key: "3783ed24365ad7dc22d7f6f94f99843d",
        page: 15,
      };

      await axios
        .get(url, { params })
        .then((response) => {
          debugger;
          this.peliculas = response.data.results;
        })
        .catch((error) => {
          console.log("Error: " + error);
        });
    },
  },
  data() {
    return {
      peliculas: [],
    };
  },
};
</script>
