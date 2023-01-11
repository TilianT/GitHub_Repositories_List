<template>
  <div class="repo-item">
    <div class="repo-item__header">
      <span class="repo-item__num">{{ repo.index+1 }}</span>
      <a :href="repo.html_url" target="_blank">{{ repo.full_name }}</a>
      <p>
        Stars:
        <span class="repo-item__stars">{{ repo.stargazers_count }}</span>
      </p>
    </div>
    <div class="repo-item__description">
      <p>{{ repo.description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    repo: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped lang="scss">
.repo-item {
  max-width: 580px;
  width: 100%;
  height: 100%;
  position: relative;

  text-align: left;

  background: rgba(236, 233, 255, 0.1);
  box-shadow: 1px 2px 2px #d6d6d6;
  border-radius: 8px;

  p {
    margin: 0;
  }

  &__header {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: flex-start;
    padding: 24px 14px 14px 14px;

    background-color: #dfe2fc;
    border-top-left-radius: 8px;
    border-top-right-radius: 8px;

    a {
      margin-bottom: 4px;

      font-size: 1.2rem;
    }
  }
  &__num,
  &__stars {
    font-weight: bold;

    color: #f9d696;
    background: rgba(148, 133, 248, 1);
    border-radius: 14px;
  }
  &__num {
    position: absolute;
    top: -5px;
    left: -10px;
    min-width: 50px;
    height: 20px;
    padding: 0 8px;

    text-align: center;
  }
  &__description {
    padding: 14px;
  }

  &__stars {
    padding: 4px 6px;

    font-size: 0.8rem;
  }
}
</style>
