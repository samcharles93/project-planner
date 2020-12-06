<template>
  <nav class="main-nav">
    <router-link class="shadow" :to="{ name: 'Home' }">Projects</router-link>
    <router-link class="shadow" :to="{ name: 'AddProject' }">Add Project</router-link>
  </nav>
</template>

<script>
export default {

}
</script>

<style>
.main-nav {
  text-align: center;
  margin: 40px auto;
}
.main-nav a {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  color: #858585;
  font-size: 18px;
  transition: border-bottom 0.2s ease;
  border-bottom: 4px solid transparent;
  padding-bottom: 4px;

}
.main-nav a:hover {
  color: #464646;
}
a.router-link-active {
  border-bottom: 4px solid #00ce89;
  padding-bottom: 4px;
}
</style>