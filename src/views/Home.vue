<template>
  <div>
    <SearchArea />
    <div id="search-body">
      <ul>
        <li v-for="location in locations" v-bind:key="location">{{ location }}</li>
      </ul>
      <JobList v-bind:jobs="jobs" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import JobList from "@/components/JobList.vue";
import SearchArea from "@/components/SearchBox.vue";
import axios from "axios";

export default {
  name: "Home",
  components: {
    JobList,
    SearchArea,
  },
  data() {
    return {
      jobs: [],
      locations: [],
    };
  },
  created() {
    axios
      .get(
        "https://cors-anywhere.herokuapp.com/https://jobs.github.com/positions.json?page=1"
      )
      .then((response) => {
        response.data.forEach((item) => {
          this.jobs.push(item);

          if (!this.locations.find((location) => location === item.location)) {
            this.locations.push(item.location);
          }
        });
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style scoped>
#search-body {
  display : flex;
  justify-content: space-between;
}
li {
  list-style-type: none;
  text-align: left;
}
</style>
