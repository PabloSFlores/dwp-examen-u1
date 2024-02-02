<template>
  <div>
    <b-breadcrumb :items="items"></b-breadcrumb>
    <b-form @submit="onSubmit" @reset="onReset">
      <b-row class="m-3">
        <b-col cols="12">
          <b-form-group label="Marca" label-for="marca">
            <b-form-input
              id="marca"
              v-model="carData.marca"
              :state="validate.marca"
              @input="validateField('marca')"
              type="text"
              placeholder="Nissan"
              trim
              required
            >
            </b-form-input>
            <b-form-invalid-feedback>
              {{ errors.marca }}
            </b-form-invalid-feedback>
          </b-form-group>
        </b-col>
        <b-col cols="12">
          <b-form-group label="Modelo" label-for="modelo">
            <b-form-input
              id="modelo"
              v-model="carData.modelo"
              :state="validate.modelo"
              @input="validateField('modelo')"
              type="text"
              placeholder="March"
              trim
              required
            >
            </b-form-input>
            <b-form-invalid-feedback>
              {{ errors.modelo }}
            </b-form-invalid-feedback>
          </b-form-group>
        </b-col>
        <b-col cols="12">
          <b-form-group
            label="Fecha de fabricación"
            label-for="fechaFabricacion"
          >
            <b-form-select
              v-model="carData.fechaFabricacion"
              :options="dateOptions"
              :state="validate.fechaFabricacion"
              @input="validateField('fechaFabricacion')"
            ></b-form-select>
            <b-form-invalid-feedback>
              {{ errors.fechaFabricacion }}
            </b-form-invalid-feedback>
          </b-form-group>
        </b-col>
        <b-col cols="12">
          <b-form-group label="Matrícula" label-for="matricula">
            <b-form-input
              id="matricula"
              v-model="carData.matricula"
              :state="validate.matricula"
              @input="validateField('matricula')"
              type="text"
              placeholder="XXXX000-00XX"
              trim
              required
            >
            </b-form-input>
            <b-form-invalid-feedback>
              {{ errors.matricula }}
            </b-form-invalid-feedback>
          </b-form-group>
        </b-col>
      </b-row>
      <b-button class="m-2" type="submit" variant="primary">Enviar</b-button>
      <b-button type="reset" variant="danger">Borrar</b-button>
    </b-form>
    <b-button to="/list">Ver listado de vehículos</b-button>
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
          text: "Inicio",
          href: "/",
        },
        {
          text: "Formulario",
          active: true,
        },
      ],
      dateOptions: [
        {
          value: null,
          text: "Selecciona una opción",
        },
      ],
      carData: {
        marca: "",
        modelo: null,
        fechaFabricacion: null,
        matricula: null,
      },
      errors: {},
      validate: {},
    };
  },
  methods: {
    getDateOptions() {
      var date = new Date();
      var year = date.getFullYear();
      for (var i = 1886; i <= year; i++) {
        this.dateOptions.push({
          value: i,
          text: i.toString(),
        });
      }
    },
    validateMandatory(field) {
      if (!this.carData[field]) {
        this.errors[field] = "Campo obligatorio";
        this.validate[field] = false;
      } else {
        this.errors[field] = "";
        this.validate[field] = true;
      }
    },
    validateMatricula() {
      const matriculaRe = /^[A-Z]{0,4}\d{3}-\d{2}[A-Z]{2}$/;
      console.log(matriculaRe.test(this.carData.matricula));
      if (!matriculaRe.test(this.carData.matricula)) {
        this.errors.matricula = "Formato no válido";
        this.validate.matricula = false;
      } else {
        this.errors.matricula = "";
        this.validate.matricula = true;
      }
    },
    validateMarca(){
        const formato = /^[A-Z]{1}[aA-zZ]{1,}/;
    },
    validateModelo(){
        const formato = /^[A-Z]{1}[aA-zZ]{1,}/;
    },
    validateFecha() {
        console.log(this.carData.fechaFabricacion);
    },
    validateField(field) {
      console.log();
      this.validateMandatory(field);
      if (field === "matricula" && this.validate["matricula"])
        this.validateMatricula();
      if (field === "fechaFabricacion" && this.validate["fechaFabricacion"])
        this.validateFecha();
    },
    onSubmit(event) {
      event.preventDefault();
      alert(JSON.stringify(this.carData));
    },
    onReset(event) {
      event.preventDefault();
      for (let field in this.carData) {
        this.carData[field] = null;
        this.errors[field] = "";
        this.validate[field] = null;
      }
    },
  },
  mounted() {
    for (let field in this.carData) {
      this.errors[field] = "";
      this.validate[field] = null;
    }
    this.getDateOptions();
  },
});
</script>

<style>
</style>