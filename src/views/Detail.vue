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
  <h2>
    {{ post.title }}
  </h2>
  <h4>{{ post.datetime }}</h4>

  <textarea readonly :value="post.content"> </textarea>
</template>

<style scoped>
textarea {
  resize: none;
  outline: none;
  border: none;

  width: 80%;
}
</style>
