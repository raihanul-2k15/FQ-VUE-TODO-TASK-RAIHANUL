<template>
  <v-row justify="center">
    <v-col sm="12" md="6">
      <v-text-field
        v-model="newItem"
        placeholder="New To-Do Item"
        label="New Item"
      ></v-text-field>

      <v-btn v-on:click="addItem">
        <span>Add</span>
        <v-icon>mdi-plus</v-icon>
      </v-btn>
    </v-col>
  </v-row>
</template>

<script>
import { globalBus } from "../main";

export default {
  name: "AddItem",

  data: () => ({
    newItem: "",
  }),

  methods: {
    addItem() {
      if (this.newItem !== "") {
        globalBus.$emit("add-item", this.newItem);
        this.newItem = "";
      }
    },
  },
};
</script>

<style>
</style>