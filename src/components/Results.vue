<template>
  <p>Reaction time : {{ score }} ms</p>

  <p class="rank">{{ rank }}</p>
</template>

<script>
export default {
  props: {
    score: Number,
  },

  data() {
    return {
      rank: null,
    };
  },

  // mounted hook
  mounted() {
    if (this.score < 250) {
      this.rank = "ninja fingers 🤞";
    } else if (this.score < 400) {
      this.rank = "rapid reflexes";
    } else {
      this.rank = "snail pace ..";
    }
  },
};
</script>

<style>
.rank {
  font-size: 1rem;
  color: #0faf87;
  font-weight: bold;
}
</style>