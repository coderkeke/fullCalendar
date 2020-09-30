<template>
  <grid-layout :layout.sync="layout" :maxRows="configData.maxRows" :col-num="configData.colNum"
    :row-height="configData.rowHeight" :is-draggable="configData.isDraggable" :is-resizable="configData.isResizable"
    :is-mirrored="configData.isMirrored" :auto-size="configData.autoSize" :vertical-compact="configData.verticalCompact"
    :responsive="configData.responsive" :margin="configData.margin" :use-css-transforms="configData.useCssTransforms">
    <grid-item @moveEvent="moveEvent" v-for="(item,index) in layout" :x="item.x" :y="item.y" :w="item.w" :h="item.h"
      :i="item.i" :key="item.i" :static="configData.static">
      <div @click="addMaterial(item,index)" style="width:100%;height:100%">
        <GridLayoutItem :gridItem="item" />
      </div>
      <slot name="grid" v-bind:grid="item" />
    </grid-item>
  </grid-layout>
</template>

<script>
import VueGridLayout from "vue-grid-layout";
import GridLayoutItem from "./GridLayoutItem";
export default {
  components: {
    GridLayout: VueGridLayout.GridLayout,
    GridItem: VueGridLayout.GridItem,
    GridLayoutItem,
  },

  props: {
    layout: {
      type: Array,
      default() {
        return [];
      },
    },

    layoutConfig: {
      type: Object,
      default() {
        return {};
      },
    },
  },

  data() {
    return {
      configData: {
        colNum: 4, //定义栅格系统的列数，其值需为自然数。
        maxRows: 4, //定义最大行数。
        rowHeight: 200, //每行的高度，单位像素。
        static: false, //标识栅格元素是否为静态的（无法拖拽、调整大小或被其他元素移动）。
        isDraggable: true, //标识栅格中的元素是否可拖拽。
        isResizable: true, //标识栅格中的元素是否可调整大小。
        isMirrored: false, //标识栅格中的元素是否可镜像反转。
        autoSize: true, //标识容器是否自动调整大小。
        verticalCompact: false, //标识布局是否垂直压缩。
        responsive: false, //标识布局是否为响应式。
        margin: [0, 0], //定义栅格中的元素边距。值必须是包含两个 Number的数组，数组中第一个元素表示水平边距，第二个表示垂直边距，单位为像素。
        useCssTransforms: true, //标识是否使用CSS属性 transition-property: transform;
      },
    };
  },

  created() {
    this.initConfig();
  },

  methods: {
    //初始化配置--------------------------------------------
    initConfig() {
      for (const key in this.layoutConfig) {
        if (
          this.layoutConfig.hasOwnProperty(key) &&
          this.configData.hasOwnProperty(key)
        ) {
          this.$set(this.configData, key, this.layoutConfig[key]);
        }
      }
    },
    //添加素材--------------------------------------------
    addMaterial(item, index) {
      let data = {
        item,
        index,
      };

      this.$emit("addMaterial", data);
    },

    //移动时--------------------------------------------
    moveEvent(i, newX, newY) {
      console.log("MOVE i=" + i + ", X=" + newX + ", Y=" + newY);
    },
  },
};
</script>

<style lang="scss" scoped>
.vue-grid-layout {
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  .vue-grid-item {
    border: 1px solid #ccc;
    box-sizing: border-box;
  }
}
</style>
