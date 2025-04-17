<template>
  <div>
    <h2>Aktualne wydarzenie</h2>
    <div v-if="event">
      <p><strong>Nazwa:</strong> {{ event.name }}</p>
      <p><strong>Slug:</strong> {{ event.slug }}</p>
      <p><strong>Początek:</strong> {{ event.start_at }}</p>
      <p><strong>Koniec:</strong> {{ event.end_at }}</p>
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
    const response = await axios.get('http://localhost:4010/api/v1/events/current')
    event.value = response.data.data // <- dostęp tylko do "data"
  } catch (error) {
    console.error('Błąd przy pobieraniu danych:', error)
  }
})
</script>
