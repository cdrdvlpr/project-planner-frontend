<template>
  <div class="project" :class="{ completed: project.completed }">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icons">
        <CIcon @click="toggleCompleted" class="icon check" :icon="cilCheck" />
        <router-link :to="{ name: 'EditProject', params: { id: project._id } }">
          <CIcon class="icon" :icon="cilPen" />
        </router-link>
        <div>
          <CIcon @click="deleteProject" class="icon trash" :icon="cilTrash" />
        </div>
      </div>
    </div>
    <div v-if="showDetails" class="details">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
import { CIcon } from "@coreui/icons-vue";
import { cilTrash, cilPen, cilCheck } from "@coreui/icons";
export default {
  components: { CIcon },
  data() {
    return {
      showDetails: false,
      uri: `https://project-planner-api.onrender.com/api/projects/${this.project._id}`,
      cilTrash,
      cilPen,
      cilCheck,
    };
  },
  methods: {
    deleteProject() {
      fetch(this.uri, { method: "DELETE" })
        .then(() => this.$emit("delete", this.project._id))
        .catch((error) => console.log(error));
    },
    toggleCompleted() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ completed: !this.project.completed }),
      })
        .then(() => this.$emit("completed", this.project._id))
        .catch((error) => console.log(error));
    },
  },
  props: ["project"],
};
</script>

<style>
.project {
  max-width: 800px;
  margin: 1.5em auto;
  background: #ffe8eb4c;
  padding: 1em 2em;
  border-radius: 0.4em;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.05);
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
  border-left: 0.4em solid #c84e8b;
}
.project.completed {
  border-left: 0.4em solid #00ce89;
  background: #e9ffd768;
}
.blurred .project.completed {
  filter: blur(15px);
  transition: all 0.1s linear;
}
.not-blurred .project.completed {
  filter: blur(0);
  transition: all 0.1s linear;
}
.project.completed:hover {
  filter: blur(0);
}
.project.completed .icons .icon.check {
  color: #00ce89;
}
h3 {
  cursor: pointer;
  max-width: 75%;
  overflow: hidden;
}
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.icons {
  border: 1px solid #ffffff7a;
  border-radius: 20%;
  padding: 0.1em;
  text-align: center;
  transition: all 0.1s linear;
}
.icons:hover {
  box-shadow: 1px 1px 25px rgba(255, 255, 255, 0.5);
}
.icons .icon {
  width: 1em;
  margin: 0 0.1em;
  color: #555;
  border-radius: 35%;
  padding: 5px;
  box-sizing: content-box;
  transition: all 0.1s linear;
}
.icons .icon:hover {
  color: #222;
  cursor: pointer;
  background: #ffffff9f;
}
.icons .icon.trash {
  color: #ff4545c2;
}
.icons .icon.trash:hover {
  color: #ff4545;
}
.details {
  position: relative;
  margin-top: 0.5em;
  padding-top: 0.5em;
  white-space: pre-line; /* Cool! Fix for textarea line breaks*/
  overflow: hidden;
}
.details::before {
  content: "";
  position: absolute;
  width: 33.33%;
  height: 1px;
  background: #778877aa;
  top: 0;
  left: 0;
}

/* responsive */
@media (max-width: 900px) {
  body .project {
    max-width: 80%;
  }
}
</style>
