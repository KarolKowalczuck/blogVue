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
      ],
    };
  },
  methods: {
    addPost(newPost) {
      this.posts.push(newPost);
    },
    updatePost(updatedpost, id) {
      this.posts[id] = updatedpost;
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
    <RouterView :posts="posts" @create-post="addPost" @edit-post="updatePost" />
  </main>
</template>

<style scoped>

</style>
