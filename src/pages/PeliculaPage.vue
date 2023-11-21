<template>
  <div class="q-pa-lg flex flex-center">
    <button @click="AgregarFavoritos()">click</button>
  </div>
  <div class="q-pa-lg flex flex-center">
    <div class="Pelicula-page">
      <!-- <div class="Pelicula-filter q-ml-md q-mr-xl">
      <PeliculaFilter />
    </div> -->
      <div class="Pelicula-list">
        <ListarPerliculas />
      </div>
    </div>
  </div>
</template>

<style>
.Pelicula-page {
  display: flex;
  justify-content: space-between;
}

.Pelicula-filter {
  width: 25%;
}

.Pelicula-list {
  width: 75%;
}
</style>

<script>
// import PeliculaFilter from "src/components/pelicula/PeliculaFilter.vue";
import { ref } from "vue";
import ListarPerliculas from "src/components/pelicula/ListarPerliculas.vue";
import axios from "axios";

export default {
  name: "PeliculaPage",
  components: {
    ListarPerliculas,
  },
  data() {
    return {};
  },
  setup() {
    return {
      current: ref(1),
    };
  },
  methods: {
    async AgregarFavoritos(pelicula) {
      const options = {
        method: "GET",
        url: "https://api.themoviedb.org/3/authentication/guest_session/new",
        headers: {
          accept: "application/json",
          Authorization: "Bearer 0d875707b106a6c6b453a0167a423d41",
        },
      };

      axios
        .request(options)
        .then(function (response) {
          console.log(response.data);
        })
        .catch(function (error) {
          console.error(error);
        });
    },
    IniciarSesion() {},
  },
};
</script>
