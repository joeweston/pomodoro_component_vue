<template>
  <div id="app">
    <h2>
      <span>Pomodoro</span>
      <controls-component :state="state" @click="onClick"></controls-component>
    </h2>
    <div>
    </div>
  </div>
</template>

<script>
  import ControlsComponent from "./components/ControlsComponent";

  const [ WORKING_MINUTES, RESTING_MINUTES ] = [ 2, 2 ];
  const TICK_STATE = { 
    ON: "on",
    OFF: "off",
    PAUSED: 'paused'
  }

  export default {
    components:{
      ControlsComponent
    },
    data () {
      return  {
        state: TICK_STATE.OFF,
        working: true, // resting otherwise
        minutes: WORKING_MINUTES,
        seconds: 0,
      };
    },
    computed:{
      title: function(){
        return this.working ? "Working" : "On break";
      },
      paddedMinutes: function(){
        return this.minutes < 10 ? "0" + this.minutes: this.minutes;
      },
      paddedSeconds: function(){
        return this.seconds < 10 ? "0" + this.seconds: this.seconds;
      }
    },
    methods: {
      onClick: function(buttonType){
        switch(buttonType){
          case "start":
          this.start();
          break;
          case "pause":
          this.pause();
          break;
          case "stop":
          this.stop();
          break;
        }
      },
      start: function(){
        this.state = TICK_STATE.ON;
        this.tick(); //click immeatately commences first click
        this.interval = setInterval(this.tick, 1000);
      },
      pause: function(){
        this.state = TICK_STATE.PAUSED;
        clearInterval(this.interval);
      },
      stop: function(){
        clearInterval(this.interval);
        this.state = TICK_STATE.OFF;
        this.minutes = WORKING_MINUTES;
        this.seconds = 0;
      },
      tick: function(){
        if (this.seconds !== 0){
          this.seconds--;
        } else if (this.minutes !== 0){ //&& seconds === 0
          this.minutes--;
          this.seconds = 59;
        } else { //both minutes and seconds are zero
          // go from resting to work or visa/versa
          this.working = !this.working;
          this.minutes = this.working ? WORKING_MINUTES : RESTING_MINUTES ;
        }
      }
    }
  }
</script>

<style lang="scss">

</style>
