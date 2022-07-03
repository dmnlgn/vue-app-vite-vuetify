<template>
  <v-container class="container">
    <v-card class="containerCard">
      <v-card-actions class="justify-center">
        <v-btn color="primary" text @click="sortValueAsc"> sort by asc </v-btn>
        <v-btn color="primary" text @click="sortValueDesc">
          sort by desc
        </v-btn>
      </v-card-actions>
      <v-layout class="containerLayout">
        <v-col cols="7" class="containerCols">
          <div
            v-for="(element, index) in category"
            @click="selectedValue(element)"
            :key="index"
            class="subheading mx-3"
          >
            {{ element }}
          </div>
        </v-col>
      </v-layout>
    </v-card>
  </v-container>
  <Dialog
    :visible="showDialog"
    @close="showDialog = false"
    :category="selected"
  />
</template>

<script>
import axios from "axios";
import Dialog from "../components/Dialog.vue";

import "./BoxContainer.scss";

export default {
  name: "BoxContainer",
  data: () => ({
    category: [],
    selected: null,
    showDialog: false,
  }),
  methods: {
    selectedValue(event) {
      this.selected = event;
      this.showDialog = true;
      console.log(" this.selected", this.selected);
    },
    sortValueAsc() {
      this.category = this.category.sort();
    },
    sortValueDesc() {
      this.category = this.category.sort().reverse();
    },
  },
  mounted() {
    axios({
      method: "GET",
      url: "https://api.chucknorris.io/jokes/categories",
    })
      .then((response) => (this.category = response.data))
      .catch((err) => console.log(err));
  },
  components: { Dialog },
};
</script>
