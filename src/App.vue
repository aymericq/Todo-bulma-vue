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
          <div v-for="card in cards_not_started" v-bind:key="card.id"
            class="card" style="margin: 0 0 30px 0">
            <div class="card-header">
              <div class="card-header-title">{{ card.title }}</div>
            </div>
            <div class="card-content">
              Très bieng.
            </div>
            <div class="card-footer">
              <div class="card-footer-item">
                <a v-on:click="card.status = 'wip'" class="button is-info">Start</a>
              </div>
              <div class="card-footer-item">
                <a v-on:click="card.status = 'deleted'" class="button is-danger">
                  <span class="icon">
                    <font-awesome-icon icon="trash" />
                  </span>
                </a>
              </div>
            </div>
          </div>
        </div>
        <div class="column is-one-third ">
          <div class="title">
            In progress
          </div>
          <div v-for="card in cards_wip" v-bind:key="card.id"
            class="card" style="margin: 0 0 30px 0">
            <div class="card-header">
              <div class="card-header-title">{{ card.title }}</div>
            </div>
            <div class="card-content">
              Très bieng.
            </div>
            <div class="card-footer">
              <div class="card-footer-item">
                <a class="button is-success">Done</a>
              </div>
              <div class="card-footer-item">
                <a class="button is-warning">Stop</a>
              </div>
              <div class="card-footer-item">
                <a class="button is-danger">Delete</a>
              </div>
            </div>
          </div>
        </div>
        <div class="column is-one-third ">
          <div class="title">
            Done
          </div>
          <div v-for="card in cards_done" v-bind:key="card.id"
            class="card" style="margin: 0 0 30px 0">
            <div class="card-header">
              <div class="card-header-title">{{ card.title }}</div>
            </div>
            <div class="card-content">
              Très bieng.
            </div>
            <div class="card-footer">
              <div class="card-footer-item">
                <a class="button is-info">Reset</a>
              </div>
              <div class="card-footer-item">
                <a class="button is-danger">Delete</a>
              </div>
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
import { library } from '@fortawesome/fontawesome-svg-core'
import { faTrash } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import Vue from 'vue'

library.add(faTrash)

Vue.component('font-awesome-icon', FontAwesomeIcon)

Vue.config.productionTip = false

export default {
  name: 'app',
  data: function () {
    return {
      message: "Hello!",
      cards: [
        {
          id: 0,
          title: "Hello",
          status: 'not_started'
        },
        {
          id: 1,
          title: "Helloooo",
          status: "not_started"
        },
        {
          id: 2,
          title: "Chibre.",
          status: "done"
        },
        {
          id: 3,
          title: "Chibron.",
          status: "wip"
        }
      ]
    }
  },
  computed: {
    cards_not_started: function() {
      return this.cards.filter(item => (item.status == "not_started"))
    },
    cards_wip: function() {
      return this.cards.filter(item => (item.status == "wip"))
    },
    cards_done: function() {
      return this.cards.filter(item => (item.status == "done"))
    }
  },
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
