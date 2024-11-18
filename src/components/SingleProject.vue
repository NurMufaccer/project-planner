<template>
  <div class="projects" :class="{complete: project.complete}">
    <div class="actions">
        <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
        <div class="icon">
          <router-link :to="{name: 'EditProject', params: {id: project.id}}">
            <i class="fa-solid fa-pen"></i>
          </router-link>
          <i @click="deletProject" class="fa-solid fa-trash-can"></i>
          <i @click="toggleComplete" class="fa-solid fa-check tick"></i>
        </div>
    </div>
    <div v-if="showDetails" class="details">
        <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
props: ['project'],
data() {
  return {
    showDetails: false,
    uri: 'http://localhost:3000/projects/' + this.project.id,
  }
  },
  methods: {
    deletProject() {
      fetch(this.uri, { method: 'DELETE' })
        .then(() => this.$emit('delete', this.project.id))
        .catch(err => console.log(err)
        )
    },
    toggleComplete() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-type': 'application/json' },
        body: JSON.stringify({complete: !this.project.complete})
       })
        .then(() => this.$emit('complete', this.project.id))
        .catch(err => console.log(err)
        )
    }
  },

}
</script>

<style>
.projects{
    margin: 20px auto;
    padding: 10px 20px;
    background: #fff;
    border-radius: 8px;
    box-shadow: 1px 2px 3px rgba(0 0 0 .05);
    border-left: 4px solid tomato;
}
h3{
    cursor: pointer;
}
.actions{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.fa-solid{
  font-size: 24px;
  margin-left: 14px;
  color: #bbb;
  cursor: pointer;
}
.fa-solid:hover{
  color: #777;
}
.projects.complete{
  border-left: 4px solid yellowgreen;
}
.projects.complete .tick{
  color: yellowgreen;
}
</style>