<script>
import PostForm from "@/components/PostForm.vue";
export default {
  components: {
    PostForm
  }
}
</script>

<template>
  <PostForm />
</template>

<style scoped>
input {
  outline: none;
  border: none;

  margin-top: 10px;
  padding-left: 20px;
  height: 30px;
  width: 60vw;
  background-color: whitesmoke;
  font-size: 14px;
  border-radius: 50px;
  box-shadow: inset 6px 6px 6px #cbced1, inset -6px -6px 6px white;

  color: #497e7e;
  caret-color: #497e7e;

  margin-left: 20px;
}
</style>