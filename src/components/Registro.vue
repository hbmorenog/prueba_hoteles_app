<template>
  <b-container>
    <b-form class="myform mt-5" v-on:submit.prevent="submit">
      <b-form-group id="input-group-1" label-for="input-1">
        <b-form-input
          id="email"
          v-model="form.email"
          type="email"
          placeholder="Correo electronico"
          required
        ></b-form-input>
      </b-form-group>
      <b-form-group id="input-group-2" label-for="input-2">
        <b-form-input
          id="password"
          v-model="form.password"
          type="password"
          placeholder="Contraseña"
          required
        ></b-form-input>
      </b-form-group>
      <b-form-group id="input-group-3" label-for="input-3">
        <b-form-input
          id="username"
          v-model="form.name"
          type="text"
          placeholder="Nombre del hotel"
          required
        ></b-form-input>
      </b-form-group>
      <b-form-group id="input-group-4" label-for="input-4">
        <b-form-input
          id="ubication"
          v-model="form.ubication"
          type="text"
          placeholder="Ubicación del hotel"
          required
        ></b-form-input>
      </b-form-group>
      <b-form-group id="input-group-4" label-for="input-4">
        <b-form-input
          id="price"
          type="tel"
          v-model="form.price"
          placeholder="Precio estándar habitación"
          required
        ></b-form-input>
      </b-form-group>
      <b-form-group id="input-group-5" label-for="input-5">
        <b-form-input
          id="image"
          type="tel"
          v-model="form.image"
          placeholder="Pag web del hotel"
          required
        ></b-form-input>
      </b-form-group>
      <b-form-group id="input-group-6" label-for="input-6">
        <b-form-input
          id="description"
          type="text"
          v-model="form.description"
          placeholder="Descripción del hotel"
          required
        ></b-form-input>
      </b-form-group>
      <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>
  </b-container>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      form: {
        email: "",
        name: "",
        price: "",
        ubication: "",
        password: "",
      },
      show: true,
    };
  },
  methods: {
    submit: function () {
      axios
        .post(
          "https://g3m3-e9-hoteles-api.herokuapp.com/hotel/agregar",
          JSON.stringify(this.form)
        )
        .then((result) => {
          var profile = true;
          this.$router.push({name: "user_profile", params:{ email: this.form.email  }})
        })
        .catch((error) => {
          if (error.response.status == 400) {
            alert("El hotel ya existe", error.response.data);
            this.$router.push({ path: "/registro" });
          }
        });

       
      
    },
  },
};
</script>

<style scoped>
.myform {
  min-width: 500px;
  text-align: center;
  font-size: 2.5rem;
}
</style>
