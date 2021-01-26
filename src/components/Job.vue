<template>
    <div class="job-item">
        <h3>Job Title: {{ job.title }}</h3>
        <p>Decription: {{ job.description }}</p>
        Skills:
        <div v-bind:key="skill.id" v-for="skill in job.skills">
            {{ skill }}
        </div>
        <button > Edit </button>
        <button @click="$emit('del-job', job.id)" class="del-job"> Delete </button>
    </div>
    
</template>

<script>
export default {
    name: "Job",
    props: ["job"]
    
}
</script>

<style scoped>
 .job-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1.5px #ccc dotted;
    margin: 20px;
  }

 .del-job {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    margin: 10px;
    cursor: pointer;
  }

</style>