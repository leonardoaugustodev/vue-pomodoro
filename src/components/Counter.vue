<template>
  <div class="counter">
    <!-- <div class="circle outside shadow"></div> -->
    <div class="circle outside">
      <div class="circle inside">
        <ProgressCircular />
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
  data () {
    return {
    }
  },
  methods: {
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
