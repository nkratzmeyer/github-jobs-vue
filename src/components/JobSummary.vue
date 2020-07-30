<template>
  <div class="job-mini" v-on:click="handleJobClick">
    <img v-if="job.company_logo" class="logo" :src="job.company_logo" alt="Company logo" />
    <div class="main-details">
      <p class="company">{{ job.company }}</p>
      <p class="job-title">{{ job.title }}</p>

      <div class="minor-details">
        <div class="job-type">
          <p>{{ job.type }}</p>
        </div>

        <div class="location-posted">
          <p>
            <i class="fa fa-globe" aria-hidden="true"></i>
            <span>{{ job.location }}</span>

            <i class="fa fa-clock-o" aria-hidden="true"></i>
            <span>{{ jobPosted }}</span>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// This component is responsible for displaying basic summary details about a job such as title,
// company, logo, etc. 
import moment from "moment";

export default {
  props: {
    job: {
      type: Object,
    },
  },
  methods: {
    handleJobClick() {
      this.$emit("job-clicked", this.job.id);
    },
  },

  computed: {
    //Get the job created_at variable formatted with a "from now" format.
    jobPosted() {
      return moment(this.job.created_at).fromNow();
    },
  },
};
</script>

<style scoped>
.job-mini {
  font-family: Roboto;
  display: flex;
  flex-wrap: nowrap;
  align-items: stretch;
  width: 95%;
  margin: 0 0 20px 0;
  padding: 5px;
  text-align: left;
  background-color: white;
  height: 114px;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.job-mini:hover {
  cursor: pointer;
}

.job-mini .logo {
  flex-shrink: 0;
  object-fit: contain;
  width: 90px;
  height: 90px;
  border-radius: 4px;
  align-self: center;
}

.main-details {
  position: relative;
  width: 100%;
  margin-left: 15px;
}

.minor-details {
  position: absolute;
  bottom: 10px;
  display: flex;
  justify-content: space-between;
  width: 100%;
  font-size: 14px;
  font-weight: 300;
  color: rgb(134, 134, 134);
  line-height: 26px;
}

.job-type {
  border: 1px solid #334680;
  color: #334680;
  text-align: center;
  height: 26px;
  border-radius: 4px;
  padding: 0 5px;
  font-style: normal;
  font-weight: bold;
  font-size: 12px;
}

.location-posted {
  margin-left: 5px;
  margin-right: 10px;
  color: #B9BDCF;
}

.job-title {
  font-style: normal;
  font-weight: normal;
  font-size: 18px;
  line-height: 21px;
  margin-top: 10px;
}

.company {
  font-style: normal;
  font-weight: bold;
  font-size: 12px;
  line-height: 14px;
}

i{
  margin: 0 10px;
}

@media only screen and (max-width: 600px) {
  .job-mini {
    height: 147px;
  }

  .minor-details {
    flex-direction: column;
    align-content: flex-start;
    line-height: 14px;
    bottom: 0;
    height: 50px;
  }

  .job-type{
    height: 14px;
    width: 60px;
  }

  .job-title {
    font-size: 16px;
    line-height: 19px;
  }
}
</style>