<template>
  <div class="jobs">
    <h1>Jobs List</h1>
    <div v-bind:key="job.id" v-for="job in jobs">
        <h3>{{ job.title }}</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Jobs',
  props: ["jobs"]
}
</script>

<style scoped>

</style>