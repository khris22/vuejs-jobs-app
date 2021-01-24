<template>
  <div id="app">
    <Jobs v-bind:jobs="jobs"/>
  </div>

</template>

<script>
import Jobs from './components/Jobs.vue'

export default {
  name: 'App',
  components: {
    Jobs
  },
  data() {
    return {
      jobs: [
        {
          id: 1,
          title: "Software Developer",
          skills: ["Javascript", "html", "css"],
          description: "Entry level position for Company A"
        },
        {
          id: 2,
          title: "Frontend Dev",
          skills: ["React", "html", "css"],
          description: "Needs to have intermediate knowledge in React"
        },
        {
          id: 3,
          title: "Senior Backend Dev",
          skills: ["Java"],
          description: "5 years experience in Java"
        },
        {
          id: 4,
          title: "UX/UI Designer",
          skills: ["html", "css", "materialUI"],
          description: "Looking for someone with design passion"
        },
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
