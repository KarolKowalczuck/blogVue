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
        alert("Preencha o título do post");
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

      this.$emit("create-post", newPost);

      this.formData = {
        title: "",
        content: "",
      };

      this.$router.push("/");
    },
    handleInputChange(event) {
      const { name, value } = event.target;
      this.formData[name] = value;
    },
  },
};
</script>

<template>
  <form action="" class="forms flex">
    <input v-model="formData.title" placeholder="Titulo" />

    <textarea
      name="content"
      :value="formData.content"
      placeholder="Escreva seu post aqui.."
      @keyup="handleInputChange"
      id=""
      cols="30"
      rows="10"
    >
    </textarea>

    <button type="button" @click="handleClick" class="flex">Salvar</button>
  </form>
</template>

<style scoped>
input {
  outline: none;
  border: none;

  margin-top: 10px;
  padding-left: 20px;
  height: 30px;
  width: 60vw;
  background-color: whitesmoke;
  font-size: 14px;
  border-radius: 50px;
  box-shadow: inset 6px 6px 6px #cbced1, inset -6px -6px 6px white;

  color: #497e7e;
  caret-color: #497e7e;

  margin-left: 20px;
}
</style>