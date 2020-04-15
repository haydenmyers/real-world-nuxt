<template>
  <div>
    <h1>Events</h1>

    <event-card
    v-for="(event, index) in events"
    :key="index"
    :event="event"
    :data-index="index"
    ></event-card>
    
  </div>
</template>

<script>
import EventCard from "@/components/EventCard.vue";
import { mapState } from 'vuex';

export default {
  components: {
    EventCard
  },
  head() {
    return {
      title: "Event Listing"
    };
  },
  async fetch({ store, error }) {
    try {
      await store.dispatch('events/fetchEvents')
    } catch (e) {
      error({
        statusCode: 503,
        message: "Nah fam, not working. Sos!"
      });
    }
  },
  computed: mapState({
    events: state => state.events.events
  })
};
</script>