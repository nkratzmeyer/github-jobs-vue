<template>
  <div>
    <div v-if="job" class="container">
      <div class="left-sidebar">
        <h3>
          <a @click="$router.go(-1)">&larr; Back to search</a>
        </h3>
        <br />
        <h4>How to apply</h4>
        <div v-html="job.how_to_apply"></div>
      </div>
      <div class="main-content">
        <div class="job-header">
          <p class="job-title">
            {{ job.title }}
            <span class="job-type">{{job.type}}</span>
          </p>
          <p>
            <i class="fa fa-clock-o" aria-hidden="true"></i>
            <span class="location-posted">{{ jobPosted }}</span>
          </p>
        </div>

        <div class="main-details">
          <img class="logo" :src="job.company_logo" alt="Company logo" />
          <div>
            <h4>{{ job.company }}</h4>

            <p>
              <i class="fa fa-globe" aria-hidden="true"></i>
              <span class="location-posted">{{ job.location }}</span>
            </p>
          </div>
        </div>

        <br />
        <div v-html="job.description"></div>
      </div>
    </div>
    <div v-else class="loading"></div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";

export default {
  name: "Job",
  data() {
    return {
      id: null,
      job: null,
    };
  },
  computed: {
    jobPosted() {
      return moment(this.job.created_at).fromNow();
    },
  },

  async created() {
    this.id = this.$route.params.id;
    let response = await axios.get(
      `https://cors-anywhere.herokuapp.com/https://jobs.github.com/positions/${this.id}.json`
    );
    if (response) {
      this.job = response.data;
    }
  },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-between;
}

.left-sidebar {
  flex-basis: 30%;
  padding: 10px;
  flex-shrink: 0;
  flex-grow: 0;
  text-align: left;
  max-width: 30%;
}

.main-content {
  flex-basis: 65%;
  padding: 0 20px;
  /* background-color: plum; */
  text-align: left;
}

.job-header {
  margin-bottom: 30px;
}

.job-title {
  font-size: 20px;
  font-weight: 500;
  align-self: flex-start;
  vertical-align: middle;
}

.logo {
  width: 80px;
  height: 80px;
  flex-shrink: 0;
  object-fit: contain;
  margin-right: 20px;
}

.job-type {
  font-weight: bold;
  font-size: 14px;
  border: 1px solid #334680;
  text-align: center;
  border-radius: 3px;
  margin-left: 20px;
  padding: 0 3px;
}

.main-details {
  display: flex;
}

i {
  margin-right: 5px;
}

a {
  color: #1e86ff;
}

a:hover {
  cursor: pointer;
}

div >>> a {
  color: #1e86ff;
  text-decoration: none;
  font-weight: 700;
  word-wrap: break-word;
}

div >>> p {
  font-weight: 400;
}

div >>> li {
  font-weight: 400;
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
  .container {
    flex-direction: column;
  }

  .left-sidebar{
    max-width: 100%;
  }
}
</style>
