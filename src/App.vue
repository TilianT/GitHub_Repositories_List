<template>
  <h1>Top of Github JavaScript repositories</h1>
  <RepoList />
</template>

<script>
import RepoList from "./components/RepoList.vue";

export default {
  name: "App",
  components: {
    RepoList,
  },
};
</script>

<style lang="scss">
*,
body {
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  font-size: 16px;
  color: #374451;
  margin-top: 20px;
}
.error {
  font-size: 1.5rem;

  color: rgb(230, 3, 3);
}
</style>
