<script>
import { RouterLink } from "vue-router";

export default {
  props: {
    posts: Array,
  },
  data() {
    return {
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
    getPostId(title) {
      // passa pela lista de posts - não filtrada
      for (const index in this.posts) {
        //acessa o post na poição index da lista de posts
        const post = this.posts[index];
        //verifica se o titulo do post atual é igual ao título buscado
        if (post.title === title) return index;
      }
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
    <div
      class="post flex"
      v-for="(post, index) in filteredPosts"
      :key="post.key"
    >
      <h3>
        {{ post.title }}
        <RouterLink :to="`/edit/${getPostId(post.title)}`">
          <span class="material-symbols-outlined">more_vert</span>
        </RouterLink>
      </h3>
      <h5>{{ post.datetime }}</h5>
      <p>{{ post.content }}</p>
    </div>
  </div>
</template>

<style scoped>
input {
  width: 30vw;
  color: #497e7e;
}
/* 
h3 {
  width: 95%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;

}

p {
  border: 1px solid red;

  width: 95%;
  height: 100%;
} */

</style>
