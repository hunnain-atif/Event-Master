<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title>
        <g-link to="/">Event Master</g-link>
      </v-toolbar-title>

      <v-text-field
        v-model="searchText"
        placeholder="Search"
        @click:clear="searchText = ''"
        class="ml-8"
        clearable
        style="max-width: 350px"
        prepend-inner-icon="mdi-magnify"
        outlined
        rounded
        dense
        hide-details
      />

      <v-spacer />
      <v-btn>Create Event</v-btn>
    </v-app-bar>
    <v-main>
      <slot :searchText="searchText" />
    </v-main>
  </v-app>
</template>

<static-query>
query {
  metadata {
    siteName,
    siteDescription
  }
}
</static-query>

<script>
export default {
  data() {
    return {
      searchText: "",
    };
  },
};
</script>


<style scoped>
.v-toolbar__title a {
  text-decoration: none;
  color: black;
}
</style>