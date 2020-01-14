// App.vue

<template>
  <div class="container">
      <b-navbar class="level">
        <template slot="brand">
            <b-navbar-item tag="router-link" :to="{ path: '/' }">
                <img
                    src="http://172.16.4.242/img/inah.png"
                    alt="Lightweight UI components for Vue.js based on Bulma"
                >
            </b-navbar-item>
        </template>
        <template slot="start">
            <b-navbar-item url="/"  tag="router-link" to="/">
                 Principal
            </b-navbar-item>
            <b-navbar-item tag="router-link" to="/create">
                 Crear Post
            </b-navbar-item>
            <b-navbar-item tag="router-link" to="/posts">
                 Ver Post
            </b-navbar-item>

        </template>

        <template slot="end">
            <b-navbar-item tag="div">
                <div class="buttons">
                    <a class="button is-primary">
                        <strong>Sign up</strong>
                    </a>
                    <a class="button is-light">
                        Log in
                    </a>
                </div>
            </b-navbar-item>
        </template>
    </b-navbar>
    <div class="container has-background-black">
        <router-view></router-view>
    </div>
  </div>
</template>

<style>
    .fade-enter-active, .fade-leave-active {
      transition: opacity 0.5s
    }
    .fade-enter, .fade-leave-active {
      opacity: 0
    }
</style>

<script>

    export default{
    }
</script>
