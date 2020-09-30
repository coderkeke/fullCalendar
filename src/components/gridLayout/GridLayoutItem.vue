<template>
  <el-carousel height="100%" indicator-position="none" :arrow="configData.arrow" :autoplay="configData.autoplay">
    <el-carousel-item v-for="item of materialList" :key="item.uuid">
      
      <div class="carousel-item" v-if="item.materialType==0">
        <img :src="item.filePath" alt="">
      </div>

      <div class="carousel-item" v-if="item.materialType==1">
        <video :src="item.filePath" controls></video>
      </div>

      <div class="carousel-item" v-if="item.materialType==2">
        <a :href="item.filePath" target="_blank">{{item.materialName}}</a>
      </div>

    </el-carousel-item>
  </el-carousel>
</template>

<script>
export default {
  props: {
    gridItem: {},
    config: {
      type: Object,
      default() {
        return {};
      },
    },
  },

  data() {
    return {
      configData: {
        autoplay: false,
        arrow: "hover",
      },
    };
  },

  created() {
    this.initConfig();
  },

  methods: {
    //初始化配置--------------------------------------------
    initConfig() {
      for (const key in this.config) {
        if (
          this.config.hasOwnProperty(key) &&
          this.configData.hasOwnProperty(key)
        ) {
          this.$set(this.configData, key, this.config[key]);
        }
      }
    },
  },

  computed: {
    materialList() {
      if (!this.gridItem.hasOwnProperty("materialList")) return [];
      if (this.gridItem.materialList.length == 0) return [];
      return this.gridItem.materialList;
    },
  },
};
</script>

<style lang="scss" scoped>
.el-carousel {
  width: 100%;
  height: 100%;

  .carousel-item {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;

    img {
      width: auto;
      height: auto;
    }

    video {
      width: auto;
      height: auto;
    }
  }
}

.el-carousel__container {
  height: 100%;
}
</style>