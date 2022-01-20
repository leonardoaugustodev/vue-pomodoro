<template>
  <div class="container">
    <div class="title">pomodoro</div>
    <div class="buttons">
      <button @click.prevent="active = 'pomodoro'" :class="{active: isActive('pomodoro')}">pomodoro</button>
      <button @click.prevent="active = 'short break'" :class="{active: isActive('short break')}">short break</button>
      <button @click.prevent="active = 'long break'" :class="{active: isActive('long break')}">long break</button>
    </div>
    <div class="counter">
      <Counter />
    </div>
    <div class="settings">settings</div>
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
      active: 'pomodoro'
    }
  },
  methods: {
    isActive(value){
      console.log(value);
      return this.active === value;
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
