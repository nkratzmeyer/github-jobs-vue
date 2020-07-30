<template>
  <div>
    <!-- Top Search box -->
    <SearchArea v-on:search="setSearchTerm" class="shadow" />
    <div id="container">
      <!-- Sidebar with filter options -->
      <div id="left-sidebar">
        <div class="checkbox">
          <input v-on:click="clearAndSearch" type="checkbox" name="full-time" v-model="fullTime" />
          <label for="full-time">Full Time</label>
        </div>
        <!-- Location freeform search box -->
        <div class="location-filter">
          <label for="location">LOCATION</label>
          <input
            v-model="searchLocation"
            v-on:keyup.enter="clearAndSearch"
            class="shadow"
            type="text"
            name="location"
            placeholder="City, state, zipcode, or country"
          />
        </div>

        <!-- List of default locations with checkboxes -->
        <ul>
          <li v-for="location in defaultLocations" :key="location.value">
            <div class="checkbox">
              <input
                type="checkbox"
                v-on:change="handleLocationClick"
                v-bind:name="location.value"
                v-bind:value="location.value"
                v-bind:checked="location.checked"
              />
              <label v-bind:for="location.value">{{location.value}}</label>
            </div>
          </li>
        </ul>
      </div>
      <!-- The list of jobs and pagination -->
      <div class="jobs-area" v-bind:class="{ loading : loading }">
        <JobList v-if="currentJobs.length" class="joblist" v-bind:jobs="currentJobs" />
        <div v-else-if="!loading">No more jobs to display</div>
        <Paginator v-on:next-page="nextSubPage" v-on:prev-page="prevSubPage" />
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import JobList from "@/components/JobList.vue";
import SearchArea from "@/components/SearchArea.vue";
import Paginator from "@/components/Paginator.vue";
import axios from "axios";

const jobsPerPage = 5;

export default {
  name: "Home",
  components: {
    JobList,
    SearchArea,
    Paginator,
  },
  //Component Data********************
  data() {
    return {
      jobs: [],
      defaultLocations: [
        {
          value: "Worldwide",
          checked: false,
        },
        {
          value: "Austin",
          checked: false,
        },
        {
          value: "New York",
          checked: false,
        },
        {
          value: "California",
          checked: false,
        },
      ],
      page: 1,
      //The API only returns 50 results at a time which is their "page". So am sectioning each page into
      //subpages for the purpose of navigation and displaying only 5 results at a time.
      subpage: 0,
      searchTerm: "",
      searchLocation: "",
      loading: false,
      fullTime: false,
    };
  },

  //Component Methods********************
  methods: {
    //Get the next set of 5 jobs from the jobs array
    nextSubPage() {
      this.subpage++;

      if (this.subpage === this.numSubPages) {
        this.page++;
        this.doSearch();
      }

      //We have gone past our number of pages, go back to prev
      if (this.subpage > this.numSubPages) {
        this.subpage--;
      }
    },

    //Go to the previous 5 jobs in the jobs array
    prevSubPage() {
      if (this.subpage > 0) this.subpage--;
    },

    //Called when one of the pre-defined location checkboxes is checked
    handleLocationClick(e) {
      this.defaultLocations.forEach((location) => {
        if (location.value === e.target.value) {
          location.checked = e.target.checked;
          if (e.target.checked) {
            this.searchLocation = e.target.value;
            this.clearAndSearch();
          }
        } else {
          location.checked = false;
        }
      });
    },

    //Called when the full time checkbox is checked
    clearAndSearch() {
      this.clearResults();
      this.doSearch();
    },

    //Called when the search component emits the search event.abnf
    //The event will have search term as payload
    setSearchTerm(searchTerm) {
      this.searchTerm = searchTerm;
      this.clearAndSearch();
    },

    //Helper method to clear jobs array and reset variables
    clearResults() {
      this.jobs = [];
      this.subpage = 0;
      this.page = 1;
    },

    // This does the actual call to the API to get jobs
    async doSearch() {
      this.loading = true;

      let response = await axios.get(this.searchUrl);
      if (response) {
        this.jobs = this.jobs.concat(response.data);
      }
      this.loading = false;
    },
  },

  //Component Hooks********************
  created() {
    this.doSearch("");
  },

  //Component Computed********************
  computed: {
    //This gets a slice of the jobs array based on what subpage we're on
    currentJobs() {
      return this.jobs.slice(this.subpage * jobsPerPage, this.subpage * jobsPerPage + jobsPerPage);
    },

    //Get number of subpages based on the total number of jobs in the jobs array
    numSubPages() {
      return Math.floor(this.jobs.length / jobsPerPage);
    },

    //Construct the search URL based on current search term, full-time, and location
    searchUrl() {
      const base =
        "https://cors-anywhere.herokuapp.com/https://jobs.github.com/positions.json?";
      const page = `page=${this.page}`;
      let returnVal = base + page;
      if (this.searchTerm) {
        returnVal += `&description=${this.searchTerm}`;
      }
      if (this.searchLocation) {
        returnVal += `&location=${this.searchLocation}`;
      }
      if (this.fullTime) {
        returnVal += "&full_time=true";
      }

      return returnVal;
    },
  },
};
</script>

<style scoped>
#container {
  display: flex;
  justify-content: space-between;
}

#left-sidebar {
  font-family: Poppins;
  text-align: left;
  padding: 10px;
  flex-grow: 0;
  flex-basis: 20%;
}

.jobs-area {
  flex-basis: 75%;
}

#left-sidebar input[type="text"] {
  width: 300px;
  border: none;
}

#left-sidebar ul {
  margin-top: 25px;
}

.joblist {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.active {
  background-color: rgb(62, 62, 253);
  color: white;
}

.location-filter {
  margin-top: 16px;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
  line-height: 21px;
  text-transform: uppercase;
  color: #b9bdcf;
}

.checkbox {
  font-weight: 500;
  font-size: 14px;
}

input[type="checkbox"] {
  margin-right: 5px;
}
/* Media Queries */
@media only screen and (max-width: 900px) {
  #container {
    flex-direction: column;
  }

  .joblist {
    align-items: center;
  }
}
</style>
