<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <a class="navbar-brand" href="/">blackbandcamp.info</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <router-link to="/" data-toggle="collapse" data-target=".navbar-collapse.show" class="nav-link">Discover</router-link>
            </li>
            <li class="nav-item">
              <router-link to="/about" data-toggle="collapse" data-target=".navbar-collapse.show" class="nav-link">About</router-link>
            </li>
            <li class="nav-item">
              <router-link to="/add" data-toggle="collapse" data-target=".navbar-collapse.show" class="nav-link">Add Submission</router-link>
            </li>
            <li class="nav-item">
              <router-link to="/read" data-toggle="collapse" data-target=".navbar-collapse.show" class="nav-link">Read</router-link>
            </li>
            <li class="nav-item">
              <router-link to="/voices" data-toggle="collapse" data-target=".navbar-collapse.show" class="nav-link">Voices</router-link>
            </li>
            <li class="nav-item">
              <router-link to="/watch" data-toggle="collapse" data-target=".navbar-collapse.show" class="nav-link">Watch</router-link>
            </li>
          </ul>
          <ul class="nav navbar-nav ml-auto">
              <li>
                  <a href="https://www.instagram.com/blackbandcamp/" class="nav-link" target="_blank"><img src="./assets/instagram-icon.png" class="ig-icon"></a>
              </li>
              <li>
                  <a href="https://www.twitter.com/blackbandcamp/" class="nav-link" target="_blank"><img src="./assets/twitter-icon.png" class="ig-icon"></a>
              </li>
          </ul>
        </div>
      </div>
    </nav>
    <router-view/>

  </div>
</template>

<script>


export default {
  name: 'App',

  data: () => ({

  }),
  computed: {
  },
  mounted () {
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  min-height:100vh;
  @media (prefers-color-scheme: dark) {
    background-color: black;
    color: white;
  }
  @media (prefers-color-scheme: light) {
    background-color: #f7f7f7;
    color: black;
  }
}

.router-link-exact-active {
  color: #fff !important;
}

.ig-icon {
  width:30px;
}
</style>
