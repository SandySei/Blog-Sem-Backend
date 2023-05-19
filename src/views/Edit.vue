<script>
import PostForm from '../components/PostForm.vue';

export default {
  props: {
    posts: Array,
  },
  data() {
    return {
      post: this.posts[this.$route.params.id],
    };
  },
  components: {
    PostForm,
  },
};
</script>

<template>
  <PostForm :post="post"/>
</template>
