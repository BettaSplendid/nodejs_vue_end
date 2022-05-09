<template>
  <div class="about">
    <form @submit.prevent>
      <p>
        <label for="fileinput">Put your file here</label>
        <input accept=".csv" type="file" name="fileinput" id="fileinput" />
        <button @click="submit()" type="submit">Submit</button>
      </p>
    </form>
  </div>
</template>

<script setup>
async function submit() {
  console.log("submit");
  let file = document.getElementById("fileinput").files[0];
  console.log(file);

  let the_form_data = new FormData();
  the_form_data.append("file", file);
  console.log(the_form_data);

  console.log(the_form_data.get('Username'));
  let response = await fetch("http://127.0.0.1:3200/csv", {
    method: "POST",
    headers: {
      "Content-Type": "text/csv",
    },
    file: the_form_data,
  })
    .then((r) => r.json())
    .catch();

  console.log(response);
}
</script>