<script setup>
  import { toRefs, watchEffect } from "vue";
  const digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
  // function useNumber() {
  //   let start = ref(0);
  //   const startAdd = () => {
  //     start.value++;
  //   };
  //   return {
  //     start,
  //     startAdd,
  //   };
  // }
  // const { start, startAdd } = useNumber();
  // // 问题 如果在同一个组件内，要多次使用useNumber  怎么保证各自的独立性

  const props = defineProps({
    numberString: String,
  });
  const { numberString } = toRefs(props);
  let numberStrArr = null;
  watchEffect(() => {
    numberStrArr = numberString.value.split("");
  });
  const digitRegexp = /\d/;
</script>

<template>
  <div class="digitWrapper" v-for="numberStr in numberStrArr" :key="numberStr">
    <span v-if="!digitRegexp.test(numberStr)" class="digitList">:</span>
    <span
      v-else
      class="digitList"
      :style="{ transform: `translate(-50%,-${numberStr * 32}px)` }"
    >
      <span v-for="digit in digits" :key="digit" class="digit">{{
        digit
      }}</span>
    </span>
  </div>
</template>

<style scoped lang="scss">
  .digitWrapper {
    margin-right: 10px;
    width: 24px;
    height: 32px;
    font-size: 24px;
    line-height: 32px;
    background-color: rgb(0, 0, 0);
    position: relative;
    border-radius: 6px;
    color: #fff;
    user-select: none;
    // overflow: hidden;
    .digitList {
      position: absolute;
      top: 0;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      flex-direction: column;
      align-items: center;
      transition: transform 500ms linear;
    }
  }
</style>
