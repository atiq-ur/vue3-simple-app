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
import { useStore } from "vuex";

const route = useRoute();

const router = useRouter();

const store = useStore();

const model = ref({
  id: "",
  title: "",
  body: "",
});

onMounted(async () => {
  if (route.params.id) {
    const post = await store.dispatch("getSinglePost", route.params.id);
    model.value = post;
  } else {
    return;
  }
});

const onSubmit = () => {
  store.dispatch("savePost", model.value).then(() => {
    router.push("/");
  });
};
</script>