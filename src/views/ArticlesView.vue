<template>
  <div>
    <h1>Articles list</h1>
    <button @click="fetchArticles()">Get all articles</button>
    <button @click="fetchArticles()">Get One</button>
    <button @click="fetchArticles()">Post</button>
    <button @click="delete_article()">Delete</button>

    <div v-for="item in articles" :key="item">
      <!-- Here be the list -->
      <!-- {{ item }} -->
      {{ item.id }}
      {{ item.title }}
      {{ item.description }}
      {{ item.price }}
      {{ item.currency }}
      {{ item.brand }}

      <p @click="modify_article(item.id)" style="background-color: lavender">
        Modify
      </p>
      <p @click="delete_article(item.id)" style="background-color: gold">
        Delete
      </p>
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
    .catch();
  //   console.log("response: " + response);
  console.log("Hello");
  console.log(response);
  let da_object = response;
  console.log(da_object);
  articles.value = da_object["articles"];
}

async function modify_article(id) {
  console.log("modify article " + id);
  let response = await fetch("http://127.0.0.1:3200/modify", {
    method: "POST",
  })
    .then((r) => r.json())
    .catch((e) => console.log(e));
}

async function delete_article(sent_id) {
  console.log("delete article " + sent_id);

  let response = await fetch("http://127.0.0.1:3200/delete/:" + sent_id , {
    method: "DELETE",
  })
    .then((r) => r.json())
    .catch();
}
</script>
