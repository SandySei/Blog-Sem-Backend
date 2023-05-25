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

  <textarea readonly :value="post.content"></textarea>

  <h4>{{ post.datetime }}</h4>
</template>

<style scoped>
textarea {
  height: 100%; 
  width: 95%;
  max-width: 1200px;
  background: #f0f0f0ea;
  border-radius: 0.3em;
  margin: 1rem;
  padding: 15px;

  font-family: 'Times New Roman', Times, serif;
  color: #000000;
  resize: none;
  outline: none;
  border: none;
  width: 90%;
  height: 75vh;

  font-weight: 500;
  letter-spacing: 0.5px;
  text-align: justify;
  text-indent: 20px;
  font-size: 20px;
}

h2,
h4 {
  font-family: 'Times New Roman', Times, serif;
}

h4 {
  color: #000000;
  text-decoration: none;
  text-align: end;
  font-size: 14px;
  font-weight: 300;
}

h2 {
  padding-left: 20px;
  padding-right: 20px;
  color: #000000;
  text-transform: uppercase;
  font-size: 35px;
}

</style>
