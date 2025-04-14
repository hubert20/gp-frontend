<template>
  <div>
    <h2>Aktualne wydarzenie</h2>
    <div v-if="event">
      <pre>{{ event }}</pre>
    </div>
    <div v-else>Ładowanie danych...</div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const event = ref(null)

onMounted(async () => {
  try {
    const response = await axios.get('http://localhost:4010/api/v1/events/aut/reward_categories')
    event.value = response.data
  } catch (error) {
    console.error('Błąd przy pobieraniu danych:', error)
  }
})
</script>
