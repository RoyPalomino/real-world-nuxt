<template>
  <div>
    <h1>Events</h1>
    <EventCard v-for="(event, index) in events" :key="index" :event="event" />
  </div>
</template>
<script>
import EventCard from '~/components/EventCard.vue'

export default {
  components: {
    EventCard
  },
  async asyncData({ $axios, error }) {
    try {
      const { data } = await $axios.get('http://localhost:3001/events')
      return {
        events: data
      }
    } catch (e) {
      error({
        errorCode: 503,
        message: 'Unable to fetch events at this time. Please try again.'
      })
    }
  },
  head() {
    return {
      title: 'List Events'
    }
  }
}
</script>
