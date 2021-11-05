<template>
  <div>
    <h4>{{ album.nome }}</h4>
    <p>Artista: {{ album.artista }}</p>
    <p>Gênero: {{ album.categoria }}</p>
    <p>Ano: {{ album.ano }}</p>
    <p>Gravadora: {{ album.gravadora }}</p>
  </div>
  <ListaMusicas :musicas="album.musicas" titulo="Músicas" />
</template>

<script>
import ListaMusicas from "./ListaMusicas";

export default {
  props: {
    album: Object,
  },
  components: {
    ListaMusicas,
  },
};
</script>