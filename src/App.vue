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
          title: "Meu primeiro post",
          datetime: Date.now(),
          content: "Postar aqui não é legal",
        },
      ],
      formData: {
        title: "",
        content: "",
      },
    };
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
  <div id="lista-posts">
    <div class="post" v-for="post in posts" :key="post.key">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>

  <form>
    <input v-model="formData.title" placeholder="Título" />
    <textarea
      name="content"
      :value="formData.content"
      @keyup="handleImputChange"
      placeholder="Escreva seu post aqui..."
      id=""
      cols="30"
      rows="10"
    >
    </textarea>

    <button class="glow-on-hover" type="button" @click="handleClick">
      Salvar
    </button>
  </form>

  <RouterView />
</template>

<style scoped>
div#lista-posts {
  background-color: rgb(0, 0, 0);
  padding: 1rem;
  font-family: "Times New Roman", Times, serif;
  text-align: center;
}

form {
  background-color: rgb(0, 0, 0);
}

input {
  height: 1rem;
  border-radius: 9999em;
  color: white;
  font-size: xx-large;
  height: 30px;
  padding-left: 10px;
  font-family: "Times New Roman", Times, serif;
}


form {
  display: flex;
  flex-direction: column;
}

form > * {
  margin: 1rem;
}

.glow-on-hover {
  width: 220px;
  height: 50px;
  border: none;
  outline: none;
  color: #fff;
  background: #111;
  cursor: pointer;
  position: relative;
  z-index: 0;
  border-radius: 10px;
}

.glow-on-hover:before {
  content: "";
  background: linear-gradient(
    45deg,
    #ff0000,
    #ff7300,
    #fffb00,
    #48ff00,
    #00ffd5,
    #002bff,
    #7a00ff,
    #ff00c8,
    #ff0000
  );
  position: absolute;
  top: -2px;
  left: -2px;
  background-size: 400%;
  z-index: -1;
  filter: blur(5px);
  width: calc(100% + 4px);
  height: calc(100% + 4px);
  animation: glowing 20s linear infinite;
  opacity: 0;
  transition: opacity 0.3s ease-in-out;
  border-radius: 10px;
}

.glow-on-hover:active {
  color: #000;
}

.glow-on-hover:active:after {
  background: transparent;
}

.glow-on-hover:hover:before {
  opacity: 1;
}

.glow-on-hover:after {
  z-index: -1;
  content: "";
  position: absolute;
  width: 100%;
  height: 100%;
  background: #111;
  left: 0;
  top: 0;
  border-radius: 10px;
}

div#lista-posts {
  color: #fff;
  letter-spacing: 0.1em;
  line-height: 1.5ch;
}
</style>
