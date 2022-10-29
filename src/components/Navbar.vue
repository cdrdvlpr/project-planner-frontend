<template>
  <nav class="main-nav">
    <router-link :to="{ name: 'Home' }">Projects</router-link>
    <router-link :to="{ name: 'AddProject' }">Add a new Project</router-link>
  </nav>
</template>

<script>
export default {};
</script>

<style>
.main-nav {
  text-align: center;
  margin: 2em auto 1em;
}
.main-nav a {
  display: inline-block;
  margin: 0 1em;
  color: #ffffffda;
  font-size: 1.8em;
  transition: color 0.25s linear;
}
.main-nav a.router-link-active {
  color: #222;
}
.main-nav a:hover {
  color: #444;
}
</style>
