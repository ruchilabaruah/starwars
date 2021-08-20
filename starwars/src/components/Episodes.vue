<template>
  <div class="episodesContainer">
    <div
      v-for="episode of filteredEpisodes"
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
    filter: {
      type: String,
      default: () => null,
    },
    sortBy: {
      type: Object,
      default: () => null,
    },
  },
  computed: {
    // First apply the filter, then sort the filtered list based on selected order
    filteredEpisodes() {
      const filteredList = this.list.filter((episode) => {
        return this.filter
          ? episode.fields.title
              .toLowerCase()
              .includes(this.filter.toLowerCase())
          : episode;
      });

      if (
        this.sortBy &&
        this.sortBy.id == "episode" &&
        this.sortBy.order == "-"
      ) {
        // Descending order of episodes
        filteredList.sort(
          (ep1, ep2) => ep2.fields.episode_id - ep1.fields.episode_id
        );
      } else if (
        this.sortBy &&
        this.sortBy.id == "episode" &&
        this.sortBy.order == "+"
      ) {
        // Ascending order of episodes
        filteredList.sort(
          (ep1, ep2) => ep1.fields.episode_id - ep2.fields.episode_id
        );
      } else if (
        this.sortBy &&
        this.sortBy.id == "date" &&
        this.sortBy.order == "-"
      ) {
        // Order by latest movies
        filteredList.sort(
          (ep1, ep2) =>
            new Date(ep2.fields.release_date).getTime() -
            new Date(ep1.fields.release_date).getTime()
        );
      } else if (
        this.sortBy &&
        this.sortBy.id == "date" &&
        this.sortBy.order == "+"
      ) {
        // Order by oldest movies
        filteredList.sort(
          (ep1, ep2) =>
            new Date(ep1.fields.release_date).getTime() -
            new Date(ep2.fields.release_date).getTime()
        );
      }
      console.log(filteredList);
      return filteredList;
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
