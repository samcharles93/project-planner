<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditProject', params: { id: project.id } }" >
          <span @click="editProject" class="material-icons">edit</span>
        </router-link>
        <span @click="deleteProject" class="material-icons">delete</span>
        <span @click="toggleComplete" class="material-icons tick">done</span>
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
      uri: 'https://my-json-server.typicode.com/samcharles93/project-planner/projects/' + this.project.id,
    }
  },
  methods: {
    deleteProject() {
      fetch(this.uri, { method: 'DELETE' })
        .then(() => this.$emit('delete', this.project.id))
        .catch((err) => console.log(err.message))
    },
    toggleComplete() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ complete: !this.project.complete }),
      })
        .then(() => this.$emit('complete', this.project.id))
        .catch((err) => console.log(err.message))
    },
    editProject() {},
  },
}
</script>

<style>
.project {
  margin: 20px auto;
  background-color: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.2);
  border-left: 6px solid #e90074;
  transition: all 0.5s ease;
}
.project.complete {
  border-left: 6px solid #00ce89;
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
  padding: 3px;
  color: #858585;
  cursor: pointer;
  transition: all 0.5s ease;
}
.material-icons:hover {
  color: #464646;
  background-color: rgba(0, 0, 0, 0.05);
  border-radius: 20px;
  padding: 3px;
}
.project.complete .tick {
  color: #00ce89;
  background-color: #ddfff3;
  border-radius: 20px;
  padding: 3px;
}
</style>
