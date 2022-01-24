<template>
  <div class="counter">
    <!-- <button @click="addProgress">Add</button> -->
    <!-- <button @click="removeProgress">Remove</button> -->
    <!-- <div class="circle outside shadow"></div> -->
    <div class="circle outside">
      <div class="circle inside">
        <ProgressCircular ref="progress" :progress="progress" />
        <!-- <span class="time">50:00</span> -->
      </div>
    </div>
  </div>
</template>

<script>
import ProgressCircular from "./Progress_Circular.vue";

export default {
  props: {
    minutes: {
      type: Number,
      default: 25,
    },
  },
  components: {
    ProgressCircular,
  },
  created() {
    this.setTime();
  },
  data() {
    return {
      progress: 0,
      startDate: undefined,
      futureDate: undefined,
      interval: undefined,
      start: false,
      pause: false,
    };
  },
  methods: {
    setTime() {
      if (!this.start) return;

      clearInterval(this.interval);

      this.startDate = new Date();
      this.futureDate = new Date(
        this.startDate.getTime() + this.minutes * 60000
      );

      this.interval = setInterval(() => {
        if (this.pause) {
          this.futureDate = new Date(
            this.futureDate.getTime() + 1000
          );

          return;
        }

        let partialProgress =
          (this.futureDate.getTime() - new Date().getTime()) /
          (this.minutes * 60000);

        if (partialProgress > 1) clearInterval(this.interval);
        else if (partialProgress < 0) partialProgress = 0;
        this.progress = 1 - partialProgress;
      }, 1000);
    },

    setStart(isResume) {
      this.start = true;
      this.pause = false;

      if (!isResume) this.setTime();
    },

    setPause() {
      this.pause = true;
      this.start = false;
    },
  },
  watch: {
    minutes: function () {
      this.setTime();
    },
  },
  computed: {},
};
</script>

<style scoped>
.counter {
  height: 400px;
  width: 400px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.circle {
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.outside {
  height: 100%;
  width: 100%;
  background: #586097;

  background: linear-gradient(135deg, #131732, #292b52);
  box-shadow: -30px -30px 60px #393c7280, 30px 30px 60px #13173280;
}

.inside {
  height: 85%;
  width: 85%;
  background: #151932;
}

.time {
  font-size: 80px;
  font-weight: 100;
}
</style>
