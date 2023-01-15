<template>
  <p>
    <RouterLink to="/new" class="btn btn-primary">New Post</RouterLink>
  </p>
  <div>
    <PostItem
      v-for="post of posts"
      :key="post.id"
      :post="post"
    />
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import { useStore } from "vuex";
import PostItem from "../components/PostItem.vue";

const store = useStore();

const posts = computed(() => store.state.posts);

// const onDelete = (post) => {
//   //   const index = posts.value.findIndex((p) => p.id === post.id);
//   //   posts.value.splice(index, 1);

//   // we can it like this too
//   posts.value = posts.value.filter((p) => p.id !== post.id);
// };
</script>