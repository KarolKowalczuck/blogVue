<script>
import { RouterLink, RouterView } from "vue-router";
import "../src/assets/base.css";

export default {
  data() {
    return {
      posts: [
        {
          title: "Meu primeiro post",
          datetime: "18/05/2023",
          content: "Conteúdo do post.",
        },
        {
          title: "Meu segundo post",
          datetime: "18/05/2023",
          content: "Texto bem bacana.",
        },
      ],
    };
  },
  methods: {
    addPost(newPost) {
      //adicionar o novo post na lista de posts
      this.posts.push(newPost);
    },
    updatePost(updatedpost, id) {
      this.posts[id] = updatedpost;
    },
    removePost(id) {
      //como remover um post do array this.posts
      const minhaNovaLista = [];

      for (const index in this.posts) {
        if (index === id) {
          //não vou incluir ele na lista nova
          continue;
        }

        const post = this.posts[index];
        minhaNovaLista.push(post);
      }
      this.posts = minhaNovaLista;
    },
  },
};
</script>

<template>
  <header>
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/create">Novo Post</RouterLink>
    </nav>
  </header>

  <main>
    <RouterView
      :posts="posts"
      @create-post="addPost"
      @edit-post="updatePost"
      @delete-post="removePost"
    />
  </main>
</template>

<style scoped></style>
