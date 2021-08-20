<template>
  <div class="episodesContainer">
    <div
      v-for="episode of list"
      :key="episode.id"
      class="episode"
      @click="selectEpisode(episode)"
    >
      <div class="id">EPISODE {{ episode.fields.episode_id }}</div>
      <div class="title">{{ episode.fields.title }}</div>
      <div class="releasedate">{{ episode.fields.release_date }}</div>
    </div>
  </div>
</template>
<script lang="ts">
/**
 * Container showing the list of episodes
 */
export default {
  name: "episodes",
  props: {
    list: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    /** Emit the selected episode to the parent component*/
    selectEpisode(episode) {
      this.$emit("select", episode);
    },
  },
};
</script>
<style lang="scss" scoped>
.episodesContainer {
  border-right: 1px solid #d3d3d3;
}
.episode {
  display: flex;
  height: 50px;
  border-bottom: 1px solid #d3d3d3;
  text-align: left;
  align-items: center;
  cursor: pointer;
  .id {
    flex-basis: 200px;
  }
  .title {
    flex-basis: 400px;
  }
  .releasedate {
    flex-basis: 200px;
  }
}
</style>
