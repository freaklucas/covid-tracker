<template>
  <Header />
  <div class="container mx-auto ">
    <router-view />
    <Home />
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import Home from '@/views/Home.vue'

export default {
  name: 'App',
  components: {
    Header,
    Home
  }
}
</script>
