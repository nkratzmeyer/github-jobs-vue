<template>
  <div>
    <SearchArea v-on:search="setSearchTerm" class="shadow" />
    <div id="search-body">
      <div id="left-sidebar">
        <div class="checkbox">
          <input v-on:click="doSearch" type="checkbox" name="full-time" v-model="fullTime" />
          <label for="full-time">Full Time</label>
        </div>
        <div class="location-filter">
          <label for="location">LOCATION</label>
          <input
            v-model="searchLocation"
            v-on:keyup.enter="doSearch"
            class="shadow"
            type="text"
            name="location"
            placeholder="City, state, zipcode, or country"
          />
        </div>

        <ul>
          <li>
            <div class="checkbox">
              <input
                v-on:click="handleLocationClick('Worldwide')"
                type="checkbox"
                name="worldwide"
                value="Worldwide"
              />
              <label for="worldwide">Worldwide</label>
            </div>
          </li>
          <li>
            <div class="checkbox">
              <input v-on:click="handleLocationClick('USA')" type="checkbox" name="usa" value="USA" />
              <label for="usa">USA</label>
            </div>
          </li>
          <li>
            <div class="checkbox">
              <input
                v-on:click="handleLocationClick('Remote')"
                type="checkbox"
                name="remote"
                value="Remote"
              />
              <label for="remote">Remote</label>
            </div>
          </li>
          <li>
            <div class="checkbox">
              <input
                v-on:click="handleLocationClick('Austin')"
                type="checkbox"
                name="austin"
                value="Austin"
              />
              <label for="austin">Austin, TX</label>
            </div>
          </li>
        </ul>
      </div>
      <div class="jobs-area" v-bind:class="{ loading : loading }">
        <JobList class="joblist" v-bind:jobs="currentJobs" />
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
    async nextSubPage() {
      this.subpage++;
      if (this.subpage === this.numSubPages) {
        this.page++;
        this.doSearch();
      }
    },
    prevSubPage() {
      if (this.subpage > 0) this.subpage--;
    },
    handleLocationClick(loc) {
      this.searchLocation = loc;
      this.jobs = [];
      this.doSearch();
    },
    setSearchTerm(e) {
      this.searchTerm = e;
      this.jobs = [];
      this.subpage = 0;
      this.page = 1;
      this.doSearch();
    },
    async doSearch() {
      this.loading = true;

      let response = await axios.get(this.searchUrl);
      if (response) {
        // this.jobs = response.data;
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
    currentJobs() {
      return this.jobs.slice(this.subpage * 5, this.subpage * 5 + 5);
    },
    numSubPages() {
      return Math.floor( this.jobs.length / 5);
    },
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
#search-body {
  display: flex;
  justify-content: space-between;
}

#left-sidebar {
  text-align: left;
  padding: 10px;
}

.jobs-area {
  width: 100%;
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
  min-height: 300px;
}

.active {
  background-color: rgb(62, 62, 253);
  color: white;
}

.location-filter {
  margin-top: 12px;
  font-size: 14px;
}

.checkbox {
  font-weight: 500;
  font-size: 14px;
}

input[type="checkbox"] {
  margin-right: 5px;
}

/* Loader */
.loading {
  display: inline-block;
  width: 50%;
  height: 80px;
}
.loading::before {
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid rgb(255, 255, 255);
  border-color: rgb(53, 50, 253) transparent rgb(82, 107, 248) transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

/* Media Queries */
@media only screen and (max-width: 900px) {
  #search-body {
    background-color: lightblue;
    flex-direction: column;
  }

  .joblist {
    align-items: center;
  }
}
</style>
