<template>
  <div class="circular">
    <div class="inner"></div>
    <div class="number">{{progressToShow}}</div>
    <div class="circle">
      <div class="bar right">
        <div class="progress" :style="progressLeftClass"></div>
      </div>
      <div class="bar left">
        <div class="progress" :style="progressRightClass"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    remaining: {
      type: Number,
      default: 0.15
    },

    max: {
      type: Number,
      default: 0.15
    },

    // progress: {
    //   type: Number,
    //   default: 0.15
    // },
  },
  data() {
    return {
    };
  },
  methods: {
    progressRotation(isLeft){
      let deg = (this.progress * 360) - (isLeft ? 180 : 0);
      
      if(deg < 0) deg = 0;
      else if(deg > 180) deg = 180;

      return {
        'transform': `rotate(${deg}deg)`
      };
    },

    start(){
      console.log('start');
    }
       
  },
  computed: {

    progress(){
      return this.remaining / this.max;
    },
    
    progressLeftClass: function () {
      return this.progressRotation(true);
    },

    progressRightClass: function () {
      return this.progressRotation(false);
    },

    progressPercent: function () {
      return `${(this.progress * 100).toFixed(2)}%`;
    },

    progressToShow(){
      var date = new Date(null);
      date.setSeconds(this.remaining);
      return date.toISOString().substr(14, 5);
    }
  }
};
</script>

<style scoped>
.circular {
  height: 300px;
  width: 300px;
  position: relative;
  /* border: solid 1px green; */
}

.circular .inner {
  position: absolute;
  z-index: 6;
  top: 50%;
  left: 50%;
  height: 280px;
  width: 280px;
  margin: -140px 0 0 -140px;
  background: #151932;
  border-radius: 100%;
}

.circular .number {
  position: absolute;
  top: 50%;
  left: 50%;
  z-index: 10;
  transform: translate(-50%, -50%);
  font-size: 80px;
  font-weight: 500;
  color: #FFF;
}

.circular .bar {
  position: absolute;
  height: 100%;
  width: 100%;
  /* background: #f87070; */
  border-radius: 100%;
  -webkit-border-radius: 100%;
  clip: rect(0px, 300px, 300px, 150px);
}

.circular .bar .progress {
  position: absolute;
  height: 100%;
  width: 100%;
  -webkit-border-radius: 100%;
  border-radius: 100%;
  clip: rect(0, 150px, 300px, 0px);
  background: #f87070;
}

.circle .left .progress, .circle .right .progress {
  transition: all 0.5s;
}

.circle .right {
  transform: rotate(180deg);
  z-index: 3;
}

</style>
