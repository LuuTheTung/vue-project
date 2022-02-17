<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";
import "bootstrap";
import "bootstrap/dist/css/bootstrap.min.css";
</script>

<template>
  <div id="nav">
    <header id="header">
      <nav id="nav-bar">
        <ul>
          <li>
            <img
              id="header-img"
              src="https://timesheet.savvycom.vn/img/savvycom-logo.png"
              alt="savvycom-logo"
            />
          </li>
          <li style="float: right">
            <a class="nav-link"><router-link to="/"><strong>Home</strong></router-link></a>
          </li>
          <li style="float: right">
            <a class="nav-link"><router-link to="/about"><strong>About</strong></router-link></a>
          </li>
        </ul>
      </nav>
    </header>
  </div>
  <router-view />
</template>

<style>
@import "@/assets/base.css";
body {
  background-color: rgb(254, 236, 225);
}
nav ul {
  display: block;
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 10;
  background-color: black;
  list-style-type: none;
}

nav li {
  display: inline;
}

nav a {
  text-decoration: none;
  color: white;
  padding: 10px;
  display: block;
}

nav a:hover {
  text-decoration: none;
  color: black;
  background-color: white;
}

header li img {
  max-height: 20px;
  margin-top: 20px;
}
</style>
