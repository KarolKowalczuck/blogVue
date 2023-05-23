<script>
export default {
  props: {
    posts: Array,
  },
  data() {
    //acessa o parametro id uma unica vez
    const id = this.$route.params.id;

    return {
      //expondo a variavel id para ser acessivel no template
      id: id,
      post: this.posts[id],
    };
  },
};
</script>

<template>
  <h2 class="detail-title">
    {{ post.title }}
  </h2>
  <h5 class="detail-date">{{ post.datetime }}</h5>

  <textarea readonly rows="30" cols="50" :value="post.content"> </textarea>
</template>

<style scoped>
textarea {
  resize: none;
  outline: none;
  border: none;

  width: 60%;
  height: fit-content;
}

body * {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  border: 1px solid salmon;
}
</style>
