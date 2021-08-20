<template>
  <div class="container">
    <Episodes :list="starWars" @select="selectEpisode" />
    <Episode :episode="episode" />
  </div>
</template>
<script lang="ts">
import Episodes from "./Episodes.vue";
import Episode from "./Episode.vue";
/*
 * Container for showing searchbox, movie list and description of selected episode.
 */
export default {
  name: "star-wars",
  components: {
    Episodes,
    Episode,
  },
  data() {
    return {
      starWars: [],
      episode: null,
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
  },
  mounted() {
    this.getStarWarsList();
  },
};
</script>
<!--TODO: Use SCSS if needed -->
<style scoped>
.container {
  display: grid;
  grid-template-columns: auto auto;
  /* background-color: red; */
}
</style>
