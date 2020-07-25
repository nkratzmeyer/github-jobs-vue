<template>
  <div>
    <JobSummary class="shadow" v-for="job in jobs" v-bind:key="job.id" v-bind:job="job" />
  </div>
</template>

<script>
import JobSummary from './JobSummary.vue';

export default {
  name: "JobList",
  components : {
    JobSummary
  },

  props : {
    jobs : {
      type : Array
    }
  }
};
</script>
