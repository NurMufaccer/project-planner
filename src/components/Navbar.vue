<template>
  <nav class="main-nav">
    <router-link :to="{name: 'home'}">Projects</router-link>
    <router-link :to="{name: 'AddProject'}">Add New Project</router-link>
  </nav>
</template>

<script>
export default {

}
</script>

<style>
    .main-nav{
        text-align: center;
        margin: 40px auto;
    }
    .main-nav a{
        display: inline-block;
        text-decoration: none;
        margin: 0 10px;
        font-size: 18px;
        color: #999;
    }
    a.router-link-active{
        border-bottom: 3px solid greenyellow;
        padding-bottom: 4px;
    }
</style>