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
    <input
      class="search"
      v-model="formData.title"
      placeholder="Escreva seu Título aqui ..."
    />
    <textarea
      name="content"
      :value="formData.content"
      @keyup="handleImputChange"
      placeholder="Escreva seu Post aqui ..."
      class="search"
      cols="30"
      rows="10"
    >
    </textarea>

    <button type="button" @click="handleClick">SALVAR</button>
  </form>
</template>

<style scoped>

form {
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  background: linear-gradient(
    280deg,
    rgba(5, 237, 254, 1) 0%,
    rgba(78, 172, 254, 1) 100%
  );
  border-radius: 0.5em;
  margin: 1rem;
  padding: 8px;
}

input {
  font-family: "coolvetica condensed";
  width: 90%;
  height: 30px;
}

textarea {
  width: 90%;
  height: 130px;
  resize: none;
  font-family: "coolvetica condensed";
}
.search {
  border: none;
  outline: none;
  color: #00000094;
  background: #f0f0f0;
  font-size: 0.9em;
  padding-left: 10px;
  border-radius: 0.5em;
  letter-spacing: 2px;
}

.search:focus {
  border-radius: 0.5em;
  box-shadow: inset 1.5px 1px 1px 1px rgb(73, 155, 228);
}

button {
  font-family: "coolvetica condensed";
  font-weight: 50;
  font-size: 17px;
  text-align: center;
  color: #797979;
  cursor: pointer;
  max-width: 100px;
  width: 100%;
  outline: 2px solid;
  border: none;
  border-radius: 0.5em;
  outline-color: rgba(78, 172, 254, 1);
  outline-offset: 0px;
  transition: all 600ms cubic-bezier(0.2, 0, 0, 0.8);
}

button:hover {
  color: rgba(78, 172, 254, 1);
  outline-color: rgba(71, 126, 232, 0);
  outline-offset: 30px;
}

button:focus {
  box-shadow: inset 1.5px 1px 1px 1px rgb(73, 155, 228);
}
</style>
