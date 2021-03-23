<template>
  <div class="container">
    <div class="header my-3">
      <blog-header />
    </div>
    <div class="row">
      <blog-menu/>
      <Nuxt />
    </div>
  </div>
</template>
<script>
import BlogHeader from '../components/BlogHeader.vue'
import BlogMenu from '../components/BlogMenu.vue'
export default {
  components: {
    BlogHeader,
    BlogMenu,
  },
}
</script>
<style>
</style>