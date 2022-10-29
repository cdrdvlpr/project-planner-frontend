<template>
  <Navbar />
  <router-view />
  <Footer />
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Footer from "@/components/Footer.vue";
export default {
  components: {
    Navbar,
    Footer,
  },
};
</script>

<style>
/* google font */
@import url("https://fonts.googleapis.com/css2?family=Quicksand:wght@300;400;500;600;800&family=VT323&display=swap");
/* custom scrollbar */
::-webkit-scrollbar {
  width: 0.3em;
}
::-webkit-scrollbar-thumb {
  border-radius: 0.5em;
  background: #13acf373;
}
::-webkit-scrollbar-thumb:hover {
  width: 0.3em;
  background: #00a6f3a4;
}

/* general resets */
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
html {
  font-size: 62.5%;
  min-height: 100vh;
}
body {
  font-family: "Quicksand", sans-serif;
  width: 100%;
  cursor: default;
  font-size: 2em;
  position: relative;
  margin: 0 auto;
  color: #111;
  background: radial-gradient(at top left, #7dd56fd9 0%, #28b487d9 100%);
}
p,
a,
ul,
li,
div {
  text-decoration: none;
  list-style-type: none;
}
a {
  color: #000;
}
div#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

/* responsive */
@media (max-width: 900px) {
  body {
    font-size: 1.5em;
  }
}
@media (max-width: 600px) {
  body {
    font-size: 1em;
  }
}
@media (max-width: 400px) {
  body {
    font-size: 0.9em;
  }
}
</style>
