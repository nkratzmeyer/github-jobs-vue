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
          {{ job.title }}
          <span class="job-type">{{ job.type }}</span>
        </div>
        <p class="light">
          <i class="fa fa-clock-o" aria-hidden="true"></i>
          <span>{{ jobPosted }}</span>
        </p>
        <br />
        <br />
        <div class="main-details">
          <img v-if="job.company_logo" class="logo" :src="job.company_logo" alt="Company logo" />
          <div>
            <h4>{{ job.company }}</h4>

            <p class="light">
              <i class="fa fa-globe" aria-hidden="true"></i>
              <span>{{ job.location }}</span>
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
  flex-basis: 25%;
  padding: 10px;
  flex-shrink: 0;
  flex-grow: 0;
  text-align: left;
  max-width: 30%;
}

.main-content {
  flex-basis: 73%;
  padding: 10px;
  text-align: left;
}

.job-header {
  font-style: normal;
  font-weight: bold;
  font-size: 24px;
  line-height: 28px;
}

.logo {
  width: 80px;
  height: 80px;
  flex-shrink: 0;
  object-fit: contain;
  margin-right: 20px;
}

.job-type {
  display: inline-block;
  border: 1px solid #334680;
  text-align: center;
  border-radius: 3px;
  margin-left: 20px;
  padding: 0 3px;
  height: 20px;

  font-style: normal;
  font-weight: bold;
  font-size: 16px;
  line-height: 20px;
}

.light {
  font-style: normal;
  font-weight: 500;
  font-size: 12px;
  line-height: 14px;
  color: #b7bcce;
  margin-top: 8px;
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
  font-style: normal;
  font-weight: normal;
  font-size: 16px;
  line-height: 150%;
}

div >>> li {
 font-style: normal;
font-weight: normal;
font-size: 16px;
line-height: 150%;
}

/* Media Queries */
@media only screen and (max-width: 900px) {
  .container {
    flex-direction: column;
  }

  .left-sidebar {
    max-width: 100%;
  }
}
</style>
