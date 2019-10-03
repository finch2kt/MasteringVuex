<template>
  <div>
    <form @submit.prevent="createEvent">
      <label>Select a category</label>
      <select v-model="event.category">
        <option v-for="cat in categories" :key="cat">{{ cat }}</option>
      </select>
      <h3>Name & describe your event</h3>
      <div class="field">
        <label>Title</label>
        <input
          v-model="event.title"
          type="text"
          placeholder="Add an event title"
        />
      </div>
      <div class="field">
        <label>Description</label>
        <input
          v-model="event.description"
          type="text"
          placeholder="Add a description"
        />
      </div>
      <h3>Where is your event?</h3>
      <div class="field">
        <label>Location</label>
        <input
          v-model="event.location"
          type="text"
          placeholder="Add a location"
        />
      </div>
      <h3>When is your event?</h3>
      <div class="field">
        <label>Date</label>
        <datepicker v-model="event.date" placeholder="Select a date" />
      </div>
      <div class="field">
        <label>Select a time</label>
        <select v-model="event.time">
          <option v-for="time in times" :key="time">{{ time }}</option>
        </select>
      </div>
      <input type="submit" class="button -fill-gradient" value="Submit" />
    </form>
    <!-- INSTEAD OF 'userName' and 'UserID' -->
    <!-- <h1>Create an Event, {{ user.name }}</h1>
    <p>This event was created by {{ user.id }}</p>
    <p>There are {{ catLength }} categories</p>
    <p>{{ getEventById(2) }}</p>
    <ul>
      <li v-for="cat in categories" :key="cat">{{ cat }}</li>
    </ul>-->
  </div>
</template>

<script>
// import { mapState, mapGetters } from 'vuex';
import Datepicker from 'vuejs-datepicker';

export default {
  components: {
    Datepicker
  },
  data() {
    const times = [];
    for (let i = 1; i <= 24; i++) {
      times.push(i + ':00');
    }
    return {
      event: this.createFreshEventObject(),
      // Or times: times
      times,
      categories: this.$store.state.categories
    };
  },
  methods: {
    createEvent() {
      this.$store
        .dispatch('event/createEvent', this.event)
        .then(() => {
          this.$router.push({
            name: 'event-show',
            params: { id: this.event.id }
          });
          this.event = this.createFreshEvenObject();
        })
        .catch(() => {});
    },
    createFreshEventObject() {
      const user = this.$store.state.user.user;
      const id = Math.floor(Math.random() * 10000000);

      return {
        id: id,
        user: user,
        category: '',
        organizer: user,
        title: '',
        description: '',
        location: '',
        date: '',
        time: '',
        attendees: []
      };
    }
  },
  //Even simiplier, Use an array
  // Instead use string to access those state properties
  computed: {
    // //Old way without using mapGetters after importing it
    // getEvent() {
    //   return this.$store.getters.getEventById;
    // },
    // // User catLength getter method
    // catLength() {
    //   return this.$store.getters.catLength;
    // }
    // Can you a getting to acces categories.length from anywhere
    // catLength() {
    //   return this.$store.categories.length
    // },
    // IMPORT mapState and mapGetters from vuex store
    // ...mapGetters(['getEventById'])
    // ...mapState(['user', 'categories'])
    // Instead use string to access those state properties
    // computed: mapState({
    //   user: 'user',
    //   categories: 'categories'
    // })
    // Without top level state, we won't need dot notation to access property on that state
    // computed: mapState({
    //   userName: state => state.user.name,
    //   userID: state => state.user.id,
    //   categories: state => state.categories
    // })
  }
};
</script>

<style scoped>
.field {
  margin-bottom: 24px;
}
</style>
