<template>
  <Layout>
    <v-container>
      <v-row>
        <v-col sm="6" offset-sm="3">
          <v-tabs v-model="tab" grow>
            <v-tab>All Events</v-tab>
            <v-tab>Music</v-tab>
            <v-tab>Coding</v-tab>
          </v-tabs>
          <v-row>
            <v-card
              v-for="edge in events"
              :key="edge.node.id"
              class="mt-5"
              width="300"
            >
              <v-img
                class="white--text align-end"
                height="200px"
                :src="edge.node.image"
              />
              <!-- <v-card-title>Top 10 Australian beaches</v-card-title> -->
              <v-card-title>{{ edge.node.title }}</v-card-title>

              <v-card-subtitle class="pb-0">
                {{ edge.node.date }}
              </v-card-subtitle>
              <v-card-actions>
                <v-btn color="orange" text> MORE INFO </v-btn>
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
        date
        image,
        category
      }
    }
  }
}
</page-query>

<script>
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
      // use a switch here
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
        // console.log("WHAT IS EDGE?:", edge.node);
        return edge.node.category === val;
      });
    },
  },
};
</script>

<style>
.home-links a {
  margin-right: 1rem;
}
</style>
