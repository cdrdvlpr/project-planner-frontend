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
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      uri: `https://project-planner-api.onrender.com/api/projects/${this.id}`,
      title: "",
      details: "",
    };
  },
  methods: {
    handleSubmit() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ title: this.title, details: this.details }),
      })
        .then(() => this.$router.push("/"))
        .catch((error) => console.log(error));
    },
  },
  mounted() {
    fetch(this.uri)
      .then((res) => res.json())
      .then((data) => {
        (this.title = data.title), (this.details = data.details);
      })
      .catch((error) => console.log(error));
  },
};
</script>
