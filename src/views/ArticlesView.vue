<template>
  <div>
    <h1>Articles list</h1>
    <button @click="fetchArticles()">Function</button>
    <div v-for="(item) in articles" :key="item">
      <!-- Here be the list -->
      <!-- {{ item }} -->
      {{ item.id }}
      {{ item.title }}
      {{ item.description }}
      {{ item.price }}
      {{ item.currency }}
      {{ item.brand }}


    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
const articles = ref([]);

async function fetchArticles() {
  console.log("fetching articles");
  let response = await fetch("http://127.0.0.1:3200", {
    method: "GET",
  })
    .then((r) => r.json())
    .catch(console.log("error"));
//   console.log("response: " + response);
//   console.log(response)
  let da_object = JSON.parse(response);
  console.log(da_object);
  articles.value = da_object['articles'];
}
</script>
