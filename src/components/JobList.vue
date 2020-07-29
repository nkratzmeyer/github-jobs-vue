<template>
  <div>
    <JobSummary class="shadow" 
    v-on:job-clicked="handleJobClick"
    v-for="job in jobs" 
    v-bind:key="job.id" 
    v-bind:job="job" />
  </div>
</template>

<script>
import JobSummary from './JobSummary.vue';

export default {
  name: "JobList",
  components : {
    JobSummary
  },
  methods :{
    handleJobClick(id){
      this.$router.push(`/job/${id}`);
    }
  },
  props : {
    jobs : {
      type : Array
    }
  }, 
};
</script>
