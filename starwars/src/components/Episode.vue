<template>
  <div>
    <div v-if="episode" class="episode">
      <h3>{{ episode.fields.title }}</h3>
      <p class="description">{{ episode.fields.opening_crawl }}</p>
      <p>Directed by: {{ episode.fields.director }}</p>
    </div>
    <div v-else>No episode selected</div>
  </div>
</template>
<script>
/**
 * Container showing the description of selected episode from the list
 */
export default {
  name: "episode",
  props: {
    episode: {
      type: Object,
      default: () => {},
    },
  },
};
</script>
<style scoped>
.episode {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: 20px;
}
.description {
  text-align: left;
}
</style>
