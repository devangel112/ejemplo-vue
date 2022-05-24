<template>
  <div>
      <Home message="Hola, enviando un mensaje desde template" />
  </div>
</template>

<script>
import Home from '@/components/Home.vue'

export default {
  name: 'HomeView',
  components: {
    Home
  }
}
</script>
