<template>
  <nav class="navbar" role="navigation" aria-label="main navigation">
  <div class="navbar-brand">
    <a class="navbar-item" href="/">
      <h1>Notebook</h1>
      <!-- <img src="" alt="Notebook" width="112" height="28"> -->
    </a>
    <div class="navbar-menu is-active">
      <router-link class="navbar-item" to="/home">Home</router-link>
      <router-link class="navbar-item" to="/about">About</router-link>
    </div>

    <a role="button" class="navbar-burger" aria-label="menu" aria-expanded="false">
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
    </a>
  </div>
</nav>
</template>
