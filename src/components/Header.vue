<template>
  <div class="header">
    <h3 class="titulo-site">LISTA DE ÁLBUNS</h3>
    <ul class="menu-site">
      <li>
        <a v-on:click.prevent="mostrarForm"> CADASTRAR ÁLBUM </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  methods: {
    mostrarForm() {
      this.$emit("mostrar-form", {});
    },
  },
};
</script>