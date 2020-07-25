<template>
  <div>
    <SearchArea class="shadow" />
    <div id="search-body">
      <div id="left-sidebar">
        <input type="checkbox" name="full-time" />
        <label for="full-time">Full Time</label>
        <br />
        <br />
        <label for="location">Location</label>
        <input class="shadow" type="text" name="location" placeholder="City, state, zipcode, or country" />
        <ul>
          <li>
            <div class="location-cb">
              <input type="checkbox" name="worldwide" />
              <label for="worldwide">Worldwide</label>
            </div>
          </li>
          <li>
            <div class="location-cb">
              <input type="checkbox" name="usa" />
              <label for="usa">USA</label>
            </div>
          </li>
          <li>
            <div class="location-cb">
              <input type="checkbox" name="remote" />
              <label for="remote">Remote</label>
            </div>
          </li>
          <li>
            <div class="location-cb">
              <input type="checkbox" name="austin" />
              <label for="austin">Austin, TX</label>
            </div>
          </li>
        </ul>
      </div>
      <JobList class="joblist" v-bind:jobs="jobs" />
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
        });
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style scoped>
#search-body {
  display: flex;
  justify-content: space-between;
}

#left-sidebar {
  flex-basis: 1;
  text-align: left;
}

.joblist {
  width: 80%;
  display: flex;
  flex-direction: column;
}

#left-sidebar input[type="text"] {
  width: 300px;
  border: none;
}

#left-sidebar ul {
  margin-top: 25px;
}
</style>
