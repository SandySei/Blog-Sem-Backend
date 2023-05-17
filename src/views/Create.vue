<script>
export default {
  data() {
    return {
      formData: {
        title: "",
        content: "",
      },
    };
  },
  methods: {
    handleClick(event) {
      if (!this.formData.title) {
        alert("Preencha o Título do post ! \u2368");
        return;
      }

      const now = new Date();

      const dataDaPostagem = `${now.getDate()}/${
        now.getMonth() + 1
      }/${now.getFullYear()}`;

      const newPost = {
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      };

      //emitir o evento create-post
      this.$emit("create-post", newPost);

      this.formData = {
        title: "",
        content: "",
      };

      this.$router.push("/");
    },
    handleImputChange(event) {
      const { name, value } = event.target;
      this.formData[name] = value;
    },
  },
};
</script>

<template>
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
</template>
