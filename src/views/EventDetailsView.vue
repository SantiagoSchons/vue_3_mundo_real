<script setup>
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService.js'

const props = defineProps({
  id: {
    require: true,
  }
})

const event = ref(null)


onMounted(() => {
  EventService.getEvent(props.id)
  .then((response) => {
      event.value = response.data
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
    <p>{{ props.id }}</p>
    <p>{{ props.value }}</p>
  </div>
</template>