<template>
  <div class="bg-line">
    <div
      class="bg-line-item"
      :style="{ height: config.rowHeight + 'px' }"
      v-for="index of 24"
      :key="index"
    ></div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
.bg-line {
  width: 100%;
  height: 100%;

  .bg-line-item {
    width: 100%;
    border-bottom: 1px solid #ccc;
    box-sizing: border-box;
  }
}
</style>
