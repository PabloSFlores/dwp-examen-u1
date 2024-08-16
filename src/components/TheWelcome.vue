<template>
  <div>
    <b-breadcrumb :items="items"></b-breadcrumb>
    <b-button to="/form">Si jala el action</b-button>
  </div>
</template>

<script>
import Vue from "vue";
export default Vue.extend({
  name: "Comienzo",
  data() {
    return {
      items: [
        {
          text: "Comienzo",
          active: true,
        },
      ]
    };
  },
});
</script>

<style>
</style>