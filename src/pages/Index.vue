<template>
  <q-page
    style="
      background-image: url('https://www.igeeksblog.com/wp-content/uploads/2022/04/Ghost-Pokemon-gengar-iPhone-wallpaper-630x450.jpg');
    "
    class="flex flex-center"
  >
    <div class="column items-center">
      <h3>{{ name }}</h3>
      <q-img :src="url" width="230px" />
    </div>
    <div class="row justify-around full-width">
      <q-input
        rounded
        color="white"
        bg-color="purple"
        filled
        v-model="search"
        label="Search a Pokemon"
      />

      <q-btn
        color="purple"
        label="Search"
        @click="getPokemon"
        icon-right="fas fa-paw"
      />
    </div>

    <div class="absolute-bottom text-subtitle1 text-center">
      <p>&copy; By Tizy. All Rights Reserved.</p>
    </div>
  </q-page>
</template>

<script>
import api from "../services/api";
export default {
  name: "PageIndex",

  data() {
    return {
      name: "",
      url: "",
      search: "ditto",
    };
  },
  async beforeMount() {
    await this.getPokemon();
  },

  methods: {
    getPokemon() {
      api
        .get(`/pokemon/${this.search}/`)
        .then((response) => {
          console.log(response);
          this.name = response.data.name;
          this.url = response.data.sprites.other.dream_world.front_default;
          this.triggerPositive();
        })
        .catch((error) => {
          this.triggerNegative();
        });
    },

    triggerPositive() {
      this.$q.notify({
        type: "positive",
        position: "bottom",
        message: `Pokemon Found!`,
      });
    },

    triggerNegative() {
      this.$q.notify({
        type: "negative",
        position: "bottom",
        message: `Invalid Pokemon`,
      });
    },
  },
};
</script>
