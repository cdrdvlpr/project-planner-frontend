<template>
  <footer>
    Copyright &copy; 2020-{{ now.getFullYear() }}. Mahmoud Kebbeh, All rights reserved.
  </footer>
</template>

<script>
export default {
  name: "Footer",
  data() {
    return {
      now: new Date(),
    };
  },
};
</script>

<style>
footer {
  margin-top: auto;
  font-size: 0.75em;
  width: 100%;
  bottom: 0;
  background: #eaeaea67;
  text-align: center;
  padding: 0.5em;
  color: #111;
  font-weight: bold;
  z-index: 3;
  transition: all 0.3s ease;
}
</style>
