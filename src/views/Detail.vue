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

  <textarea
    class="text-detail"
    readonly
    rows="30"
    cols="50"
    :value="post.content"
  >
  </textarea>
</template>

<style scoped>
.text-detail {
  resize: none;
  outline: none;
  border: none;
  width: 80%;
  min-width: fit-content;
  height: 600px;

  padding-top: 25px;
  padding-left: 25px;
  padding-right: 25px;
  margin-left: 10%;
  margin-right: 10%;
}

.detail-title {
  color: #559494;
  font-size: 30px;
  text-align: center;
}

.detail-date {
  color: rgb(116, 116, 116);
  text-align: end;
  font-weight: lighter;
}

body * {
  margin-left: 10%;
  margin-right: 10%;
}
</style>
