<template>
  <div >
    <h3>Search Blog</h3>
    <div action="" class="mb-3">
      <div class="form-group row">
        <label for="title" class="col-sm-2 col-form-label">Tiêu đề</label>
        <div class="col-sm-10">
          <input type="text" class="form-control" v-model="search" id="title" />
        </div>
      </div>
      <button class="btn btn-success" @click="sendKeySearch()">Search</button>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'Search',
  data() {
    return {
      search: '',
    }
  },
  methods: {
    /**
     * send key search to searchBlog()
     */
  sendKeySearch() {
      this.$emit('getKeyWord',this.search);
    },
  },
}
</script>
<style>
</style>