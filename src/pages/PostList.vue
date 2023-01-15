<template>
  <p>
    <RouterLink to="/new" class="btn btn-primary">New Post</RouterLink>
  </p>
  <div>
    <PostItem
      v-for="post of posts"
      :key="post.id"
      :post="post"
      @delete="onDelete"
    />
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import PostItem from "../components/PostItem.vue";

const posts = ref([]);

onMounted(() => {
  fetch("https://jsonplaceholder.typicode.com/posts")
    .then((res) => res.json())
    .then((data) => {
      posts.value = data;
    });
});

const onDelete = (post) => {
  //   const index = posts.value.findIndex((p) => p.id === post.id);
  //   posts.value.splice(index, 1);

  // we can it like this too
  posts.value = posts.value.filter((p) => p.id !== post.id);
};
</script>