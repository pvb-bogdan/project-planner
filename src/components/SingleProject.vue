<template>
  <div class="project" :class="{complete: project.isComplete}">
    <div class="actions">
      <h3 @click="seeDetails">{{project.title}}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: { id: project.id }}">
          <span class="material-icons">edit</span>
        </router-link>
        <span class="material-icons" @click="deleteProject">delete</span>
        <span class="material-icons tick" @click="toggleComplete">done</span>
      </div>
    </div>
    <div class="details" v-if="showDetails">
      <p>{{project.details}}</p>
    </div>
  </div>
</template>

<script>
  export default {
    props: ['project'],
    data () {
      return {
        showDetails: false,
        url: 'http://localhost:3000/projects/' + this.project.id
      }
    },
    methods: {
      seeDetails () {
        this.showDetails = !this.showDetails
      },
      deleteProject () {
        fetch(this.url,{method: 'DELETE'})
        .then( ()=> this.$emit('delete', this.project.id))
        .catch(err => console.log(err.message))
      },
      toggleComplete () {
        fetch(this.url, {
          method: 'PATCH',
          // send in headers a contetn as a json
          headers: {'Content-Type': 'application/json'},
          // send an obj with just the key we want to update (PATCH) - complete in this case
          // and add negative to complete to change the complete proprety in db
          // it the complete is true then it will be false and viceversa
          // we have to make a string form obj to send data between client and db
          body: JSON.stringify({isComplete: !this.project.isComplete})
       }).then(()=> this.$emit('complete', this.project.id))
       .catch(err => console.log(err.message))
      }
    }
  }
</script>

<style lang="css" scoped>
  .project {
    margin:20px auto;
    background: white;
    padding: 10px 20px;
    border-radius: 4px;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
    border-left: 4px solid #e90074;
  }
  h3 {
    cursor: pointer;
  }
  .actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .material-icons {
    font-size: 24px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
  }
  .material-icons:hover {
    color: #777;
  }
  .project.complete{
    border-left:4px solid #00ce89;
  }
  .project.complete .tick{
    color: #00ce89;
  }
</style>