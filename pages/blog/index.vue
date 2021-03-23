<template>
  <div class="col-lg-9">
    <list-blogs :dataBlogs="dataBlogs" @getListBlogs="getData" />
  </div>
</template>

<script>
import axios from 'axios'
import ListBlogs from '../../components/Blogs/ListBlogs.vue'
export default {
  components: {
    ListBlogs,
  },
  data() {
    return {
      dataBlogs: [],
    }
  },
  methods: {
    /**
     * get list blog
     */
    getData() {
      axios.get('http://localhost:8000/api/blogs').then((res) => {
        this.dataBlogs = res.data
        // this.$emit('getData',this.dataBlogs)
        console.log(this.dataBlogs)
      })
    },
  },
  mounted() {
    this.getData()
  },
}
</script>
