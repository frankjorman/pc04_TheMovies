<template>
  <q-card class="item-card">
    <q-card-section>
      <q-img
        :src="'https://image.tmdb.org/t/p/original' + pelicula.poster_path"
      ></q-img>
    </q-card-section>
    <q-card-section>
      <!-- <q-card-title>{{ pelicula.overview }}</q-card-title> -->
      <div class="text-h6 font-weight-bold">{{ pelicula.original_title }}</div>
      <div class="text-center">
        <q-btn
          color="primary"
          icon="star"
          label="Agregar Favoritos"
          @click="AgregarFavorito(pelicula.id)"
        />
      </div>
    </q-card-section>
  </q-card>
</template>
<style>
.item-card {
  width: 300px;
}

.item-card q-card-section {
  height: 100px;
  overflow: hidden;
}
</style>

<script>
import axios from "axios";
import { Notify } from "quasar";

export default {
  name: "PeliculaItem",
  props: {
    pelicula: {
      type: Object,
      required: true,
    },
  },
  methods: {
    AgregarFavorito(id) {
      const options = {
        method: "POST",
        url: "https://api.themoviedb.org/3/account/20708625/favorite",
        headers: {
          accept: "application/json",
          "content-type": "application/json",
          Authorization:
            "Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiJmYWEzOTE5YmM2MGNhMTAxZWZiMmY2MzFjOTEzMWMwOCIsInN1YiI6IjY1NTU2NzJlYWM0MTYxMDExZWY4NmE2MyIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.O9LY2kU5z439a8-7BLECkJzvw0Xv7jVb5FwB5bpYmkc",
        },
        data: { media_type: "movie", media_id: id, favorite: true },
      };

      axios
        .request(options)
        .then(function (response) {
          Notify.create({
            type: "positive",
            message: "Agregado exitosamente",
          });
          console.log(response.data);
        })
        .catch(function (error) {
          debugger;
          console.error(error);
        });
    },
  },
};
</script>
