<template>
  <div>
    <h1>Welcome to the login page</h1>
    <div v-if="error_mess">
      <h2>
        {{ error_mess }}
      </h2>
    </div>

    <form @submit.prevent>
      <p>
        <label for="email">Email:</label>
        <input v-model="email" type="text" name="" id="email" />
      </p>
      <p>
        <label for="password">Password:</label>
        <input v-model="password" type="text" name="" id="password" />
      </p>
      <button @click="start_login()" type="submit">Submit</button>
    </form>
  </div>
</template>
<script setup>
import { ref, onMounted } from "vue";

const error_mess = ref("");

onMounted(() => {
  console.log("mounted");
});

async function start_login() {
  console.log("start login");
  error_mess.value = "";
  let values = {
    email: email.value,
    password: password.value,
  };
  console.log(values);

  if (values.email == "") {
    // alert("Please enter an email");
    error_mess.value = "Please enter an email";
    return;
  }

  if (values.password == "") {
    // alert("Please enter a password");
    error_mess.value = "Please enter a password";
    return;
  }

    let response = await fetch("http://127.0.0.1:3200/login", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(values),
  })
    .then((r) => r.json())
    .catch();

  console.log(response);

}
</script>