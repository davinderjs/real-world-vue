<template>
  <div>
    <h1>Create an Event, {{ user.name }}</h1>
    <form @submit.prevent="createEvent">
      <BaseSelect
        v-model="event.category"
        label="Select a category"
        :options="categories"
        class="field"
      />
      <h3>Name & describe your event</h3>
      <BaseInput
        v-model="event.title"
        label="Title"
        type="text"
        placeholder="Add an event title"
        class="field"
      />
      <BaseInput
        v-model="event.description"
        label="Description"
        type="text"
        placeholder="Add a description"
        class="field"
      />
      <h3>Where is your event?</h3>
      <BaseInput
        v-model="event.location"
        label="Location"
        type="text"
        placeholder="Add a location"
        class="field"
      />
      <h3>When is your event?</h3>
      <div class="field">
        <label>Date</label>
        <datepicker v-model="event.date" placeholder="Select a date"/>
      </div>

      <BaseSelect v-model="event.time" label="Select a time" :options="times" class="field"/>

      <!-- <input type="submit" class="button -fill-gradient" value="Submit"> -->
      <BaseButton type="submit" buttonClass="-fill-gradient">Submit</BaseButton>
    </form>
  </div>
</template>

<script>
import { mapState, mapGetters } from "vuex";
import Datepicker from "vuejs-datepicker";
import NProgress from "nprogress";
import { required } from "vuelidate/lib/validators";

export default {
  components: {
    Datepicker
  },
  data() {
    const times = [];
    for (let i = 0; i < 24; i++) {
      times.push(i + ":00");
    }
    return {
      times,
      categories: this.$store.state.categories,
      event: this.createFreshEventObject()
    };
  },
  methods: {
    createFreshEventObject() {
      const user = this.$store.state.user.user;
      const id = Math.floor(Math.random() * 10000000);

      return {
        id: id,
        user: user,
        category: "",
        organizer: user,
        title: "",
        description: "",
        location: "",
        date: "",
        time: "",
        attendees: []
      };
    },
    createEvent() {
      NProgress.start();
      this.$store
        .dispatch("event/createEvent", this.event)
        .then(() => {
          this.$router.push({
            name: "event-show",
            params: { id: this.event.id }
          });
          this.event = this.createFreshEventObject();
        })
        .catch(() => {
          NProgress.done();
        });
    }
  },
  computed: {
    catLength() {
      return this.$store.getters.catLength;
    },
    ...mapState(["user"]),
    ...mapGetters(["getEventById"])
  }
};
</script>

<style scoped>
.field {
  margin-bottom: 24px;
}
</style>
