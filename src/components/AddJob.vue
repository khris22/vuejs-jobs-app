<template>
<div>
    <form @submit.prevent="addJob">
        <input class="form-title" type="text" v-model="title" name="title" placeholder="Add Job Title">
        <input class="form-description" type="text" v-model="description" name="description" placeholder="Add Job Description" >
        <input class="form-skills" type="text" name="skills[]" v-model="skills[0]" v-on:input="changed" placeholder="Add Skills">
        <input class="form-skills" type="text" name="skills[]" v-model="skills[1]" v-on:input="changed" placeholder="Add Skills">
        <input class="form-skills" type="text" name="skills[]" v-model="skills[2]" v-on:input="changed" placeholder="Add Skills">
        <input type="submit" value="Submit" class="btn">
    </form>
</div>
    
</template>

<script>
import { v4 as uuidv4 } from 'uuid'

export default {
    name: "AddJob",
    data() {
        return {
            title: '',
            description: '',
            skills: []
        }
    },
    methods: {
        addJob() {
            const newJob = {
                id: uuidv4(),
                title: this.title,
                description: this.description,
                skills: this.skills
            }
            this.$emit('add-job', newJob)
            this.title = ''
            this.description = ''
            this.skills = []
        }
    } 
    
}
</script>

<style scoped>
  form {
    display: flex;
  }
  
  .form-title {
    flex: 10;
    padding: 5px;
  }

  .form-description {
    flex: 20;

    padding: 5px;
  }

  .form-skills {
    flex: 2;
    padding: 5px;
  }

  input[type="submit"] {
    flex: 2;
  }

</style>>
