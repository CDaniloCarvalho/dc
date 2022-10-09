<template>
  <div class="home">
    <bannerHome class="banner" msg="banner"/>
  </div>
</template>
<style scoped>
  .banner{
    position: relative;
    top: 54px;
  }
</style>

<script>
// @ is an alias to /src
import bannerHome from '@/components/banners/bannerHome.vue'

export default {
  name: 'HomeView',
  components: {
    bannerHome
  }
}
</script>
