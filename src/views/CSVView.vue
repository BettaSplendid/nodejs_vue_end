<template>
  <div class="about">
    <form @submit.prevent>
      <p>
        <label for="fileinput">Put your file here</label>
        <input accept=".csv" type="file" name="u" id="fileinput" />
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

  let formData = new FormData();
  //   formData.append('file', file);
  formData.append("name", "John");
  formData.append("password", "John123");
  console.log(formData);

  console.log(formData.get("name"));
  let response = await fetch("http://127.0.0.1:3200/csv", {
    method: "POST",
    headers: {
      "Content-Type": "multipart/form-data",
    },
    files: formData,
  })
    .then((r) => r.json())
    .catch();

  console.log(response);
}
</script>