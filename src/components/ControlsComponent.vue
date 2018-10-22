<template>
  <div>
    <p>{{ state }}</p>
    <button :disabled="state==='on'" @click="start">Start</button>
    <button :disabled="state!=='on'" @click="pause">Pause</button>
    <button :disabled="state==='off'" @click="stop">Stop/Reset</button>
  </div>
</template>

<script>
export default {
  props: ["state"],
  methods: {
    start() {
      this.$emit('click',"start")
    },
    pause() {
      this.$emit('click',"pause")
    },
    stop() {
      this.$emit('click',"stop")
    }
  }

}

</script>

<style lang="scss">

</style>