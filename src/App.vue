<script>
import { RouterLink, RouterView } from "vue-router";
import "../src/assets/base.css";

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
      search: "",
    };
  },
  computed: {
    filteredPosts() {
      // se search estiver vazio, retorne a lista completa de posts
      if (!this.search) return this.posts;

      // se tiver qualquer coisa em search, faz o filtro
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

    handleInputChange(event) {
      const { name, value } = event.target;
      this.formData[name] = value;
    },
  },
};
</script>

<template>
  <input
    v-model="search"
    placeholder="Procure pelo título do post..."
    class="search"
  />

  <div id="lista-posts" class="flex">
    <div class="post flex" v-for="post in filteredPosts" :key="post.key">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>

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
.post {
  /* border: 1px solid rgb(54, 54, 54); */
  
  border-radius: 30px;
  background: #e0e0e0;
  box-shadow: 5px 5px 20px #5a5a5a, -5px -5px 20px #ffffff;
  
  width: 60vw;
  height: 30vh;
  justify-content: flex-start;
  align-items: flex-start;
  margin-block-end: 20px;
}

#lista-posts {
  justify-content: center;
  align-items: center;
}

#lista-posts * {
  background-color: whitesmoke;
  color: rgb(36, 35, 35);
  

  
}

form > * {
  margin: 1rem;
  background-color: whitesmoke;
  border: none;
}

textarea {
  padding: 10px;
  padding-left: 20px;
  height: 250px;
  width: 60vw;
  font-size: 16px;
  color: rgb(54, 54, 54);
  border-radius: 30px;
  box-shadow: inset 6px 6px 6px #cbced1, inset -6px -6px 6px white;
}


button {
  background-color: whitesmoke;
  font-size: 16px;
  font-family: 'Montserrat', sans-serif;
  color: rgb(54, 54, 54);

  position: relative;
  width: 200px;
  height: 100px;
  border-radius: 150px;
  align-items: center;
  justify-content: center;

  
}

button:before {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  display: block;
  width: 200px;
  height: 100px;
  content: " ";
  cursor: pointer;
  transition: 0.3s ease-out;
  border-radius: 150px;
  filter: blur(7px);
  box-shadow: 8px 8px 20px #747475, -8px -8px 20px #fff;

}

button:hover:before {
  box-shadow: 8px 8px 20px #747475, -8px -8px 20px #fff,
  inset -8px -8px 20px #fff, inset 8px 8px 20px #747475;

  /* transition: 0.3s ease-in;
  transform: scale(1.1); */
}
</style>
