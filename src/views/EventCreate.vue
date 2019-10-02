<template>
  <div>
    <!-- INSTEAD OF 'userName' and 'UserID' -->
    <h1>Create an Event, {{ user.name }}</h1>
    <p>This event was created by {{ user.id }}</p>
    <p>There are {{ catLength }} categories</p>
    <p>{{ getEventById(2) }}</p>
    <ul>
      <li v-for="cat in categories" :key="cat">{{ cat }}</li>
    </ul>
  </div>
</template>

<script>
import { mapState, mapGetters } from 'vuex';

export default {
  //Even simiplier, Use an array
  // Instead use string to access those state properties
  computed: {
    // //Old way without using mapGetters after importing it
    // getEvent() {
    //   return this.$store.getters.getEventById;
    // },

    // // User catLength getter method
    catLength() {
      return this.$store.getters.catLength;
    },
    // Can you a getting to acces categories.length from anywhere
    // catLength() {
    //   return this.$store.categories.length
    // },
    ...mapGetters(['getEventById']),
    ...mapState(['user', 'categories'])

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

<style scoped></style>
