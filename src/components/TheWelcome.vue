<template>
  <div>
    <b-breadcrumb :items="items"></b-breadcrumb>
    <b-button to="/form">Registro</b-button>
  </div>
</template>

<script>
import Vue from "vue";
export default Vue.extend({
  name: "inicio",
  data() {
    return {
      items: [
        {
          text: "Inicio",
          active: true,
        },
      ]
    };
  },
});
</script>

<style>
</style>