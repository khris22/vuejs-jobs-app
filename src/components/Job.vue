<template>
    <div class="job-item">
       
        <div v-if="isEditing">
            EDIT JOB DETAILS
            <form @submit.prevent="updateJobDetails">
            <div>
            <label for="title">Title:</label>
            <input class="form-title" type="text" v-model="title" name="title" :placeholder="job.title" required>
            </div>
            <div>
            <label for="description">Description: </label>
            <input class="form-description" type="text" v-model="description" name="description" :placeholder="job.description" required >
            </div>
            <div>
            <label for="skills">Skills: </label>
            <input class="form-skills" type="text" name="skills[]" v-model="skills[0]" :placeholder="job.skills[0]">
            <input class="form-skills" type="text" name="skills[]" v-model="skills[1]" :placeholder="job.skills[1]">
            <input class="form-skills" type="text" name="skills[]" v-model="skills[2]" :placeholder="job.skills[2]">
            </div>
      
            <input type="submit" value="Save" class="btn">
            </form>
        </div>
        <div v-else>
            <h3>Job Title: {{ job.title }}</h3>
            <p>Decription: {{ job.description }}</p>
        Skills:
            <div v-bind:key="skill.id" v-for="skill in job.skills">
                {{ skill }}
            </div>
        <button @click="updateJob"> Edit </button>
        <button @click="$emit('del-job', job.id)" class="del-job"> Delete </button>

        </div>
    </div>
    
</template>

<script>
export default {
    name: "Job",
    // acts like props to avoid pass through components
    inject: ['editJob'],
    props: ["job", "jobs"],
    data() {
    return {
        isEditing: false,
        id: this.job.id,
        title: this.job.title,
        description: this.job.description,
        skills: this.job.skills
    }},
    methods: {
        updateJob() {
            this.id = this.job.id
            this.isEditing = !this.isEditing
        },
        updateJobDetails() {
            let updatedJob = {
                id: this.id,
                title: this.title,
                description: this.description,
                skills: this.skills
            }
        //    const updatedJob = this.jobs.filter((job) => {
        //        if(job.id === this.id) {
        //            job.title = this.title
        //            job.description = this.description
        //            job.skills=this.skills
        //        }
        //    })
            console.log("EDIT", updatedJob)
            // from grandchild to App, better use vuex?
            // this.$parent.$emit('update-job', updatedJob)
            
            // using listeners: 
            // update: listeners are deprecated
            // just emit is used
            // this.$emit('update-job', updatedJob)

            // using inject
            this.editJob(updatedJob)

            this.isEditing = !this.isEditing
        }
    }
    
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