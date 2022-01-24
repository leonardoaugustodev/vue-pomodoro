<template>
  <div class="container">
    <div class="title">pomodoro</div>
    <div class="buttons">
      <button @click.prevent="selectInterval('pomodoro')" :class="{active: isActive('pomodoro')}">pomodoro</button>
      <button @click.prevent="selectInterval('short break')" :class="{active: isActive('short break')}">short break</button>
      <button @click.prevent="selectInterval('long break')" :class="{active: isActive('long break')}">long break</button>
    </div>
    <div class="counter">
      <Counter ref="counter" :minutes="minutes"/>
    </div>
    <div class="actions">
      <button class="button start" v-if="showStartButton" @click.prevent="start">Start</button>
      <button class="button resume" v-if="showResumeButton" @click.prevent="resume">Resume</button>
      <button class="button pause" v-if="showPauseButton" @click.prevent="pause">Pause</button>
      <button class="button reset" v-if="showResetButton" @click.prevent="reset">Reset</button>
    </div>
  </div>
</template>

<script>
import Counter from './Counter.vue';

export default {
  name: 'HelloWorld',
  components: {
    Counter
  },
  data () {
    return {
      active: 'pomodoro',
      minutes: 25,
      intervalMap: {
        'pomodoro': 25,
        'short break': 5,
        'long break': 15
      },
      showStartButton: true,
      showPauseButton: false,
      showResumeButton: false,
      showResetButton: false
    }
  },
  methods: {
    isActive(value){
      console.log(value);
      return this.active === value;
    },

    selectInterval(intervalName){
      this.active = intervalName;
      this.minutes = this.intervalMap[intervalName]
      this.reset();
    },

    start(){
      this.$refs.counter.start();

      this.showStartButton = false;
      this.showResumeButton = false;
      this.showPauseButton = true;
      this.showResetButton = true;
    },

    pause(){
      this.$refs.counter.pause();

      this.showStartButton = false;
      this.showResumeButton = true;
      this.showPauseButton = false;
      this.showResetButton = true;
    },

    resume(){
      this.$refs.counter.resume();

      this.showStartButton = false;
      this.showResumeButton = false;
      this.showPauseButton = true;
      this.showResetButton = true;
    },

    reset(){
      this.$refs.counter.reset();

      this.showStartButton = true;
      this.showResumeButton = false;
      this.showPauseButton = false;
      this.showResetButton = false;
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container{
  height: calc(100% - 160px);
  padding: 80px;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}

.title{
  font-size: 24px;
  font-weight: bold;
}

.buttons{
  background: #151932;
  border-radius: 100px;
  height: 60px;
  width: 475px;

  display: flex;
  align-items: center;
  justify-content: center;
}

button {
  border-radius: 100px;
  height: 50px;
  width: 150px;
  margin: 0 3px;
  background: #151932;
  border: none;
  color: #5d617c;
  font-weight: bold;
  cursor: pointer;
}

button:hover{
  background: #1e2140;
}

button.active, button.active:hover {  
  background: #f87070;
  color: #1e223f;
}

button.start {
  background: #adf870;
}

button.pause {
  background: #f8a770;
  color: #333;
}

button.resume {
  background: #adf870;
}

button.reset {
  background: #f87070;
  color: #FFF;
}

</style>
