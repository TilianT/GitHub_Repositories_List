<template>
  <div class="container">
    <p class="error" v-show="errorMessage !== ''">
      {{ errorMessage }}
    </p>
    <div class="repo-list" ref="reposContainer">
      <RepoItem v-for="(repo, index) in postsList" :repo="repo" :key="index" />
    </div>
    <Loader v-show="isLoading" />
  </div>
</template>

<script>
import axios from "axios";
import { onMounted, onUnmounted, ref } from "vue";
import RepoItem from "./RepoItem.vue";
import Loader from "./Loader.vue";

export default {
  components: {
    RepoItem,
    Loader,
  },
  setup() {
    const postsList = ref([]);
    const currentPage = ref(1);
    const isLoading = ref(true);
    const errorMessage = ref("");
    const URL_GitHub = "https://api.github.com/search/repositories";
    const reposContainer = ref(null);

    const loadPosts = async () => {
      isLoading.value = true;
      try {
        const { data } = await axios.get(`${URL_GitHub}?q=javascript+in:language&sort=stars&order=desc&page=${currentPage.value}&per_page=10`);
        postsList.value.push(...data.items);
        currentPage.value++;
      } catch (error) {
        console.error(`Error message: `, error.message);
        errorMessage.value = error.message;
      } finally {
        isLoading.value = false;
      }
    };

    const handleScroll = () => {
      const block = reposContainer.value;
      if (
        block.getBoundingClientRect().bottom < window.innerHeight &&
        !isLoading.value
      ) {
        loadPosts();
      }
    };

    onMounted(() => {
      loadPosts();
      window.addEventListener("scroll", handleScroll);
    });
    onUnmounted(() => {
      window.removeEventListener("scroll", handleScroll);
    });

    return {
      postsList,
      isLoading,
      reposContainer,
      errorMessage,
    };
  },
};
</script>

<style scoped lang="scss">
.container {
  padding-bottom: 25px;
}
.repo-list {
  display: grid;
  gap: 16px;
  grid-auto-columns: minmax(100%, 500px);
  justify-items: center;
  margin-bottom: 10px;
}
</style>
