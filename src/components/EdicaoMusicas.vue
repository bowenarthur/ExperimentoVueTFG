<template>
  <div class="edicao">
    <h3>Musicas</h3>
    <br />
    <label for="nome">Nome: </label>
    <input type="text" name="nome" v-model="nome" />
    <br />
    <label for="duracao">Duração: </label>
    <input type="text" name="duracao" v-model="duracao" />
    <button type="button" v-on:click="adicionarMusica">Adicionar</button>
    <ListaMusicas
      :musicas="musicas"
      v-on:remover-musica="removerMusica"
      titulo=""
    />
  </div>
</template>

<script>
import ListaMusicas from "./ListaMusicas";

export default {
  data() {
    return {
      nome: "",
      duracao: "",
    };
  },
  props: {
    musicas: [Object],
  },
  components: {
    ListaMusicas,
  },
  methods: {
    adicionarMusica() {
      if (this.nome.trim() != "" && this.duracao.trim() != "") {
        let musicas = this.musicas ?? [];
        musicas.push({ nome: this.nome, duracao: this.duracao });

        this.$emit("atualizar-musicas", musicas);

        this.nome = "";
        this.duracao = "";
      }
    },
    removerMusica(nome) {
      const musicas = this.musicas.filter((item) => item.nome !== nome);
      this.$emit("atualizar-musicas", musicas);
    },
  },
};
</script>