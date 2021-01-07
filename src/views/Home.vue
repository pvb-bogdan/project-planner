<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" @update="updateProjects"/>
      </div>
    </div>
  </div>
</template>

<script>

import SingleProject from '../components/SingleProject'
export default {
  name: 'Home',
  components: {SingleProject},
  data () {
    return {
      projects: []
    }
  },
  mounted () {
    fetch('http://localhost:3000/projects')
    .then(res => res.json())
    .then(data => this.projects = data)
    .catch(err => console.log(err.message))
  },
  methods : {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => {
        return project.id !== id
      })
    },
    handleComplete(id){
      let p = this.projects.find(project=>{
        return project.id === id
      })
      p.isComplete = !p.isComplete
    }
  }
}
</script>
