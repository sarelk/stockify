<style scoped>
* { display: flex;justify-content: center; }
html { background:black; }
</style>

<template>
  <div class="home">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <SingleStock/>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import SingleStock from '@/components/SingleStock.vue'

export default {
  name: 'Home',
  components: {
    // HelloWorld,
    SingleStock
  }
}
</script>
