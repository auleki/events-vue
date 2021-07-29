<script>
import moment from "moment";

export default {
  metaInfo: {
    title: "!",
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
    formatDate(date) {
      return moment(date).format("MMM Do YYY, h:mm a");
    },
    getEvents(query) {
      return this.events.filter((edge) => {
        return edge.node.title.toLowerCase().includes(query.toLowerCase());
      });
    },
  },
};
</script>

<template>
  <Layout v-slot="{ searchText }">
    <v-tabs v-model="tab" grow>
      <v-tab>All Events</v-tab>
      <v-tab>Music</v-tab>
      <v-tab>Coding</v-tab>
    </v-tabs>
    <v-row class="justify-space-around">
      <v-card
        v-for="edge in getEvents(searchText)"
        :key="edge.node.id"
        class="mt-5"
        width="280"
      >
        <v-img
          class="white--text align-end"
          height="200px"
          :src="edge.node.image"
        />
        <v-card-title>{{ edge.node.title }}</v-card-title>
        <v-card-subtitle class="pb-0">
          {{ formatDate(edge.node.date) }}
        </v-card-subtitle>
        <v-card-actions>
          <v-btn
            @click="$router.push(`/events/${edge.node.id}`)"
            color="orange"
            text
          >
            MORE INFO
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-row>
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



<style>
.home-links a {
  margin-right: 1rem;
}
</style>
