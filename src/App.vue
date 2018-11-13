<template>
  <div id="app">
    <h1>Timers</h1>
    <timer :start="5" @finish="voltooideTimers++"/>
    <timer :start="15" @finish="voltooideTimers++"/> 
    <timer :start="10" @finish="voltooideTimers++"/> 
    <h2>Voltooide timers</h2>
    {{ voltooideTimers }}
  </div>
</template>

<script>
import Timer from './components/Timer.vue'

export default {
  name: 'app',
  data() {
    return {
      voltooideTimers: 0
    }
  },
  components: {
    Timer
  }
}
</script>

<style>
#app {
  
}
</style>
