<template>
  <div>
    <b-breadcrumb :items="items"></b-breadcrumb>
    <p>Aquí va la lista</p>
  </div>
</template>

<script>
import Vue from "vue";
export default Vue.extend({
  name: "formulario",
  data() {
    return {
      items: [
        {
          text: "Comienzo",
          href: "/",
        },
        {
          text: "Formulario",
          href: "/form",
        },
        {
          text: "Listado",
          active: true,
        },
      ],
    };
  },
});
</script>

<style>
</style>