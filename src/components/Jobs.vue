<template>
  <div class="jobs">
   
    <div v-bind:key="job.id" v-for="job in jobs">
        <Job v-bind:job="job" v-on:del-job="$emit('del-job', job.id)" />
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
  props: ["jobs"], 
}
</script>

<style scoped>

</style>