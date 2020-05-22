<style scoped>
* { display: flex;justify-content: center;}
html { background:black; }
</style>

<template>
  <div class="home">
    <SingleStock/>
  </div>
</template>

<script>
// @ is an alias to /src
import SingleStock from '@/components/SingleStock.vue'

export default {
  name: 'Home',
  components: {
    SingleStock
  }
}
</script>
