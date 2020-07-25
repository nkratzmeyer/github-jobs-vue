<template>
    <div class="job-mini">
      <img class="logo" :src="job.company_logo" alt="Company logo" />
      <div class="main-details">
        <h5>{{ job.company }}</h5>
        <h3>{{ job.title }}</h3>
        <p class="job-type">{{ job.type }}</p>
      </div>

      <div class="minor-details">
        <p>
          <i class="fa fa-globe" aria-hidden="true"></i>
          {{ job.location }}
          <i class="fa fa-clock-o" aria-hidden="true"></i>
          {{ jobPosted }}</p>
      </div>
    </div>
</template>

<script>
import moment from 'moment';

export default {
    props : {
        job: {
            type : Object
        }
    }, 

    computed : {
      jobPosted() {
        return moment(this.job.created_at).fromNow();
      }
    }
}
</script>

<style scoped>
.job-mini {
  display: flex;
  flex-wrap: wrap;
  margin: 0 0 20px 0;
  padding: 5px;
  width: 95%;
  height: 90px;
  text-align: left;
  background-color: white;
  align-self: flex-end;
}

.job-mini .logo {
  width: 80px;
  height: 80px;
}

.main-details {
  margin-left: 15px;
  flex-grow: 3;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.minor-details {
  font-size: 14px;
  font-weight: 300;
  color: rgb(134, 134, 134);
}

.job-type{
  font-weight: bold;
  font-size: 12px;
  border: 1px solid  #243d57;
  width: 60px;
  text-align: center;
  border-radius: 3px;
}
</style>