<template>
  <create-edit :title="title" />
</template>

<script>
import CreateEdit from '../../components/Blogs/CreateEdit'
export default {
  data() {
    return {
      title: 'New Blogs',
    }
  },
  components: {
    CreateEdit,
  },
}
</script>
