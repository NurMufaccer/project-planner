<template>
  <div>
    <form @submit.prevent="handelSubmit">
        <label>Title:</label>
        <input v-model="title" type="text" required>
        <label>Details:</label>
        <textarea v-model="details" required></textarea>
        <button>Add Project</button>
    </form>
  </div>
</template>

<script>
export default {
data() {
    return {
        title: '',
        details: ''
    }
    },
methods: {
    handelSubmit() {
        let project = {
            title: this.title,
            details: this.details,
            complete: false
        }
        fetch ('http://localhost:3000/projects', {
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(project)
        }).then(() => {
            this.$router.push('/')
        }).catch((err)=> console.log(err))
    }
},
}
</script>

<style>
form{
    background: #fff;
    padding: 20px;
    border-radius: 14px;
}
label{
    display: block;
    color: #bbb;
    text-transform: uppercase;
    letter-spacing: 1px;
    margin: 20px 0 10px 0;
    font-size: 14px;
    font-weight: bold;
}
input{
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
}
textarea{
    padding: 10px;
    border: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
}
form button{
    display: block;
    border: none;
    border-radius: 6px;
    background: greenyellow;
    color: #fff;
    margin: 20px auto 10px;
    font-size: 20px;
    padding: 5px 10px;
}
</style>