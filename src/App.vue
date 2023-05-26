<script>
import { RouterLink, RouterView } from "vue-router";
import "../src/assets/base.css";

export default {
  data() {
    return {
      posts: [
        {
          title: "Chocolate",
          datetime: "24/05/2023",
          content: "O chocolate ajuda a prevenir o envelhecimento. A semente de cacau é composta por antioxidantes que têm propriedades antienvelhecimento.",
        },
        {
          title: "Brigadeiro",
          datetime: "25/05/2023",
          content:"É um doce tipicamente brasileiro, que foi criado em 1940 no Rio Grande do Sul. Era inicialmente chamado de negrinho, possui o nome de Brigadeiro devido a uma campanha eleitoral.",
        },
        {
          title: "Cookies",
          datetime: "26/05/2023",
          content: "Você sabia que a palavra cookie vem do alemão, koekje, que significa “pequeno bolo”? Ganhou esse nome porque era, naquele tempo, feita a partir da massa de um bolo e usada para testar a temperatura do forno antes de colocar o bolo inteiro para assar.",
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
