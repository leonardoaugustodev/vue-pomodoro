<template>
  <div class="counter">
    <div class="circle outside">
      <div class="circle inside">
        <ProgressCircular
          ref="progress"
          :max="seconds"
          :remaining="remainingSeconds"
        />
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
    this.remainingSeconds = this.seconds;
  },
  data() {
    return {
      progress: 0,
      remainingSeconds: 0,
      interval: undefined,
      running: false,
      paused: false,
    };
  },
  methods: {
    start() {
      clearInterval(this.interval);

      this.running = true;
      this.paused = false;

      this.interval = setInterval(() => {
        if (this.paused) return;

        if (this.remainingSeconds < 0) {
          this.running = false;
          clearInterval(this.interval);
        }

        this.remainingSeconds = this.remainingSeconds - 1;
      }, 1000);
    },

    resume() {
      this.paused = false;
    },

    pause() {
      this.paused = true;
    },

    reset() {
      clearInterval(this.interval);
      this.running = false;
      this.paused = false;
      this.remainingSeconds = this.seconds;
    },
  },
  watch: {
    minutes: function () {
      this.reset();
    },
  },
  computed: {
    seconds() {
      return this.minutes * 60;
    },
  },
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
