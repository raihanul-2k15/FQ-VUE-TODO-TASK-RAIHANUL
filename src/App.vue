<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>
    </v-app-bar>

    <v-main>
      <v-container>
        <v-row justify="center">
          <v-col sm="12" md="6">
            <h2>Dynamic App</h2>
            <small class="secondary--text"
              >Note: I'm not very experienced with Vue or CSS. I'm a React
              person :P so...</small
            >
            <v-select
              v-model="currentSource"
              :items="sourceItems"
              item-text="name"
              item-value="index"
              label="Data Source"
              single-line
            ></v-select>
          </v-col>
        </v-row>
        <data-list
          :items="sources[currentSource].data"
          :editable="sources[currentSource].editable"
        >
        </data-list>
        <add-item v-if="sources[currentSource].editable"></add-item>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import DataList from "./components/DataList";
import AddItem from "./components/AddItem";

import { globalBus } from "./main";

export default {
  name: "App",

  components: {
    "data-list": DataList,
    "add-item": AddItem,
  },

  data: () => ({
    sources: [
      {
        id: 0,
        name: "To-Do List",
        editable: true,
        data: ["Learn Vue", "Complete Task", "Submit Task"],
      },
      {
        id: 1,
        name: "Dummy Data",
        editable: false,
        data: [
          "Just some dummy data",
          "Some big text to display. Wooo!",
          "Well, it's a small one",
          "Another small",
        ],
      },
      {
        id: 2,
        name: "More Dummy Data",
        editable: false,
        data: ["Keyboard", "Mouse!", "Monitor", "CPU", "GPU", "Laptop"],
      },
    ],
    currentSource: 0,
  }),

  methods: {
    loadFromStorage() {
      const storageItems = localStorage.getItem("todo-list");
      try {
        const parsedData = JSON.parse(storageItems);
        if (!Array.isArray(parsedData)) {
          throw "nope!";
        }
        this.sources[0].data = parsedData;
      } catch (e) {
        localStorage.removeItem("todo-list");
      }
    },
    saveToStorage() {
      localStorage.setItem("todo-list", JSON.stringify(this.sources[0].data));
    },
  },

  computed: {
    sourceItems() {
      return this.sources.map((s, i) => ({ name: s.name, index: i }));
    },
  },

  created() {
    this.loadFromStorage();

    globalBus.$on("add-item", (item) => {
      this.sources[this.currentSource].data = [
        ...this.sources[this.currentSource].data,
        item,
      ];
      this.saveToStorage();
    });
    globalBus.$on("delete-item", (idx) => {
      this.sources[this.currentSource].data = this.sources[
        this.currentSource
      ].data.filter((item, i) => idx !== i);
      this.saveToStorage();
    });
  },
};
</script>
