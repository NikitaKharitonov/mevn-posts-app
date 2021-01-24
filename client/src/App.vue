<template>
  <div>
    <br/><br/>
    <Feed/>   
  </div>
</template>

<script>
import Feed from './components/Feed'

export default {
  name: 'App',
  data() {
    return {
      date: new Date()
    }
  },
  components: {
    Feed
  }
}
</script>

<style>
body {
  color: white;
  font-family: Arial, Helvetica, sans-serif;
  background: #222226;
}
</style>
