<template>
  <div class="home" id="Home">
    <b-container class="mt-5">
      <b-row  class="">
        <b-col class="col-md-4 p-2" v-for="(hotel, i) in hoteles" :key="i">
          <b-card
            thumbnail
            fluid
            :title="hotel.name"
            :img-src="hotel.image"
            img-alt="Image"
            img-top
            tag="article"
            style="max-width: 30rem"
            class="mb-2"
          >
            <b-card-text>
              Ubicación: {{ hotel.ubication }}<br />
              Precio: {{ hotel.price }}<br />
              Correo: {{ hotel.email }}
            </b-card-text>

            <b-button v-on:click="verHotel(hotel.email)" href="#" variant="primary">Ver mas</b-button>
          </b-card>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
// @ is an alias to /src

import axios from "axios";

export default {
  name: "home",
  data() {
    return {
      hoteles: [],
    };
  },
  mounted() {
    axios
      .get("https://g3m3-e9-hoteles-api.herokuapp.com/hoteles/resumen")
      .then((response) => (this.hoteles = response.data));
  },
  methods: {
    verHotel: function (hotel) {
      this.$router.push({name: "user_profile", params:{ email: hotel }})
    }
  }
};
</script>
