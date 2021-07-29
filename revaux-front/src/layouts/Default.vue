<script>
export default {
  data() {
    return {
      searchText: "",
    };
  },
};
</script>

<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title>
        <g-link to="/">{{ $static.metadata.siteName }}</g-link>
      </v-toolbar-title>
      <v-text-field
        placeholder="Search"
        class="ml-8"
        style="max-width: 350px"
        prepend-inner-icon="mdi-magnify"
        outlined
        v-model="searchText"
        rounded
        dense
        hide-details
      />
      <v-spacer />
      <v-btn>Create Event</v-btn>
    </v-app-bar>
    <v-container>
      <v-row>
        <v-col sm="6" offset-sm="3">
          <v-main>
            <slot :searchText="searchText" />
          </v-main>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<style scoped>
.v-toolbar__title a {
  text-decoration: none;
  transition: 300ms ease-in;
  color: #1a1a1a;
}

.v-toolbar__title a:hover {
  color: rebeccapurple;
}
</style>