<template>
    <div class="events">
      <h1>Events for Good</h1>
      <EventCard v-for="event in events" :key="event.id" :event="event" />
    </div>
</template>

<script>
import { defineComponent } from 'vue';
import EventCard from '@/components/EventCard.vue';
import EventService from '@/services/EventService.js';

export default defineComponent({
  name: 'EventList',
  components: {
    EventCard
  },
  data() {
    return {
      events: null
    };
  },
  created() {
    EventService.getEvents()
      .then(resp => {
        this.events = resp.data;
      })
      .catch(err => {
        console.log(err);
      });
  }
});
</script>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
