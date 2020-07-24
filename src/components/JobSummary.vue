<template>
    <div class="job-mini">
      <img class="logo" :src="job.company_logo" alt="Company logo" />
      <div class="main-details">
        <h5>{{ job.company }}</h5>
        <h2>{{ job.title }}</h2>
        <h3>{{ job.type }}</h3>
      </div>

      <div class="minor-details">
        <h5>{{ job.location }}</h5>
        <h5>{{ job.created_at }}</h5>
      </div>
    </div>
</template>

<script>
export default {
    props : {
        job: {
            type : Object
        }
    }
}
</script>

<style scoped>
.job-mini {
  display: flex;
  flex-wrap: wrap;
  margin: 10px auto;
  padding: 5px;
  width: 100%;
  height: 90px;
  background-color: rgb(245, 240, 240);
  text-align: left;
  box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
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
</style>