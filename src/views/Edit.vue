<script>
import PostForm from '../components/PostForm.vue';

export default {
  props: {
    posts: Array,
  },
  data() {
    //acessa o parametro id uma única vez 
    const id = this.$route.params.id;

    return {
    id: id,
    post: this.posts[id],
    };
  },
  components: {
    PostForm,
  },
};
</script>

<template>
  <PostForm :post="post" :id="id"/>
</template>