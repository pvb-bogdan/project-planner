<template>
  <form @submit.prevent="handleSubmit">
    <label for="">Title</label>
    <input type="text" required v-model="title">
    <label for="">Details</label>
    <textarea required v-model="details"></textarea>
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
  props:['id'],
  data(){
    return {
      title: '',
      details:'',
      url: 'http://localhost:3000/projects/' + this.id
    }
  },
  mounted(){
    fetch(this.url)
    .then(res => res.json())
    .then(data => {
      // console.log(data)
      this.title = data.title,
      this.details = data.details
    })
    .catch(err => console.log(err.message))
  },
  methods: {
    handleSubmit(){
      fetch(this.url, {
        method: 'PATCH',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({
          title: this.title,
          details: this.details
        })
      })
      .then(()=> this.$router.push('/'))
      .catch(err => console.log(err.message))
    }
  }
}
</script>

<style>

</style>