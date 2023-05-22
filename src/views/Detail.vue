<script>
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
};
</script>

<template>
     <h2>{{ post.title }}</h2>

     <textarea :value="post.content"></textarea>

     <h4>{{ post.datetime }}</h4>
     <h5> {{ post.hora }}</h5>
</template>


<style scoped>
textarea {
    resize: none;
    outline: none;
    border: none;
    width: 80%;
}
</style>