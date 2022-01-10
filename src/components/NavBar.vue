<template>
  <nav class="main-nav">
    <router-link :to="{ name: 'Home' }">Home</router-link>
    <router-link :to="{ name: 'AddProject' }">Add new project</router-link>
  </nav>
</template>

<style>
.main-nav {
  text-align: center;
  margin: 40px auto;
}
.main-nav a {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  color: White;
  font-size: 20px;
}
a.router-link-active {
  border-bottom: 2px solid #ecb365;
  padding-bottom: 4px;
}
</style>
