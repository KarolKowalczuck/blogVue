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
