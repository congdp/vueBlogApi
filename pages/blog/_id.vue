<template>
  <create-edit :title="title" />
</template>
<script>
import CreateEdit from '../../components/Blogs/CreateEdit'
export default {
  data() {
    return {
      title: 'Edit Blogs',
    }
  },
  components: {
    CreateEdit,
  },
}
</script>
