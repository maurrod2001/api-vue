<template>

  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <router-link class="navbar-brand text-success" to="/">ConsulMedi</router-link>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
        aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <router-link class="nav-link " aria-current="page" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/about">Pacient</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/medic">Medic</router-link>
          </li>

        </ul>
      </div>
    </div>
  </nav>
  <router-view/>
  <br>
  <footer class="mt-auto py-1 bg-light">
    <span class="text-muted">aplicacccion de prueba de vue con axios</span>
  </footer>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}

::-webkit-scrollbar {
  width: 12px;
  background-color: #212529;
}

::-webkit-scrollbar-track {
  box-shadow: none;
  -webkit-box-shadow: inset 0 0 6px rgba(31, 37, 41, 1);
  border-radius: 10px;
  background-color: #212529;
}

::-webkit-scrollbar-thumb {
  border-radius: 10px;
  background-color: #41b883;
  background-image: -webkit-linear-gradient(90deg, transparent, rgb(64, 196, 130) 50%, transparent, transparent)
}
</style>
