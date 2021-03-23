<template>
  <div>
    <h3>List Blogs</h3>
    <table class="table table-bordered">
      <thead>
        <tr>
          <th scope="col">ID</th>
          <th scope="col">Tin</th>
          <th scope="col">Loại</th>
          <th scope="col">Trạng thái</th>
          <th scope="col">Vị trí</th>
          <th scope="col">Ngày public</th>
          <th scope="col">Edit</th>
          <th scope="col">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(blog, index) in dataBlogs" :key="index">
          <th scope="row">{{ blog.id }}</th>
          <td>{{ blog.title }}</td>
          <td>{{ filterCategory(blog.category) }}</td>
          <td>{{ blog.public == 1 ? 'Public' : 'Private' }}</td>
          <td>{{ filterPosition(blog.position) }}</td>
          <td>{{ blog.data_pubblic }}</td>
          <td>
            <nuxt-link :to="`/blog/${blog.id}`"
              ><button class="btn btn-primary">Edit</button></nuxt-link
            >
          </td>
          <td>
            <button class="btn btn-danger" @click="deleteBlog(blog.id)">
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import axios from 'axios'
import { DATA_CATE, DATA_POS } from '@/constants/constants.js'
import swal from 'sweetalert2'
export default {
  name: 'ListBlog',
  props: {
    dataBlogs: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      CATEGORY: DATA_CATE,
      POSITION: DATA_POS,
    }
  },
  methods: {
    /**
     * delete blog
     */
    deleteBlog(id) {
      swal
        .fire({
          title: 'Are you sure?',
          text: "You won't be able to revert this!",
          icon: 'warning',
          showCancelButton: true,
          confirmButtonColor: '#3085d6',
          cancelButtonColor: '#d33',
          confirmButtonText: 'Yes, delete it!',
        })
        .then((result) => {
          if (result.isConfirmed) {
            // swal.fire('Deleted!', 'Your file has been deleted.', 'success')
            axios.delete('http://localhost:8000/api/blogs/' + id).then((res) => {
              this.$emit('getListBlogs', this.dataBlogs)
            })
            swal.fire('Deleted!', 'Your file has been deleted.', 'success')
          }
        })
    },

    /**
     * get name position
     */
    filterPosition(pos) {
      return pos
        .map((item) => {
          return this.POSITION[item]
        })
        .join(',')
    },

    /**
     * get name category
     */
    filterCategory(id) {
      return this.CATEGORY.find((cate, index) => {
        if (index === id) {
          return cate
        }
      })
    },
  },
}
</script>
