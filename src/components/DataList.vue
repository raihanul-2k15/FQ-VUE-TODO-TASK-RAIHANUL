<template>
  <v-row justify="center">
    <v-col sm="12" md="6">
      <v-list flat>
        <v-list-item v-for="(item, index) in items" :key="index">
          <v-list-item-content>
            <v-list-item-title>{{ item }}</v-list-item-title>
          </v-list-item-content>
          <v-list-item-action v-if="editable">
            <v-btn v-on:click="deleteItem(index)">
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </v-list-item-action>
        </v-list-item>
      </v-list>
    </v-col>
  </v-row>
</template>

<script>
import { globalBus } from "../main";

export default {
  name: "DataList",
  data: () => ({}),
  methods: {
    deleteItem(i) {
      globalBus.$emit("delete-item", i);
    },
  },
  props: {
    items: {
      type: Array,
      required: true,
    },
    editable: {
      type: Boolean,
    },
  },
};
</script>

<style>
</style>