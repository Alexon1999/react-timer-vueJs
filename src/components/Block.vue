<template>
  <div class="block" v-if="showBlock" @click="stopTimer">
    click me
    <p>{{ delay }}</p>
  </div>
</template>

<script>
// we can use differnet lifecycle hooks (functions)
// run the code at different points during the components life cycle(initial,mount, unmount etc..)

// + All the lifecycle hooks
// initial,created -> cant access to template,data,events
// beforeMount() -> before it mount on the DOM (access to data,template,events)
// mounted() -> fetch requests
// beforeUpdate -> before the data changes , after this mounted on the DOM
// updated -> after its updated on the browser , after this mounted on the DOM
// beforeUnmount
// unMounted

export default {
  props: {
    delay: Number,
  },

  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0,
    };
  },

  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
      }, 10);
    },
    stopTimer() {
      clearInterval(this.timer);
      // console.log(this.reactionTime);

      // custom events
      this.$emit("end", this.reactionTime);
    },
  },

  // + when the component is mounted to the DOM , mounted hook
  // i want to run some code
  mounted() {
    console.log("component mounted");

    setTimeout(() => {
      this.showBlock = true;
      // console.log(this.delay);

      this.startTimer();
    }, this.delay);
    // }, this.$props.delay);
  },

  //+ if any data changes
  updated() {
    console.log("component updated");
  },

  // + when the component is deleted from DOM
  unmounted() {
    console.log("component unMounted");
  },

  beforeMount() {
    console.log("component before mounted");
  },
};
</script>

<style>
.block {
  width: 400px;
  border-radius: 20px;
  background: #0faf87;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>