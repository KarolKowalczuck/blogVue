<script>
export default {
    props: {
        post: Object,
    },
  data() {
    return {
      formData: {
        title: this.post?.title || "",
        content: this.post?.content || "",
      },
    };
  },
  methods: {
    handleCreatePost(event) {
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

  },
};
</script>

<template>
  <form action="" class="forms flex">
    <input v-model="formData.title" placeholder="Titulo" />

    <textarea
      v-model="formData.content"
      placeholder="Escreva seu post aqui.."
      id=""
      cols="30"
      rows="10"
    >
    </textarea>

    <button type="button" @click="handleCreatePost" class="flex">Salvar</button>
  </form>
</template>

<style scoped></style>
