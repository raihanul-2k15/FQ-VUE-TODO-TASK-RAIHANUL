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
            <v-select
              v-model="currentSource"
              :items="sources"
              item-text="name"
              item-value="id"
              label="Data Source"
              single-line
            ></v-select>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  components: {},

  data: () => ({
    sources: [
      {
        id: 0,
        name: "To-Do List",
        editable: true,
        data: [],
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
    ],
    currentSource: 0,
  }),

  computed: () => ({}),
};
</script>
