<script>
import { RouterLink, RouterView } from "vue-router";
import "../src/assets/base.css";

export default {
  data() {
    return {
      posts: [
        // {
        //   title: "Meu primeiro post",
        //   datetime: Date.now(),
        //   content: "Postar aqui é muito legal",
        // },
        // {
        //   title: "Meu segundo post",
        //   datetime: Date.now(),
        //   content: "Postar aqui não é muito legal",
        // },
      ],
    };
  },
  methods: {
    addPost(newPost) {
      this.posts.push(newPost);
    },
  },
};
</script>

<template>
  <RouterLink to="/">Home</RouterLink>
  <RouterLink to="/create">Novo Post</RouterLink>

  <RouterView :posts="posts" @create-post="addPost" />
</template>

<style scoped>
* {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
</style>
