<template>
  <div>
    <div v-if="episode">{{ episode.fields.title }}</div>
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
<style scoped></style>
