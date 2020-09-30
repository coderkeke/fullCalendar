<template>
  <div class="container">
    <leftY :config="config" />

    <div class="main"></div>
  </div>
</template>

<script>
import leftY from "./cpns/leftY";
import bgLine from './cpns/bgLine'

export default {
  components: {
    leftY
  },

  props: {
    config: {
      type: Object,
      default() {
        return {
          rowHeight: "50"
        };
      }
    }
  },

  data() {
    return {

      
      shapes: []
    };
  },

  created() {
    for (let index = 0; index < 24; index++) {
      this.shapes.push([{}]);
    }
  },

  methods: {}
};
</script>

<style lang="scss" scoped>
.container {
  width: 1200px;
  border: 1px solid #ccc;
  border-bottom: none;
  margin: 0 auto;
  position: relative;

  .main {
    height: 100%;
    position: relative;
  }
}
</style>
