<template lang="pug">
  v-app
    v-content
      v-container(fluid)
        HelloWorld
</template>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
</style>
