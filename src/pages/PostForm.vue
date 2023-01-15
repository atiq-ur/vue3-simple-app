<template>
  <p>
    <RouterLink to="/" class="btn btn-outline-secondary"
      >Back to post List</RouterLink
    >
  </p>
  <div>
    <form @submit.prevent="onSubmit">
      <h1>{{ model.id ? "Edit Post" : "Create new Post" }}</h1>

      <div class="mb-3">
        <input
          type="text"
          v-model="model.title"
          class="form-control"
          placeholder="Post title"
        />
      </div>

      <div class="mb-3">
        <textarea
          type="text"
          v-model="model.body"
          rows="5"
          class="form-control"
          placeholder="Post body"
        />
      </div>
      <p>
        <button
          :disabled="!model.title || !model.body"
          type="submit"
          class="btn btn-success"
        >
          Submit
        </button>
      </p>
    </form>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute, useRouter } from "vue-router";

const route = useRoute();

const router = useRouter();

const model = ref({
  id: "",
  title: "",
  body: "",
});

onMounted(() => {
  if (route.params.id) {
    fetch(`https://jsonplaceholder.typicode.com/posts/${route.params.id}`)
      .then((res) => res.json())
      .then((post) => {
        model.value = post;
      });
  }
});

const onSubmit = () => {
  const method = model.value.id ? "PUT" : "POST";
  const url = model.value.id
    ? `https://jsonplaceholder.typicode.com/posts/${model.value.id}`
    : "https://jsonplaceholder.typicode.com/posts";

  fetch(url, {
    method,
    body: JSON.stringify(model.value),
    headers: {
      "Content-type": "application/json; charset=UTF-8",
    },
  })
    .then((res) => res.json())
    .then((post) => {
      router.push("/");
    });
};
</script>