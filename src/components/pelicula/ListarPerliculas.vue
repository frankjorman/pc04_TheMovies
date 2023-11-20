<template>
  <h6>Listado de peliculas</h6>
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
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 20px;
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
  mounted(paginaActual) {
    this.getPeliculas(paginaActual);
  },
  methods: {
    async getPeliculas(paginaActual) {
      var url = "https://api.themoviedb.org/3/discover/movie";

      const params = {
        api_key: "0d875707b106a6c6b453a0167a423d41",
        page: paginaActual,
      };

      await axios
        .get(url, { params })
        .then((response) => {
          this.peliculas = response.data.results;
          this.$forceUpdate();
          localStorage.setItem(
            "paginas",
            JSON.stringify(response.data.total_pages)
          );
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
