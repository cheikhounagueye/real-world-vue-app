<script setup>
import { ref, onMounted } from 'vue'
import EventService from '../services/EventService'

const props = defineProps({
  id: {
    required: true,
  },
})

const event = ref(null)

onMounted(() => {
  // fetch event (by id) and set local event data
  EventService.getEvent(props.id)
    .then((response) => {
      console.log('test')
      event.value = response.data
      console.log(event.value)
    })
    .catch((error) => {
      console.log(error)
    })
})
</script>

<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>
