<template>
  <div id="app">
    <h2>미니 계산기</h2>
    <router-view/>
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/info">info</router-link>
    </nav>
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
