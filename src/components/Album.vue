<template>
  <div class="column">
    <div class="botoes">
      <a class="edit" v-on:click.prevent="mostrarForm"> &#9998; </a>
      <a class="delete" v-on:click.prevent="deleteAlbum"> &#128465; </a>
    </div>
    <div class="card" v-on:click="mostrarDetalhes">
      <img alt="" :src="album.capa" />
      <p>{{ album.nome }}</p>
    </div>
  </div>
</template>

<script>
import { excluirAlbum } from "../Servico";

export default {
  props: {
    album: Object,
  },
  methods: {
    mostrarForm() {
      this.$emit("mostrar-form", this.album);
    },
    mostrarDetalhes() {
      this.$emit("mostrar-detalhes", this.album);
    },
    deleteAlbum() {
      excluirAlbum(this.album._id);
    },
  },
};
</script>