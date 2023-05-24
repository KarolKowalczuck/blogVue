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
    handleCreatePost(event) {
      if (!this.formData.title) {
        alert("Preencha o título do post");
        return;
      }

      const now = new Date();

      const dataDaPostagem = `${now.getDate()}/${
        now.getMonth() + 1
      }/${now.getFullYear()} - ${now.getHours()}:${now.getMinutes()}`;

      // método 1:
      //this.post[this.posts.length] = {
      //title: this.formData.title,
      //content: this.formData.conteny,
      // }

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

      // this.formData = {
      //   title: "",
      //   content: "",
      // };

      this.$router.push("/");
    },
  },
};
</script>

<template>
  <form action="" class="forms flex">
    <input
      class="title"
      v-model="formData.title"
      placeholder="Titulo"
      maxlength="30"
    />

    <textarea
      v-model="formData.content"
      placeholder="Escreva seu post aqui.."
      id=""
      class="text-form"
      cols="30"
      rows="10"
      maxlength="1000"
    >
    </textarea>

    <button type="button" @click="handleCreatePost" class="flex form-button">
      Salvar
    </button>
  </form>
</template>

<style scoped>
input {
  outline: none;
  border: none;

  margin-top: 10px;
  padding-left: 20px;
  height: 35px;
  width: 60vw;
  background-color: whitesmoke;
  font-size: 14px;
  border-radius: 50px;
  box-shadow: inset 6px 6px 6px #cbced1, inset -6px -6px 6px white;

  color: #3d3d3d;
  caret-color: #497e7e;

  margin-left: 20px;
}

.title {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;

  font-size: 18px;
}

textarea {
  word-break: auto;
}

.form-button {
  width: 200px;
  height: 100px;
}

.form-button ::before {
  width: 200px;
  height: 100px;
}
</style>
