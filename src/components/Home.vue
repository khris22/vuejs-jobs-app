<template>
  <div id="app">

    <AddJob />
    <input class="search-bar" type="text" v-model="search" placeholder="Search title">
    <div v-if="isLoading">
        <h2>Loading....</h2>
    </div>
    <div v-else-if="!isLoading && (!jobs || jobs.length === 0)">
      NO DATA FOUND
    </div>
    <div v-else>
    <Jobs v-bind:filterJobs="filterJobs" v-on:del-job="deleteJob" v-bind:jobs="jobs" />
    <!-- v-on:update-job="updateJobDetails" : to use&listen emit -->
    </div>

  </div>

</template>

<script>

import Jobs from './Jobs.vue'
import AddJob from './AddJob.vue'


export default {
  name: 'Home',
  components: {
    AddJob,
    Jobs,
  },
  data() {
    return {
      jobs: [],
      search: '',
      isLoading: false
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
    // addJob(newJob) {
    //   // copy what's on the original array and add the new one
    //   console.log("CREATE", newJob)
    //   // this.jobs.push(newJob)
    //   this.jobs = [...this.jobs, newJob]
    // },
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
  },
        // created is like ComponentDidMount on React
    // Mounts the data right away when component loads
    mounted() {
    // fetch the api here (use fetch or axios)
    console.log("Use Fetch/Axios here to populate the DOM after mounting")
    // if using fetch:
    this.isLoading=true
    fetch('https://vue-jobs-test-default-rtdb.firebaseio.com/jobs.json')
      .then(response => response.json())
      .then(data => {
        this.isLoading = false
        const results = []
        for (const id in data) {
          results.push({
            id: id,
            title: data[id].title,
            description: data[id].description,
            skills: data[id].skills
          })
        }
        this.jobs = results
      
      })
      // you can use alert here for server side error
      // or set it as a state
      // or make you're modal or error
      // 
      .catch(error => console.log(error))

    // if using axios:
    // axios.get('https://---- api goes here -----')
    //   .then(response => this.jobs = response.data)
    //   .catch(error => console.log(error))
    }, 
    updated() {

    }
}
</script>

<style>

.search-bar {
  display: block;
  margin: auto;
  margin-top: 30px;
  text-align: center;
}

/* #app {
  font-family: Roboto, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin: 60px;
} */

.btn {
    display: inline-block;
    border: none;
    background: rgb(206, 124, 124);
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: rgb(218, 85, 81);
  }
</style>
