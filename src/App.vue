<script setup>
  import dayjs from "dayjs";
  import { ref, watchEffect } from "vue";
  import numberDisplay from "./components/numberDisplay.vue";
  const numberString = ref("0.185");

  setInterval(() => {
    setTime();
  }, 1000);
  let time = ref();
  const setTime = () => {
    time.value = Date.now().valueOf();
  };

  watchEffect(() => {
    numberString.value = dayjs(time.value).format("HH:mm:ss");
  });
</script>

<template>
  <div class="app">
    <numberDisplay :numberString="numberString" />
  </div>
</template>

<style scoped lang="scss">
  .app {
    height: 100vh;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #9c9c9c;
  }
</style>
