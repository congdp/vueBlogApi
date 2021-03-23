<template>
  <div class="col-lg-9">
    <h3>{{ title }}</h3>
    <ul v-if="errors.length > 0" class="alert alert-danger">
      <li v-for="error in errors" :key="error">{{ error }}</li>
    </ul>
    <div class="w-50 mb-5">
      <div class="form-group">
        <label for="title">Tiêu đề</label>
        <input
          id="title"
          v-model="form.title"
          type="text"
          class="form-control"
          placeholder="Tiêu đề"
        />
      </div>
      <div class="form-group">
        <label for="desc">Mô tả ng</label>
        <input
          id="desc"
          v-model="form.des"
          type="text"
          class="form-control"
          placeholder="Mô tả"
        />
      </div>

      <div class="form-group">
        <label for="detail">Chi tiết</label>
        <textarea
          id="detail"
          v-model="form.detail"
          class="form-control"
          rows="7"
        ></textarea>
      </div>
      <div class="mb-3">
        <label for="thumb">Hình ảnh</label> <br />
        <input id="thumb" type="file" />
      </div>
      <div class="mb-3">
        <label for="type">Loại</label> <br />
        <select id="type" v-model="form.category" name="type">
          <option v-for="(cat, index) in CATEGORY" :key="index" :value="index">
            {{ cat }}
          </option>
        </select>
      </div>
      <label for="" class="d-block">Vị trí</label>
      <div class="form-group">
        <!-- <p>Vị trí</p> -->
        <ul class="list-group list-group-flush list-unstyled">
          <li
            v-for="(post, key) in POSITION"
            :key="post"
            class="list-group-control"
          >
            <div class="custom-control custom-checkbox">
              <input
                :id="'check' + key"
                v-model="form.position"
                type="checkbox"
                :value="key"
                class="custom-control-input"
              />
              <label class="custom-control-label" :for="'check' + key">{{
                post
              }}</label>
            </div>
          </li>
        </ul>
      </div>
      <label for="" class="d-block mt-3">Public</label>
      <div class="form-check">
        <input
          v-model="form.public"
          class="form-check-input"
          type="radio"
          :value="1"
        />
        <label class="form-check-label d-block" for="exampleRadios1">
          Yes
        </label>
        <input
          v-model="form.public"
          class="form-check-input"
          type="radio"
          :value="0"
        />
        <label class="form-check-label" for="exampleRadios1"> No </label>
      </div>
      <div class="form-group mt-3">
        <label for="desc">Date Public</label>
        <input
          id="desc"
          v-model="form.data_pubblic"
          type="date"
          class="form-control w-50"
        />
      </div>
      <div class="active d-flex justify-content-center">
        <button
          v-if="title === 'New Blogs'"
          class="btn btn-success mr-2"
          @click="createBlog()"
        >
          Save
        </button>
        <button
          v-if="title === 'Edit Blogs'"
          type="button"
          class="btn btn-success mr-2"
          @click="updateBlog(form.id)"
        >
          Edit
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import { DATA_CATE, DATA_POS } from '@/constants/constants.js'
import swal from 'sweetalert2'
export default {
  name: 'New',
  props: ['title'],
  data() {
    return {
      CATEGORY: DATA_CATE,
      POSITION: DATA_POS,
      form: {
        id: '',
        title: '',
        des: '',
        detail: '',
        category: '',
        public: '',
        data_pubblic: '',
        position: [],
        thumbs: '',
      },
      errors: [],
    }
  },
  mounted() {
    if (this.$route.params.id != null) {
      this.getBlogByID(this.$route.params.id)
    }
  },
  methods: {
    /**
     * create blog
     */
    createBlog() {
      this.validate()
      if (this.errors.length > 0) {
        return this.errors
      } else {
        axios.post('http://localhost:8000/api/blogs', this.form).then((res) => {
          this.$router.push('/blog')
          swal.fire({
            position: 'center',
            icon: 'success',
            title: 'Successfully Added',
            showConfirmButton: false,
            timer: 1500,
          })
        })
      }
    },

    /**
     * get blog by id
     */
    getBlogByID(id) {
      axios
        .get('http://localhost:8000/api/blogs/' + id)
        .then((res) => (this.form = res.data))
    },

    /**
     * update blog
     */
    updateBlog(id) {
      this.validate()
      if (this.errors.length > 0) {
        return this.errors
      } else {
        axios
          .put('http://localhost:8000/api/blogs/' + id, this.form)
          .then((res) => {
              this.$router.push('/blog')
            swal.fire({
              position: 'center',
              icon: 'success',
              title: 'Successfully Update',
              showConfirmButton: false,
              timer: 1500,
            })
          })

      }
    },

    /**
     * check validate
     */
    validate() {
      this.errors = []
      if (this.form.title == '') {
        this.errors.push('title không được trống')
      }
      if (this.form.des == '') {
        this.errors.push('des không được trống')
      }
      if (this.form.detail == '') {
        this.errors.push('deatil không được trống')
      }
      if (this.form.category == '') {
        this.errors.push('category không được trống')
      }
      if (this.form.position == []) {
        this.errors.push('position không được trống!')
      }
    },
  },
}
</script>
