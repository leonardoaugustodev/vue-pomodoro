<template>
  <div class="container">
    <div class="title">pomodoro</div>
    <div class="buttons">
      <button @click.prevent="selectInterval('pomodoro')" :class="{active: isActive('pomodoro')}">pomodoro</button>
      <button @click.prevent="selectInterval('short break')" :class="{active: isActive('short break')}">short break</button>
      <button @click.prevent="selectInterval('long break')" :class="{active: isActive('long break')}">long break</button>
    </div>
    <div class="counter">
      {{minutes}}
      <Counter ref="counter" :minutes="minutes"/>
    </div>
    <div class="actions">
      <button @click.prevent="start">Start</button>
      <button @click.prevent="pause">Pause</button>
      <button @click.prevent="resume">Resume</button>
      <button>Settings</button>
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
      }
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
    },

    start(){
      this.$refs.counter.setStart(false);
    },

    pause(){
      this.$refs.counter.setPause();
    },

    resume(){
      this.$refs.counter.setStart(true);
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

</style>
