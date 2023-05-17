<script>
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "Meu primeiro post",
          datetime: Date.now(),
          content: "Postar aqui não é legal",
        },
        {
          title: "Meu segundo post",
          datetime: Date.now(),
          content: "Postar aqui não é legal",
        },
      ],
      formData: {
        title: "",
        content: "",
      },
      search: "",
    };
  },
  computed: {
    filteredPosts() {
      // se search estiver vazia, retorne a lista completa de posts
      if (!this.search) return this.posts;

      //se tiver qualquer coisa em search, faz o filtro
      const listaFiltrada = [];

      for (const post of this.posts) {
        if (post.title.includes(this.search)) {
          listaFiltrada.push(post);
        }
      }
      return listaFiltrada;
    },
  },
  methods: {
    handleClick(event) {
      const now = new Date();

      const dataDaPostagem = `${now.getDate()}/${
        now.getMonth() + 1
      }/${now.getFullYear()}`;

      this.posts.push({
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      });

      this.formData = {
        title: "",
        content: "",
      };
    },
    handleImputChange(event) {
      const { name, value } = event.target;
      this.formData[name] = value;
    },
  },
};
</script>

<template>
  <input
    class="search"
    v-model="search"
    placeholder="Procure pelo título do post..."
  />

  <div id="lista-posts">
    <div class="post" v-for="post in filteredPosts" :key="post.key">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>

  <form>
    <input class="search" v-model="formData.title" placeholder="Título" />
    <textarea
      name="content"
      :value="formData.content"
      @keyup="handleImputChange"
      placeholder="Escreva seu post aqui..."
      class="search"
      cols="30"
      rows="10"
    >
    </textarea>

    <button type="button" @click="handleClick">Salvar</button>
  </form>

  <RouterView />
</template>

<style scoped>
input {
  width: 30vw;
  height: 30px;
}

.search {
  border: none;
  outline: none;
  color: #00000094;
  background: #f0f0f0;
  font-size: 0.9em;
  padding-left: 10px;
  border-radius: 0.5em;
  font-family: "PlayfairDisplay";
  letter-spacing: 2px;
}

.search:focus {
  border-radius: 0.5em;
  box-shadow: inset 1.5px 1px 1px 1px rgb(73, 155, 228);
}

textarea {
  width: 90vw;
  height: 130px;
  resize: none;
}

div.post {
  padding: 3px;
  margin: 1rem;
  width: 75%;
  height: 100%;
  border: solid 1px rgba(53, 53, 53, 0.034);
  box-shadow: -3px 2px 3px rgba(78, 172, 254, 0.534);
  border-radius: 0.5em;
}

form {
  background: linear-gradient(
    280deg,
    rgba(5, 237, 254, 1) 0%,
    rgba(78, 172, 254, 1) 100%
  );
  display: block;
  flex-direction: column;
  padding: 10px;
  margin: 1rem;
  border-radius: 0.5em;
}

form > * {
  margin: 1rem;
}
</style>
