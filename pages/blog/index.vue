<template>
  <div class="col-lg-9">
    <list-blogs :dataBlogs="dataBlogs" @getListBlogs="getData" />
      <b-pagination
      v-model="currentPage"
      :total-rows="page.total"
      :per-page="page.per_page"
      @page-click="nextPage"
      prev-text="Prev"
      next-text="Next"
      ></b-pagination>
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
      page:{},
      currentPage: 1,
    }
  },
  methods: {
    /**
     * get list blog
     */
    getData() {
      axios.get('http://127.0.0.1:8000/api/blogs').then((res) => {
        this.dataBlogs = res.data.data
        this.page = res.data
      })
    },

    /**
     * get list blog next page
     */
    nextPage(e, page){
      axios.get('http://127.0.0.1:8000/api/blogs?page=' + page).then((res) => {
        this.dataBlogs = res.data.data
        this.page = res.data
        console.log(res.data);
      })
    }
  },
  mounted() {
    this.getData()
  },
}
</script>
<style>
.pagination{
      justify-content: flex-end;
}
</style>
