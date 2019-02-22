<template>
  <div>
    <h1>Create an Event, {{ user.name }}</h1>
    <p>There are {{ catLength }} categories.</p>
    <p>{{ getEventById(1) }}</p>
    <ul>
      <li v-for="category in categories" :key="category.id">{{ category }}</li>
    </ul>
  </div>
</template>

<script>
import { mapState, mapGetters } from "vuex";

export default {
  computed: {
    catLength() {
      return this.$store.getters.catLength;
    },

    ...mapState(["user", "categories"]),
    ...mapGetters(["getEventById"])
  }
};
</script>

<style scoped></style>
