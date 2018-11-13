<template>
  <div class="timerclass">

    <div class="timer">
      <div id="timer-number">{{ huidigeTijd }}</div>
        <svg @click="pauze = !pauze">
          <circle r="18" cx="20" cy="20" :style="setAnimation()"></circle>
        </svg>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Timer',
  data() {
    return {
      huidigeTijd: this.start,
      pauze: false
    }
  },
  props: {
    start: Number
  },
  computed: {
    
  },
  methods: {
    setAnimation() {
      return this.finished ? {stroke: `transparent`} : {animation: `timer ${this.start}s ${this.pauze ? 'paused' : ''} linear infinite forwards`}
    },

  },
  created() {
    const interval = setInterval(() => {
      if (this.pauze) return;
      if (--this.huidigeTijd <= 0) {
         this.$emit("finish");
         clearInterval(interval);
         this.finished = true;
         this.setAnimation();
      }
    }, 1000);
  }
}
</script>


<style scoped>
  .timer {
    height: 40px;
    width: 40px;
    text-align: center;
    position: relative;
  }

  #timer-number {
    display: inline-block;
    line-height: 40px;
  }

  svg {
    position: absolute;
    top: 0;
    right: 0;
    width: 40px;
    height: 40px;
    transform: rotateY(-180deg) rotateZ(-90deg);
  }

  svg circle {
    stroke-dasharray: 113px;
    stroke-dashoffset: 0px;
    stroke-linecap: round;
    stroke-width: 2px;
    stroke: black;
    fill: none;
    /* animation: timer 10s linear infinite forwards; */
  }
</style>

<style>
  @keyframes timer {
    from {
      stroke-dashoffset: 0px;
    }
    to {
      stroke-dashoffset: 113px;
    }
  }
</style>

