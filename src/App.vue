<template>
  <div id="app">
    <Navbar />
    <!-- <router-view/> -->
    <AddJob v-on:add-job="addJob" />
    <input type="text" v-model="search" placeholder="Search title">
    <Jobs v-bind:filterJobs="filterJobs" v-on:del-job="deleteJob" v-bind:jobs="jobs" />
    <!-- v-on:update-job="updateJobDetails" : to use&listen emit -->
  </div>

</template>

<script>
import Navbar from './components/layout/Navbar.vue'
import Jobs from './components/Jobs.vue'
import AddJob from './components/AddJob.vue'

export default {
  name: 'App',
  components: {
    Navbar,
    AddJob,
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
      ],
       search: ''
    }
  },
  // Will provide data in other places in your app that's not directly a child
  // to avoid duplication of passing down data, use it as a function instead
  // provide: { jobs: []},
  // provide() {
  //   return {
  //     jobs: this.jobs
  //   }
  // },

  // listen to an emit?
  provide() {
    return {
      editJob: this.updateJobDetails
    }
  },

  methods: {
    // created is like ComponentDidMount on React
    // Mounts the data right away when component loads
    created() {
    // fetch the api here (use fetch or axios)
    console.log("Use Fetch/Axios here to populate the DOM after mounting")
    // if using fetch:
    // fetch('https://---- api goes here -----')
    //   .then(response => response.json())
    //   .then(data => (this.jobs = data))

    // if using axios:
    // axios.get('https://---- api goes here -----')
    //   .then(response => this.jobs = response.data)
    //   .catch(error => console.log(error))
    },
    addJob(newJob) {
      // copy what's on the original array and add the new one
      console.log("CREATE", newJob)
      // this.jobs.push(newJob)
      this.jobs = [...this.jobs, newJob]
    },
    deleteJob(id) {
      this.jobs = this.jobs.filter( job => job.id !== id )
    },
    updateJobDetails(updatedJob) {
      // can also deconstruct
      // const { title } = updatedJob
      console.log('HERE', updatedJob)
      // this.jobs.filter((job) => {
      //       if(job.id === updatedJob.id) {
      //         job.title = updatedJob.title
      //         job.description = updatedJob.description
      //         job.skills=updatedJob.skills
      //       }
      // })
      const jobFound = this.jobs.find((job) => job.id === updatedJob.id)
      jobFound.title = updatedJob.title
      jobFound.description = updatedJob.description
      jobFound.skills=updatedJob.skills

    }
  },
  computed: {
// post.title.toLowerCase().includes(this.search.toLowerCase())

    filterJobs() {
      // console.log("search", this.search)
     return this.jobs.filter(job => {
      //  return job.title.match(this.search)
       return job.title.toLowerCase().includes(this.search.toLowerCase())
       })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin: 60px;
}
.btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #666;
  }
</style>
