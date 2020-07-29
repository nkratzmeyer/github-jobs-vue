<template>
  <div class="job-mini" v-on:click="handleJobClick">
    <img class="logo" :src="job.company_logo" alt="Company logo" />
    <div class="main-details">
      <h6>{{ job.company }}</h6>
      <p class="job-title">{{ job.title }}</p>

      <div class="minor-details">
        <h3 class="job-type">
          {{ job.type }}
        </h3>

        <div class="location-posted">
          <p>
            <i class="fa fa-globe" aria-hidden="true"></i>
            <span class="location-posted">{{ job.location }}</span>

            <i class="fa fa-clock-o" aria-hidden="true"></i>
            <span class="location-posted">{{ jobPosted }}</span>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  props: {
    job: {
      type: Object,
    },
  },
  methods :{
    handleJobClick(){
      this.$emit('job-clicked', this.job.id);
    }
  },

  computed: {
    jobPosted() {
      return moment(this.job.created_at).fromNow();
    },
  },
};
</script>

<style scoped>
.job-mini {
  display: flex;
  flex-wrap: nowrap;
  width: 95%;
  margin: 0 0 20px 0;
  padding: 5px;
  height: 90px;
  text-align: left;
  background-color: white;
  /* align-self: flex-end; */
}

.job-mini:hover {
  cursor: pointer;
}

.job-mini .logo {
  width: 80px;
  height: 80px;
  flex-shrink: 0;
  object-fit: contain;
}

.main-details {
  position: relative;
  width: 100%;
  margin-left: 15px;
}

.minor-details {
  position: absolute;
  bottom: 0;
  display: flex;
  justify-content: space-between;
  width: 100%;
  font-size: 14px;
  font-weight: 300;
  color: rgb(134, 134, 134);
  flex-wrap: wrap;
}

.job-type {
  font-weight: bold;
  font-size: 12px;
  border: 1px solid #334680;
  color: #334680;
  padding:0 3px;
  text-align: center;
  height: 20px;
  border-radius: 3px;
}

.location-posted {
  margin-left: 5px;
  margin-right: 10px;
}

.job-title {
  font-size: 16px;
  font-weight: 500;
  align-self: flex-start;
}

@media only screen and (max-width: 600px) {
  .job-mini {
    height: 125px;
  }

  .minor-details {
  flex-wrap: wrap;
}
}
</style>