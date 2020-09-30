<template>
  <div class="left-Y">
    <div class="left-Y-list">
      <div class="left-Y-item" :style="{height:config.rowHeight+'px'}" v-for="index of 24" :key="index">
        {{index}}:00
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "leftY",
  props: ["config"],
};
</script>

<style lang="scss" scoped>
.left-Y {
  width: 50px;
  height: 100%;
  position: absolute;
  left: -50px;
  margin-top: 25px;

  .left-Y-item {
    line-height: 50px;
  }
}
</style>