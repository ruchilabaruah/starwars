<template>
  <div class="containere">
    <div class="sorter">
      <button @click="showSortPopover" class="target">Sort by...</button>
      <div v-if="sortPopoverOpen" class="popovercontainer">
        <div class="popoverHeader">
          <h5>Sort by</h5>
          <button type="button" class="btn" @click="hideSortPopover">
            Cancel
          </button>
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
    <input @change="searchEpisode" placeholder="Search by episode name..." />
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
      const selectedSorter =  this.sorterOptions.find(
        (curr) => curr.id == sortOption.id
      );
      selectedSorter.order = selectedSorter.order == "+" ? "-" : "+";
      // Create a new object because Vuejs sometimes fails to detect a key change in a prop of type "Object"
      this.$emit("sort", Object.assign({}, selectedSorter));
    },
  },
};
</script>
<style lang="scss" scoped>
$primaryColor: rgb(20, 24, 245);
$secondaryColor: #d3d3d3;
$baseSize: 4px;

.containere,
.popoverHeader {
  display: flex;
}
.containere {
  height: 50px;
  background-color: rgb(219, 216, 216);
  align-items: center;
  justify-content: center;
  padding: 0 10px;
}
.popoverHeader {
  justify-content: space-between;
  align-items: center;
  height: 40px;
}
button {
  height: 35px;
  width: 100px;
  color: $primaryColor;
  border: 1px solid $secondaryColor;
  border-radius: 3px;
}
input {
  height: 30px;
  width: 100%;
  border: 1px solid $secondaryColor;
  border-radius: 3px;
}
.target {
  position: relative;
}
.popovercontainer {
  position: absolute;
  background-color: #ffffff;
  z-index: 2;
  border-radius: 5px;
  border: 1px solid $secondaryColor;
  box-shadow: 1px 2px 2px $secondaryColor;
  width: 250px;
  height: 250px;
  margin-top: 3px;
}

.popovercontainer,
.sorterOptions {
  display: flex;
  flex-direction: column;
  text-align: left;
}
.popoverHeader,
.sortKey {
  border-bottom: 1px solid $secondaryColor;
  padding: 0 10px;
}
.sortKey {
  height: 35px;
  display: flex;
  align-items: center;
  &:hover {
    background-color: $secondaryColor;
  }
}
</style>
