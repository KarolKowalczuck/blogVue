<script>
import { RouterLink } from "vue-router";

export default {
  props: {
    posts: Array,
  },
  data() {
    return {
      search: "",
      showModal: false,
      selectedPost: null,
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
    setupModal(id) {
      // mostrar e esconder o modal
      this.showModal = !this.showModal;

      //selecionar e desselecionar o post
      if (id) {
        //salva o post inteiro - titulo, data e conteudo
        this.selectedPost = this.posts[id];
        return;
      }
      this.selectedPost = null;
    },
    deletePost() {
      const id = this.getPostId(this.selectedPost.title);
      this.$emit("delete-post", id);

      //feche o modal e desselecione o post
      this.setupModal();
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
      <!-- Esse é o post com o id {{ getPostId(post.title) }} -->
      <div class="title-post">
        <RouterLink :to="`/detail/${getPostId(post.title)}`">
          <h3>
            {{ post.title }}
          </h3>
        </RouterLink>
        <div class="icons">
          <RouterLink :to="`/edit/${getPostId(post.title)}`">
            <span class="material-symbols-outlined">edit</span>
          </RouterLink>
          <span
            class="material-symbols-outlined"
            @click="setupModal(getPostId(post.title))"
            >delete</span
          >
        </div>
      </div>
      <h5 class="content-post date-time">{{ post.datetime }}</h5>
      <p class="content-post postcont">{{ post.content }}</p>
    </div>
  </div>

  <div class="modal" v-show="showModal">
    <div class="modal-content flex">
      <h3>Deletar Post</h3>
      <p>
        Você tem certeza que deseja deletar o post '{{ selectedPost?.title }}' ?
      </p>
      <div class="modal-actions">
        <button class="modal-bt cancel" @click="setupModal">Cancelar</button>
        <button class="modal-bt confirm" @click="deletePost">Confirmar</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
input {
  width: 30vw;
  color: #497e7e;
}

.material-symbols-outlined {
  color: #b6b8b8;
  font-size: 22px;
}
</style>
