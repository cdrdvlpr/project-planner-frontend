<template>
  <form @submit.prevent="handleSubmit">
    <div class="form-container">
      <label for="title">Title:</label>
      <input type="text" name="title" id="title" v-model="title" required />
      <label for="details">Details:</label>
      <textarea
        name="details"
        cols="30"
        rows="10"
        id="details"
        v-model="details"
        required
      ></textarea>
    </div>
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      uri: `https://project-planner-api.onrender.com/api/projects`,
      title: "",
      details: "",
    };
  },
  methods: {
    handleSubmit() {
      let project = {
        title: this.title,
        details: this.details,
        completed: false,
      };
      fetch(this.uri, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(project),
      })
        .then(() => this.$router.push("/"))
        .catch((error) => console.log(error));
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;300;400;500;600;700;800&display=swap");
form .form-container {
  background: #e2fddc77;
  padding: 2em;
  border-radius: 1em;
  max-width: 40em;
  margin: 2em auto;
  box-shadow: 1px 1px 10px 10px rgba(0, 0, 0, 0.05);
}
label {
  display: block;
  color: #303030;
  text-transform: uppercase;
  font-size: 1.4em;
  font-weight: bold;
  letter-spacing: 0.1em;
  margin: 1em 0 0.5em;
}
input {
  font-family: Poppins, sans-serif;
  font-size: 1.5em;
  padding: 0.5em;
  border: 0;
  border-radius: 0.25em;
  border-bottom: 0.1em solid #ddd;
  width: 100%;
}
textarea {
  font-family: Poppins, sans-serif;
  font-size: 1.25em;
  padding: 0.5em;
  width: 100%;
  height: 40vh;
  border: 0.1em solid #ddd;
  border-radius: 0.25em;
  resize: none;
}
form button {
  display: block;
  margin: 1em auto 2em;
  background: #00ce89;
  color: #fff;
  padding: 1em;
  border: 0;
  border-radius: 0.6em;
  font-size: 1.6em;
  cursor: pointer;
  transition: background 0.25s linear;
  box-shadow: 1px 1px 3px 3px rgba(0, 0, 0, 0.05);
}
form button:hover {
  background: #10da97;
}

/* responsive */
@media (max-width: 600px) {
  form .form-container {
    margin: 2em auto;
    max-width: 80%;
  }
}
</style>
