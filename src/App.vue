<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <a class="navbar-brand" href="#">Roll-Game</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav ml-auto">
            <li class="nav-item">
              <a class="nav-link" href="#" @click="selectedComponent = 'appHome'">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#" @click="selectedComponent = 'appHowtoplay'">How To Play</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
    <div class="content-box">
      <div class="container">
        <transition name="fade" mode="out-in">
          <component :is="selectedComponent" @startNewGame='startGame' :defaultVar="defaultVar"></component>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
import Home from './components/Home.vue';
import HowToPlay from './components/HowToPlay.vue';
import Game from './components/Game.vue';

export default {
  data () {
    return {
      defaultVar: [],
      selectedComponent: 'appHome'
    }
  },
  methods: {
    startGame(a, b, c, d) {
      this.defaultVar = [];
      this.defaultVar.push(a, b, c, d);
      this.selectedComponent = 'appGame';
    }
  },
  components: {
    appHome: Home,
    appHowtoplay: HowToPlay,
    appGame: Game
  }
}
</script>

<style>

  div.content-box {
    padding: 50px 0;
  }

  .fade-enter-active {
      animation: fade-in  0.5s ease-out forwards;
  }
  .fade-leave-active {
      animation: fade-out 0.5s ease-out forwards;
  }

  @keyframes fade-out {
      from {
          opacity: 1;
          margin-top: 0;
      }
      to {
          opacity: 0;
          margin-top: 20px;
      }
  }

  @keyframes fade-in {
      from {
          opacity: 0;
          margin-top: 20px;
      }
      to {
          opacity: 1;
          margin-top: 0px;
      }
  }
</style>
