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
        <div class="column is-fixed">
          <div class="title">
            Not started
          </div>
          <transition-group name="list" tag="div">
            <div v-for="card in cards_not_started" v-bind:key="card.id"
              class="card list-item" style="margin: 0 0 30px 0">
              <div class="card-header">
                <div class="card-header-title">{{ card.title }}</div>
              </div>
              <div class="card-content">
                {{ card.description }}
              </div>
              <div class="card-footer">
                <div class="card-footer-item">
                  <a v-on:click="card.status = 'wip'" class="button is-info">
                    <span></span>
                    <span class="icon" style="margin-right: 2px">
                      <font-awesome-icon icon="play-circle" />
                    </span>
                    <span class="is-hidden-touch ">
                      Start
                    </span>
                  </a>
                </div>
                <div class="card-footer-item">
                  <a v-on:click="card.status = 'deleted'" class="button is-danger">
                    <span></span>
                    <span class="icon" style="margin-right: 2px">
                      <font-awesome-icon icon="trash" />
                    </span>
                    <span class="is-hidden-touch">
                      Delete
                    </span>
                  </a>
                </div>
              </div>
            </div>
          </transition-group>
        </div>
        <div class="is-divider-vertical"></div>
        <div class="column is-fixed">
          <div class="title">
            In progress
          </div>
          <transition-group name="list" tag="div">
            <div v-for="card in cards_wip" v-bind:key="card.id"
              class="card list-item" style="margin: 0 0 30px 0">
              <div class="card-header">
                <div class="card-header-title">{{ card.title }}</div>
              </div>
              <div class="card-content">
                {{ card.description }}
              </div>
              <div class="card-footer">
                <div class="card-footer-item">
                  <a v-on:click="card.status = 'done'" class="button is-success">
                    <span></span>
                    <span class="icon" style="margin-right: 2px">
                      <font-awesome-icon icon="check-circle" />
                    </span>
                    <span class="is-hidden-touch">
                      Done
                    </span>
                  </a>
                </div>
                <div class="card-footer-item">
                  <a v-on:click="card.status = 'not_started'" class="button is-warning">
                    <span></span>
                    <span class="icon" style="margin-right: 2px">
                      <font-awesome-icon icon="stop-circle" />
                    </span>
                    <span class="is-hidden-touch">
                      Stop
                    </span>
                  </a>
                </div>
                <div class="card-footer-item">
                  <a v-on:click="card.status = 'deleted'" class="button is-danger">
                    <span></span>
                    <span class="icon" style="margin-right: 2px">
                      <font-awesome-icon icon="trash" />
                    </span>
                    <span class="is-hidden-touch">
                      Delete
                    </span>
                  </a>
                </div>
              </div>
            </div>
          </transition-group>
        </div>
        <div class="is-divider-vertical"></div>
        <div class="column is-fixed">
          <div class="title">
            Done
          </div>
          <transition-group name="list" tag="div">
            <div v-for="card in cards_done" v-bind:key="card.id"
              class="card list-item" style="margin: 0 0 30px 0">
              <div class="card-header">
                <div class="card-header-title">{{ card.title }}</div>
              </div>
              <div class="card-content">
                {{ card.description }}
              </div>
              <div class="card-footer">
                <div class="card-footer-item">
                  <a v-on:click="card.status = 'not_started'" class="button is-info">
                    <span></span>
                    <span class="icon" style="margin-right: 2px">
                      <font-awesome-icon icon="redo" />
                    </span>
                    <span class="is-hidden-touch">
                      Reset
                    </span>
                  </a>
                </div>
                <div class="card-footer-item">
                  <a v-on:click="card.status = 'deleted'" class="button is-danger">
                    <span></span>
                    <span class="icon" style="margin-right: 2px">
                      <font-awesome-icon icon="trash" />
                    </span>
                    <span class="is-hidden-touch">
                      Delete
                    </span>
                  </a>
                </div>
              </div>
            </div>
          </transition-group>
        </div>
      </div>
    </section>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <a v-on:click="showNewCardModal = true">
      <fab class="is-primary"
        :bg-color="bgColor"
      ></fab>
    </a>
    <div v-if="showNewCardModal" class="modal is-active">
      <div class="modal-background"></div>
      <div class="modal-card">
        <header class="modal-card-head">
          <p class="modal-card-title">New task</p>
          <button v-on:click="resetCloseNewCardModal" class="delete" aria-label="close"></button>
        </header>
        <section class="modal-card-body">
          <div class="field">
            <label class="label">Task title</label>
            <div class="control">
              <input class="input" type="text" placeholder="Title"
                v-model="modalContent.title"
                v-on:keyup.enter="addNewCard"
                v-on:focusout="checkTitleValidity"
                v-bind:class="{ 'is-danger': !isTitleValid }"
                >
            </div>
            <p v-if="!isTitleValid" class="help is-danger">You must enter a title</p>
          </div>
          <div class="field">
            <label class="label">Task description</label>
            <div class="control">
              <textarea class="textarea" placeholder="Description"
                v-model="modalContent.description">
              </textarea>
            </div>
          </div>
        </section>
        <footer class="modal-card-foot">
          <button v-on:click="addNewCard" class="button is-success">Add task</button>
          <button v-on:click="resetCloseNewCardModal" class="button">Cancel</button>
        </footer>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import 'bulma/css/bulma.css'
import 'bulma-divider/dist/css/bulma-divider.min.css'
import { library } from '@fortawesome/fontawesome-svg-core'
import { faTrash, faPlayCircle, faCheckCircle, faStopCircle, faRedo } 
  from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import fab from 'vue-fab'
import Vue from 'vue'

library.add(faTrash)
library.add(faPlayCircle)
library.add(faCheckCircle)
library.add(faStopCircle)
library.add(faRedo)

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
          title: "Sample take",
          description: "This is a sample description for a sample task.",
          status: 'not_started'
        },
      ],
      lastCardIndex: 0,
      bgColor: "hsl(171, 100%, 41%)",
      showNewCardModal: false,
      modalContent: {
        title: null,
        description: null
      },
      isTitleValid: true,
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
  methods: {
    addNewCard: function() {
      this.checkTitleValidity();
      if(this.isTitleValid) {
        this.lastCardIndex += 1;
        this.cards.push({
          id: this.lastCardIndex,
          title: this.modalContent.title,
          description: this.modalContent.description,
          status: "not_started"
        });
        this.resetCloseNewCardModal();
      }
    },
    checkTitleValidity: function() {
      this.isTitleValid = !!this.modalContent.title;
    },
    resetCloseNewCardModal: function() {
      this.modalContent = {
        title: null,
        description: null
      };
      this.showNewCardModal = false;
      this.showTitleEmptyWarning = false;
    }
  },
  components: {
    HelloWorld,
    fab
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
