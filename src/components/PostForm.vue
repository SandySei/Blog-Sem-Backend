<script>
export default {
  props: {
    post: Object,
    id: String,
  },
  data() {
    return {
      formData: {
        title: this.post?.title || "",
        content: this.post?.content || "",
      },
      isEditing: Boolean(this.post),
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
      }/${now.getFullYear()} - ${now.getHours()}:${now.getMinutes()}:${now.getSeconds()}`;

      const postData = {
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      };

      if (this.isEditing) {
        this.$emit("edit-post", postData, this.id);
      } else {
        this.$emit("create-post", postData);
      }

      /*this.formData = {
        title: "",
        content: "",
      };*/

      this.$router.push("/");
    },
  },
};
</script>

<template>
  <form>
    <input
      class="search"
      v-model="formData.title"
      placeholder="Escreva seu Título aqui ..."
    />
    <textarea
      v-model="formData.content"
      placeholder="Escreva seu Post aqui ..."
      class="search"
      cols="30"
      rows="10"
    >
    </textarea>

    <button type="button" @click="handleClick">SALVAR</button>
  </form>
</template>
