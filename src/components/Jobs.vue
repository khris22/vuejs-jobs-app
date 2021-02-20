<template>
  <div class="jobs">
   
    <div v-bind:key="job.id" v-for="job in filterJobs">
        <!-- LISTENERS ARE DEPRECATED -->
        <!-- can use listeners to help parent listen to child  -->
        <!-- v-on="$listeners" -->
        <Job v-bind:job="job" v-on:del-job="$emit('del-job', job.id)" v-bind:jobs="jobs" />
    </div>
  </div>
</template>


<script>
import Job from './Job.vue'

export default {
  name: 'Jobs',
  components: {
      Job
  },
  props: ["filterJobs", "jobs"], 
}
</script>

<style scoped>

</style>

