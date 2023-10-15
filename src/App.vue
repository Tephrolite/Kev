<template>
  <div id="app">
    <nav>
      <router-link class="navLink" to="/">Home</router-link>
      <router-link class="navLink" to="/about">About</router-link>
      <router-link class="navLink" to="/booking">Book with Us</router-link>
      <router-link class="navLink" to="/contact">Contact</router-link>
    </nav>
    <router-view/>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: #B77F7F;
  height: 100vh;
}

nav {
  padding: 50px 0 10px 200px;
  padding-bottom: 10px;
  background-color: black;

  a {
    font-size: 22px;;
    font-weight: 500;
    color: white;
    text-decoration: none;

    &.router-link-exact-active {
      border-bottom: 2px solid white;
    }
  }
}
.navLink {
  margin-left: 40px
}
</style>
