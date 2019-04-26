<template>
  <div id="app">
    <section class="hero is-primary">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
            Toudous
          </h1>
          <h2 class="subtitle">
            Manage all the things you will never actually do!
          </h2>
        </div>
      </div>
    </section>
    <section class="section">
      <div class="columns">
        <div class="column is-one-third ">
          <div class="title">
            Not started
          </div>
          <div class="card">
            <div class="card-header">
              <div class="card-header-title">Excellent</div>
            </div>
            <div class="card-content">
              Très bieng.
            </div>
            <div class="card-footer">
              <div class="card-footer-item">
                <a class="button">Start</a>
              </div>
            </div>
          </div>
          <hr>
          <div class="card">
            <div class="card-header">
              <div class="card-header-title">Excellent</div>
            </div>
            <div class="card-content">
              Très bieng.
            </div>
          </div>
        </div>
        <div class="column is-one-third ">
          <div class="title">
            In progress
          </div>
          <div class="card">
            <div class="card-header">
              <div class="card-header-title">Excellent</div>
            </div>
            <div class="card-content">
              Très bieng.
            </div>
          </div>
          <hr>
          <div class="card">
            <div class="card-header">
              <div class="card-header-title">Excellent</div>
            </div>
            <div class="card-content">
              Très bieng.
            </div>
          </div>
        </div>
        <div class="column is-one-third ">
          <div class="title">
            Done
          </div>
          <div class="card">
            <div class="card-header">
              <div class="card-header-title">Excellent</div>
            </div>
            <div class="card-content">
              Très bieng.
            </div>
          </div>
          <hr>
          <div class="card">
            <div class="card-header">
              <div class="card-header-title">Excellent</div>
            </div>
            <div class="card-content">
              Très bieng.
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import 'bulma/css/bulma.css'

export default {
  name: 'app',
  components: {
    HelloWorld
  }
}
</script>

<style>
@import "../node_modules/bulma/css/bulma.css"; 
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
