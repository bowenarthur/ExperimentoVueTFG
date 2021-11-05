<template>
  <div>
    <h4>{{ titulo }}</h4>
    <table class="tabela" v-if="musicas && musicas.length > 0">
      <thead>
        <tr>
          <th>Musica</th>
          <th>Duração</th>
        </tr>
      </thead>
      <tbody v-for="musica in musicas" :key="musica._id">
        <tr v-on:click="removerMusica(musica.nome)">
          <td>{{ musica.nome }}</td>
          <td>{{ musica.duracao }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    musicas: [Object],
    titulo: String,
  },
  methods: {
    removerMusica(nome) {
      this.$emit("remover-musica", nome);
    },
  },
};
</script>