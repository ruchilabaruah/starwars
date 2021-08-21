<template>
  <div class="container">
    <TableOptimizer class="searchbox" @filter="searchEpisode" @sort="sortBy" />
    <Episodes
      class="episodes"
      :list="starWars"
      @select="selectEpisode"
      :filter="filterText"
      :sortBy="sortKey"
    />
    <Episode class="episode" :episode="episode" />
  </div>
</template>
<script lang="ts">
import TableOptimizer from "./TableOptimizer.vue";
import Episodes from "./Episodes.vue";
import Episode from "./Episode.vue";
/*
 * Container for showing searchbox, movie list and description of selected episode.
 */
export default {
  name: "star-wars",
  components: {
    TableOptimizer,
    Episodes,
    Episode,
  },
  data() {
    return {
      starWars: [],
      episode: null,
      filterText: null,
      sortKey: null,
    };
  },
  methods: {
    /** Once component is mounted, make this api call to fetch the movie list */
    async getStarWarsList() {
      try {
        const promiseData = await fetch(
          "https://star-wars-api.herokuapp.com/films"
        );
        this.starWars = await promiseData.json();
        console.log(this.starWars);
      } catch (err) {
        console.log("Error!");
      }
    },
    /** Select episode */
    selectEpisode(episode) {
      this.episode = episode ? episode : null;
    },
    /** Table to be filtered based on this entered text*/
    searchEpisode(value) {
      this.filterText = value;
    },
    /** Table to be sorted based on sort by key selected */
    sortBy(value) {
      this.sortKey = value;
    },
  },
  mounted() {
    this.getStarWarsList();
  },
};
</script>
<style lang="scss" scoped>
.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
.searchbox {
  grid-row: 1;
  grid-column: 1 / 3;
}
.episodes {
  grid-row: 2;
  grid-column: 1 / 2;
}
.episode {
  grid-row: 2;
}
</style>
