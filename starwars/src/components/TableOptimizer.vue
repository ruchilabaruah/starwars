<template>
  <div class="containere">
    <div class="sorter">
      <button @click="showSortPopover">Sort by...</button>
      <!-- TODO: Change CSS for the popover. Functionality works. -->
      <div v-if="sortPopoverOpen" class="popovercontainer">
        <div>
          <h5>Sort by</h5>
          <button @click="hideSortPopover">Cancel</button>
        </div>
        <div class="sorterOptions">
          <div
            v-for="(sorter, index) of sorterOptions"
            :key="index"
            @click="sortBy(sorter)"
            class="sortKey"
          >
            {{ sorter.name }}
          </div>
        </div>
      </div>
    </div>
    <input @change="searchEpisode" />
  </div>
</template>
<script>
/** Component for selecting sortby option and filter text */
export default {
  name: "table-optimizer",
  data() {
    return {
      sortPopoverOpen: false,
      sorterOptions: [
        { name: "Episode", order: "+", id: "episode" },
        { name: "Year", order: "+", id: "year" },
      ],
    };
  },
  methods: {
    /** Table to be filtered based on this entered text*/
    searchEpisode(ev) {
      this.$emit("filter", ev.target.value);
    },
    showSortPopover() {
      this.sortPopoverOpen = true;
    },
    hideSortPopover() {
      this.sortPopoverOpen = false;
    },
    /** Table to be sorted based on sort by key selected */
    sortBy(sortOption) {
      const sorter = this.sorterOptions.find(
        (sorter) => sorter.id == sortOption.id
      );
      sorter.order = sorter.order == "+" ? "-" : "+";
      this.$emit("sort", sorter);
    },
  },
};
</script>
<style lang="scss" scoped>
.containere {
  display: flex;
}
.popovercontainer,
.sorterOptions {
  display: flex;
  flex-direction: column;
}
.sortKey {
  border-bottom: 1px solid red;
}
</style>
