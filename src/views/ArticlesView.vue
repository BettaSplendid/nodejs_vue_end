<template>
  <div>
    <h1>Articles list</h1>
    <button @click="fetchArticles()">Get all articles</button>
    <button @click="fetchArticles()">Get One</button>
    <button @click="fetchArticles()">Post</button>
    <button @click="delete_article()">Delete</button>
    <br />
    <br />
    <hr />
    <br />
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
      <div v-if="modifying">
        Form below :
        <form
          @submit.prevent="handle_modify_submit(item)"
          style="display: flex; flex-direction: column"
        >
          <input v-model="item.id" name="title" />
          <input v-model="item.title" name="descrip" />
          <input v-model="item.description" name="currency" />
          <input v-model="item.price" name="price" />
          <input v-model="item.brand" name="brand" />
          <button type="submit">Submit</button>
        </form>
      </div>
      <br />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
const articles = ref([]);
const modifying = ref(false);

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

function modify_article(id) {
  console.log("modify article " + id);
  modifying.value = !modifying.value;
}

async function handle_modify_submit(item) {
  console.log("handle modify submit");
  let values = {
    id: item.id,
    title: item.title,
    description: item.description,
    price: item.price,
    currency: item.currency,
    brand: item.brand,
  };

  console.log(values);
  console.log(item.title);

  console.log("Sending");

  let response = await fetch("http://127.0.0.1:3200/modify", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(values),
  })
    .then()
    .catch();
  console.log(response);
  console.log("Sent request");
}

async function delete_article(sent_id) {
  console.log("delete article " + sent_id);

  let response = await fetch("http://127.0.0.1:3200/delete/:" + sent_id, {
    method: "DELETE",
  })
    .then((r) => r.json())
    .catch();
}
</script>
