<template>
  <div class="counter">
    <!-- <button @click="addProgress">Add</button> -->
    <!-- <button @click="removeProgress">Remove</button> -->
    <!-- <div class="circle outside shadow"></div> -->
    <div class="circle outside">
      <div class="circle inside">
        <ProgressCircular :progress="progress"/>
        <!-- <span class="time">50:00</span> -->
      </div>
    </div>
  </div>
</template>

<script>
import ProgressCircular from './Progress_Circular.vue';

export default {
  components:{
    ProgressCircular
  },
  created(){
    this.futureDate = new Date(this.now.getTime() + this.minutes * 60000);

    this.setTime();
  },
  data () {
    return {
      progress: 0,
      minutes: 1,
      now: new Date(),
      futureDate: undefined 
    }
  },
  methods: {
    setTime(){
      let interval = setInterval(() => {

        let partialProgress = ((this.futureDate.getTime() - new Date().getTime())/(this.minutes * 60000));

        if(partialProgress > 1) clearInterval(interval);
        else if(partialProgress < 0) partialProgress = 0;
        this.progress = 1 - partialProgress;

        
      }, 100);
    }
  },
  computed: {
    
  }

}
</script>

<style scoped>
.counter{
  height: 400px;
  width: 400px;
  display: flex;
  justify-content: center;
  align-items: center;

}
.circle{
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.outside{
  height: 100%;
  width: 100%;
  background: #586097;

  background: linear-gradient(135deg, #131732, #292b52);
  box-shadow: -30px -30px 60px #393c7280, 30px 30px 60px #13173280;
  

}

.inside{
  height: 85%;
  width: 85%;
  background: #151932;
}

.time{
  font-size: 80px;
  font-weight: 100;
}
</style>
