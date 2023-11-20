<template>
  <div class="q-pa-lg flex flex-center">
    <q-pagination
      v-model="current"
      color="black"
      :max="10"
      :max-pages="6"
      :boundary-numbers="false"
      @click="PaginarPeliculas(this.current)"
    />
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

export default {
  name: "PeliculaPage",
  components: {
    // PeliculaFilter,
    ListarPerliculas,
  },
  data() {
    return {
      totalPaginas: localStorage.getItem("paginas"),
    };
  },
  setup() {
    return {
      current: ref(1),
    };
  },
  methods: {
    PaginarPeliculas(paginaActual) {
      ListarPerliculas.methods.getPeliculas(paginaActual);
    },
  },
};
</script>
