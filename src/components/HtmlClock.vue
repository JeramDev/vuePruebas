<template>
  <div>
    <div class="container">
      <div class="clock">
        <div class="hours">{{ hours | toHuman }}</div>
        <div class="sep">:</div>
        <div class="minutes">{{ minutes | toHuman }}</div>
        <div class="sep">:</div>
        <div class="seconds">{{ seconds | toHuman }}</div>
        <div class="mode">{{ mode }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hours: '',
      minutes: '',
      seconds: '',
      mode: '-'
    }
  },
  
  methods: {
    tick() {      
      const date = new Date();
      this.hours = date.getHours();
      this.minutes = date.getMinutes();
      this.seconds = date.getSeconds();
      this.mode = this.hours >= 12 ? 'PM' : 'AM';
    }
  },

  mounted() {
    setInterval(this.tick, 1000);
  },

  filters: {
    toHuman: (value) => value.toString().padStart(2, '0')
  }
}
</script>

<style>
  /* @import url('https://fonts.googleapis.com/css?family=Orbitron&display=swap'); */

  @font-face {
    font-family: 'alarm clock';
    src: url('../assets/alarmclock.woff') format('woff');
    font-weight: normal;
    font-style: normal;
  }

  .container {
    margin: auto;
    background-color: rgb(90, 90, 90);
    height: 180px;
    width: 600px;
    display: grid;
    padding: 40px 20px 40px 20px;
    grid-template-rows: 1fr;
    grid-template-columns: 1fr;
  }

  .clock {
    background-color: rgb(0, 0, 0);
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    grid-template-rows: 1fr;
    justify-content: center;
    align-items: center;
    padding: 35px;
    color: rgb(0, 255, 0);
    font-size: 100px;
    text-align: center;
    font-family: 'alarm clock', sans-serif;
  }

  .mode {
    font-size: 40px;
    margin-left: 30px;
  }

  .sep {
    animation: 2s infinite linear blink;
  }

  @keyframes blink {
    0%,
    49% { opacity: 1; }

    50%,
    100% { opacity: 0; }
  }
  
</style>