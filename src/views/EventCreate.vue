<template>
  <div>
    <h1>Create an Event, {{ user.name }}</h1>
    <ul>
      <li v-for="category in categories" :key="category.id">{{ category }}</li>
    </ul>
  </div>
</template>

<script>
import { mapState } from "vuex";

export default {
  computed: {
    ...mapState(["user", "categories"])
  }
};
</script>

<style scoped></style>
