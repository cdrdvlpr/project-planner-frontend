<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current" />
    <button class="toggle-blur" @click="toggleBlur">
      Toggle Blur for Completed Projects
    </button>
    <div class="blurred" ref="projects" v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project._id">
        <SingleProject
          :project="project"
          @delete="handleDelete"
          @completed="handleCompleted"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from "@/components/SingleProject.vue";
import FilterNav from "@/components/FilterNav.vue";

export default {
  name: "Home",
  components: { SingleProject, FilterNav },
  computed: {
    filteredProjects() {
      if (this.current === "completed") {
        return this.projects.filter((project) => project.completed);
      } else if (this.current === "ongoing") {
        return this.projects.filter((project) => !project.completed);
      }
      return this.projects;
    },
  },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  methods: {
    toggleBlur() {
      if (this.$refs.projects.classList.contains("not-blurred")) {
        this.$refs.projects.classList.remove("not-blurred");
        this.$refs.projects.classList.add("blurred");
      } else if (this.$refs.projects.classList.contains("blurred")) {
        this.$refs.projects.classList.remove("blurred");
        this.$refs.projects.classList.add("not-blurred");
      }
    },
    handleDelete(id) {
      this.projects = this.projects.filter((project) => {
        return project._id !== id;
      });
    },
    handleCompleted(id) {
      let p = this.projects.find((project) => {
        return project._id === id;
      });
      p.completed = !p.completed;
    },
  },
  mounted() {
    fetch("https://project-planner-api.onrender.com/api/projects")
      .then((res) => res.json())
      .then((data) => (this.projects = data.sort((a, b) => -1)))
      .catch((error) => console.log(error));
  },
};
</script>

<style>
.home {
  margin-bottom: 4em;
}
button.toggle-blur {
  display: block;
  background: #ffffff46;
  padding: 0.5em 1em;
  border-radius: 0.5em;
  font-family: Quicksand;
  font-size: 1em;
  border: none;
  margin: 2em auto;
  cursor: pointer;
  transition: all 0.25s linear;
  box-shadow: 1px 1px 5px 5px rgba(0, 0, 0, 0.1);
}
button.toggle-blur:hover {
  background: #ffffff8b;
}
</style>
