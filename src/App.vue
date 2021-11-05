<template>
  <div class="app">
    <Header v-on:mostrar-form="mostrarForm" />
    <ListaAlbuns
      titulo="Últimos Álbuns"
      :albuns="albuns"
      v-on:mostrar-detalhes="mostrarDetalhes"
      v-on:mostrar-form="mostrarForm"
    />

    <ListaAlbuns
      titulo="Sertanejo"
      :albuns="sertanejo"
      v-on:mostrar-detalhes="mostrarDetalhes"
      v-on:mostrar-form="mostrarForm"
    />

    <div class="modal detalhes" v-if="openDetalhes">
      <a class="close" v-on:click.prevent="fecharDetalhes"> &times; </a>
      <Detalhes :album="album" />
    </div>

    <div class="modal" v-if="openForm">
      <a class="close" v-on:click.prevent="fecharForm"> &times; </a>
      <Formulario :album="album" />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header";
import ListaAlbuns from "./components/ListaAlbuns";
import Detalhes from "./components/Detalhes";
import Formulario from "./components/Formulario";
import { lerAlbuns } from "./Servico";

export default {
  name: "App",
  components: {
    Header,
    ListaAlbuns,
    Detalhes,
    Formulario,
  },
  data() {
    return {
      albuns: [],
      album: {},
      sertanejo: [],
      openDetalhes: false,
      openForm: false,
    };
  },
  methods: {
    fetchData() {
      lerAlbuns().then((res) => (this.albuns = res.data));
      lerAlbuns("Sertanejo").then((res) => (this.sertanejo = res.data));
    },
    mostrarDetalhes(album) {
      this.album = album;
      this.openDetalhes = true;
      this.openForm = false;
    },
    fecharDetalhes() {
      this.album = {};
      this.openDetalhes = false;
    },
    mostrarForm(album) {
      this.album = album;
      this.openForm = true;
      this.openDetalhes = false;
    },
    fecharForm() {
      this.album = {};
      this.openForm = false;
      this.fetchData();
    },
  },
  mounted() {
    const script = document.createElement("script");
    script.src =
      "https://cdnjs.cloudflare.com/ajax/libs/dragscroll/0.0.8/dragscroll.min.js";
    script.async = true;
    document.body.appendChild(script);
    this.fetchData();
  },
};
</script>

