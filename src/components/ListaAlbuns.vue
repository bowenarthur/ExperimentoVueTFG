<template>
  <div>
    <h3>{{ titulo }}</h3>
    <div class="scrollmenu row dragscroll">
      <div v-for="album in albuns" :key="album._id">
        <Album
          :album="album"
          v-on:mostrar-detalhes="mostrarDetalhes"
          v-on:mostrar-form="mostrarForm"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Album from "./Album";
export default {
  props: {
    titulo: String,
    albuns: [Object],
  },
  components: {
    Album,
  },
  methods: {
    mostrarDetalhes(album) {
      this.$emit("mostrar-detalhes", album);
    },
    mostrarForm(album) {
      this.$emit("mostrar-form", album);
    },
  },
};
</script>