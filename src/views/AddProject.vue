<template>
  <form @submit.prevent="handleSubmit">
    <label for="">Title</label>
    <input type="text" required v-model="title">
    <label for="">Details</label>
    <textarea required v-model="details"></textarea>
    <button>Add Project</button>
  </form>
</template>

<script>
  export default {
    data () {
      return {
        title:'',
        details: ''
      }
    },
    methods: {
      handleSubmit () {
        // in order to send a project we need to make one = an obj project with all the propreties that we need
        // id prop is handle by json-server in this case, but we must provide one if needed
        let project = {
          title: this.title,
          details: this.details,
          isComplete: false
        }

        fetch('http://localhost:3000/projects',{
          method: 'POST',
          headers: {'Content-Type': 'application/json'},
          body:JSON.stringify(project)
        }).then(()=>{
          this.$router.push('/')
        }).catch(err => console.log(err))
      }
    }
  }
</script>

<style lang="css">
  form{
    background: #fff;
    padding: 20px;
    border-radius: 10px;
  }
  label{
    display: block;
    color:#bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0;
  }
  input {
    padding: 10px;
    border: 0;
    border-bottom:1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
  }
  textarea {
    border:1px solid #ddd;
    padding: 10px;
    width: 100%;
    height: 100%;
    box-sizing: border-box;
  }
  form button {
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: #fff;
    padding: 10px;
    border: 0px;
    border-radius:6px;
    font-size: 16px;
  }
</style>