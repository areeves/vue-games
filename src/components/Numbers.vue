<template>
  <div id="numbers">
    <h2>{{ question }}</h2>
    <h1><span v-for="obj of objects">{{ obj }}</span></h1>
    <div>
      <button v-for="btn of buttons" v-on:click="clicked(btn)"> {{ btn }} </button>
    </div>
    <audio ref="sndCorrect"   src="static/sfx/correct.ogg" />
    <audio ref="sndIncorrect" src="static/sfx/incorrect.ogg" />
  </div>
</template>

<script>
const circle = ' \u25EF '
export default {
  name: 'numbers',
  data () {
    return {
      question: "How many circles are there?",
      level: 1,
      remaining: [1],
      objects: [],
      buttons: []
    }
  },
  beforeMount() {
    this.newRound()
  },
  methods: {
    newRound() {
      const num = this.remaining.pop()
      this.objects = Array(num).fill(circle)
      this.buttons = Array(this.level).fill(null).map((_,i) => i+1)
    },
    clicked(n) {
      const resetLevel = () => {
        this.remaining = Array(this.level)
          .fill(null)
          .map((_,i) => i+1)
          .sort(() => Math.random()-.5) // a silly way to shuffle
          .sort(() => Math.random()-.5) // again because I can.
      }
      if( n == this.objects.length ) {
        this.$refs.sndCorrect.play()
        if( this.remaining.length == 0 ) {
          this.level++
          resetLevel()
        }
      } else {
        this.$refs.sndIncorrect.play()
        resetLevel()
      }
      this.newRound()
    }
  }
}
</script>

<style>
button {
  //scale: 300%;
  margin-left: 10px;
  margin-right: 10px;
}
</style>

