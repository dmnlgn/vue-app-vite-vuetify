<template>
  <div class="text-center">
    <v-dialog v-model="dialog">
      <v-card class="dialogCard">
        <v-card-title class="text-h5 grey lighten-2">
          Category: {{ selected }}
        </v-card-title>
        <v-card-text>
          {{ joke.value }}
        </v-card-text>
        <v-divider></v-divider>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" text @click="fetchJoke"> next joke </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import axios from "axios";
import "./Dialog.scss";

export default {
  name: "Dialog",
  props: ["visible", "category"],
  data: () => ({
    dialog: false,
    selected: "",
    joke: {},
  }),
  computed: {
    dialog: {
      get() {
        return this.visible;
      },
      set(value) {
        if (!value) {
          this.$emit("close");
        }
      },
    },
  },
  mounted() {
    this.selected = this.category;
  },
  updated() {
    this.selected = this.category;
    if (this.selected) {
      this.fetchJoke(this.selected);
    }
  },
  methods: {
    fetchJoke() {
      axios({
        method: "GET",
        url: `https://api.chucknorris.io/jokes/random?category=${this.selected}`,
      })
        .then((response) => {
          console.log(" response.data", response.data);
          this.joke = response.data;
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>
