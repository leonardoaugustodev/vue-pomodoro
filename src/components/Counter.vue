<template>
  <div class="counter">
    <div class="circle outside">
      <div class="circle inside">
        <span class="time">50:00</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
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
  height: 500px;
  width: 500px;
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

  /* box-shadow: 10px 10px 100px 9px rgba(19,23,50,0.75); */
  /* -webkit-box-shadow: 10px 10px 100px 9px rgba(19,23,50,0.75); */
  /* -moz-box-shadow: 10px 10px 100px 9px rgba(19,23,50,0.75); */
 

}

.outside:before{
  box-shadow: 10px 10px 10px 9px rgba(190, 48, 136, 0.75);
}
.ouside:after{
  box-shadow: 10px 10px 10px 9px rgba(19,23,50,0.75);
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
