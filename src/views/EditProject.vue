<template>
  <form @submit.prevent="handleUpdate">
    <label>Title:</label>
    <input v-model="title" type="text" required />
    <label>Details:</label>
    <textarea v-model="details" required></textarea>
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
  props: ['id'],
  data() {
    return {
      title: '',
      details: '',
      uri: 'https://my-json-server.typicode.com/samcharles93/project-planner/projects/' + this.id,
    }
  },
  mounted() {
    fetch(this.uri)
      .then((res) => res.json())
      .then((data) => {
        this.title = data.title
        this.details = data.details
      })
  },
  methods: {
    handleUpdate() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ title: this.title, details: this.details }),
      })
        .then(() => this.$router.push('/'))
        .catch((err) => console.log(err.message))
    },
  },
}
</script>

<style></style>
