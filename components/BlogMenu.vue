<template>
  <div class="col-lg-3" >
    <ul class="list-group">
      <li class="list-group-item"> <nuxt-link to="/blog"><a href="" class="text-center d-block ">List</a></nuxt-link></li>
      <li class="list-group-item"> <nuxt-link to="/blog/new"><a href="" class="text-center d-block">New</a></nuxt-link></li>
      <li class="list-group-item"> <nuxt-link to="/blog/search"><a href="" class="text-center d-block">Search</a></nuxt-link></li>
      <li class="list-group-item"> <nuxt-link to="/blog/edit"><a href="" class="text-center d-block">Edit</a></nuxt-link></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'BlogMenu',
}
</script>
<style>
a {
    color: #000;
    font-size: 16px;
    font-weight: 500;
}
</style>