<template>
  <div>
    <nav id="nav" class="nav">
      <router-link to="/" class="brand">Real World Events</router-link>

      |
      <div id="nav">
        <router-link :to="{ name: 'event-list' }">List</router-link>|
        <router-link :to="{ name: 'event-create' }">Create</router-link>
      </div>
    </nav>
  </div>
</template>

<script>
export default {};
</script>

<style scoped></style>
