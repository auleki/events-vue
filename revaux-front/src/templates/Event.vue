<template>
  <layout>
    <h1>{{ $page.event.title }}</h1>
    <img :src="$page.event.image" alt="event cover" />
  </layout>
</template>

<page-query>
  query {
    event(id: "5") {
      id 
      title 
      duration
      price
      date
      image
    }
  }
</page-query>

<script>
export default {
  metaInfo() {
    return {
      title: this.$page.event.title,
    };
  },
};
</script>