<template lang="pug">
  v-app
    v-content
      v-container(fluid)
        NuevaCarrera
</template>

<script>
import NuevaCarrera from './components/NuevaCarrera'

export default {
  name: 'App',
  components: {
    NuevaCarrera
  }
}
</script>

<style>
</style>
