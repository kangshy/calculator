<template>
  <div id="app">
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/axios">axios</router-link> |
      <router-link to="/info">info</router-link>
    </nav>
    <h2>VUE 심화과정 과제</h2>
    <router-view/>
  </div>
</template>

<style>

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  text-decoration : none;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
