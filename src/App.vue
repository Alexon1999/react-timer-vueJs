<template>
  <h1>Reaction Timer</h1>
  <!-- data binding on disabled attribut-->
  <!-- <button v-if="!isPlaying" @click="start">play</button> -->
  <button @click="start" :disabled="isPlaying">play</button>

  <!-- we passing delay as prop (bind some data to this) -->
  <Block v-if="isPlaying" :delay="delay" @end="endGame" />

  <!-- <p v-if="showResults">Reaction time : {{ score }} ms</p> -->
  <Results v-if="showResults" :score="score" />
</template>

<script>
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";

//+ component object
export default {
  name: "App",
  components: { Block, Results },

  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false,
    };
  },

  methods: {
    start() {
      // 2000 milli seconds ms
      // Math.random() -> 0 - 1
      // Math.random() * 5000 ->  0 - 5000 ms
      // min 2000 - max 7000
      // 2-7 seconds
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      this.showResults = false;

      console.log(this.delay);
    },

    endGame(reactionTime) {
      this.score = reactionTime;

      this.isPlaying = false;
      this.showResults = true;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}

button {
  background: #0faf87;
  color: #fff;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}

/* button with the attribut disabled */
button[disabled] {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
