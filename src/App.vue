<script>
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "Meu primeiro post",
          datetime: Date.now(),
          content: "Postar aqui é muito legal",
        },
        {
          title: "Meu segundo post",
          datetime: Date.now(),
          content: "Postar aqui não é muito legal",
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

    handleInputChange(event) {
      const { name, value } = event.target;
      this.formData[name] = value;
    },
  },
};
</script>

<template>
  <div id="lista-posts" class="flex">
    <div class="post flex" v-for="post in posts" :key="post.key">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>

  <form action="" class="flex">
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

    <button type="button" @click="handleClick">Salvar</button>
  </form>

  <RouterView />
</template>

<style scoped>

template {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}

form {
  border: 2px solid blue;



}

form > * {
  margin: 1rem;
  background-color: whitesmoke;
}

#lista-posts {
  justify-content: center;
  align-items: center;
}

#lista-posts * {
  background-color: whitesmoke;
  color: rgb(36, 35, 35);
  

  
}
.post {
  border: 1px solid black;
  
  border-radius: 0px;
  background: #e0e0e0;
  box-shadow:  5px 5px 20px #5a5a5a,
             -5px -5px 20px #ffffff;

  width: 60vw;
  height: 30vh;
  justify-content: flex-start;
  align-items: flex-start;
  margin-block-end: 20px;
}

</style>
