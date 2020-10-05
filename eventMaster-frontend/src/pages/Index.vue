<template>
  <Layout>
    <v-container>
      <v-row>
        <v-col sm="6" offset-sm="3">
          <v-tabs v-model="tab" grow>
            <v-tab>All Events</v-tab>
            <v-tab>Music</v-tab>
            <v-tab>Coding</v-tab>
            <v-tab>Theatre</v-tab>
            <v-tab>Sports</v-tab>
          </v-tabs>

          <v-row class="justify-space-around">
            <v-card
              v-for="edge in events"
              :key="edge.node.id"
              width="280"
              class="mt-5"
            >
              <v-img
                class="white--text align-end"
                height="200px"
                :src="`http://localhost:1337${edge.node.thumbnail}`"
              />

              <v-card-title>{{ edge.node.title }}</v-card-title>

              <v-card-subtitle class="pb-0">
                {{ formatDate(edge.node.date) }}
              </v-card-subtitle>

              <v-card-actions>
                <v-btn color="orange" text>
                  More Info
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-row>
        </v-col>
      </v-row>
    </v-container>
  </Layout>
</template>

<page-query>
  query {
    events: allEvent {
      edges {
        node {
          id
          title
          description
          price
          duration
          date
          thumbnail
          image
          category
        }
      }
    }
  }
</page-query>

<script>
import moment from "moment";

export default {
  metaInfo: {
    title: "Hello, world!",
  },
  data() {
    return {
      tab: 0,
      events: [],
    };
  },

  mounted() {
    this.events = this.$page.events.edges;
  },

  watch: {
    tab(val) {
      if (this.tab === 0) {
        this.showAllEvents();
      } else {
        this.showEventsByType(val);
      }
    },
  },
  methods: {
    showAllEvents() {
      this.events = this.$page.events.edges;
    },

    showEventsByType(val) {
      this.events = this.$page.events.edges.filter((edge) => {
        return edge.node.category === val;
      });
    },
    formatDate(date) {
      return moment(date).format("MMM Do YYYY, h:mm a");
    },
  },
};
</script>

<style>
.home-links a {
  margin-right: 1rem;
}
</style>
