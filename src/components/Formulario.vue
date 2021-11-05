<template>
  <form v-on:submit.prevent="submit">
    <h2>Cadastro de Álbum</h2>
    <div class="formulario">
      <div>
        <label for="nome">Nome: </label>
        <input type="text" name="nome" v-model="nome" required />
        <br />
        <label for="capa">URL da capa: </label>
        <input type="text" name="capa" v-model="capa" required />
        <br />
        <label for="categoria">Gênero: </label>
        <select name="categoria" v-model="categoria" required>
          <option
            v-for="categoria in categorias"
            :value="categoria"
            v-bind:key="categoria"
          >
            {{ categoria }}
          </option>
        </select>
        <br />
        <label for="artista">Artista: </label>
        <input type="text" name="artista" v-model="artista" required />
        <br />
        <label for="ano">Ano: </label>
        <input type="number" name="ano" v-model="ano" required />
        <br />
        <label for="gravadora">Gravadora: </label>
        <input type="text" name="gravadora" v-model="gravadora" required />
        <br />
      </div>
      <EdicaoMusicas
        :musicas="musicas"
        v-on:atualizar-musicas="atualizarMusicas"
      />
    </div>
    <input type="submit" class="botao-cadastrar" value="Enviar" />
  </form>
</template>

<script>
import { inserirAlbum, atualizarAlbum } from "../Servico";
import EdicaoMusicas from "./EdicaoMusicas";

export default {
  data: () => ({
    musicas: [],
    nome: "",
    capa: "",
    categoria: "",
    artista: "",
    ano: "",
    gravadora: "",
  }),
  props: {
    album: Object,
  },
  computed: {
    categorias: () => [
      "Eletrônica",
      "MPB",
      "Pop",
      "Rap",
      "Reggae",
      "Rock",
      "Samba",
      "Sertanejo",
    ],
  },
  components: {
    EdicaoMusicas,
  },
  methods: {
    submit() {
      let data = {
        nome: this.nome,
        capa: this.capa,
        categoria: this.categoria,
        artista: this.artista,
        ano: this.ano,
        gravadora: this.gravadora,
        musicas: this.musicas,
      };
      this.album._id
        ? atualizarAlbum(this.album._id, data)
        : inserirAlbum(data);
    },
    atualizarMusicas(musicas) {
      this.musicas = musicas;
    },
  },
  mounted() {
    if (this.album._id) {
      this.nome = this.album.nome;
      this.capa = this.album.capa;
      this.categoria = this.album.categoria;
      this.artista = this.album.artista;
      this.ano = this.album.ano;
      this.gravadora = this.album.gravadora;
      this.musicas = this.album.musicas;
    } else {
      this.categoria = this.categorias[0];
    }
  },
};
</script>