<template>
  <div class="home">
    <img alt="Travel logo" height="300" src="../assets/logo.png">
    <Suggest msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Suggest from '@/components/Suggest.vue'

export default {
  name: 'HomeView',
  components: {
    Suggest
  }
}
</script>
