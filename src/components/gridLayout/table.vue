<template>
  <div ref="container" id="container" class="container">
    <GridLayout @addMaterial="addMaterial" :layout='gridLayoutList'>
    </GridLayout>
  </div>
</template>

<script>
import GridLayout from "./GridLayout";
export default {
  components: {
    GridLayout,
  },
  data() {
    return {

      //栅格布局数据
      gridLayoutList: [
        //i=>id;x=>列;y=>行; w=>初始宽度;h=>初始高度;  //0 图片  1 视频 2连接
        {
          x: 0,
          y: 0,
          w: 2,
          h: 2,
          i: "0",
          materialList: [
            {},{},{}
          ], //素材列表对象 必填 不然监听不到
          type: 0,
        },
        {
          x: 2,
          y: 0,
          w: 1,
          h: 1,
          i: "1",
          materialList: [],
          type: 0,
        },
        {
          x: 2,
          y: 1,
          w: 1,
          h: 1,
          i: "2",
          materialList: [],
          type: 0,
        },
      ],
    };
  },

  methods: {
    addMaterial(data) {
      let materialList = [
        {
          uuid: 1,
          materialType: 0,
          filePath:
            "https://dss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=2534506313,1688529724&fm=26&gp=0.jpg",
          materialName: "图片",
        },
        {
          uuid: 2,
          materialType: 1,
          filePath: "./11.mp4",
          materialName: "视频",
        },
        {
          uuid: 3,
          materialType: 2,
          filePath:
            "http://192.168.5.114:8070/doc.html#/default/LetterSendModelController/insertUsingPOST_6",
          materialName: "连接",
        },
      ];
      let gridLayoutItem = data.item;
      gridLayoutItem.materialList = materialList;
      this.$set(this.gridLayoutList, data.index, gridLayoutItem);
      // console.log(this.gridLayoutList);
    },
  },
};
</script>

<style lang="scss" scoped>
.container {
  width: 900px;
  height: 800px;
  margin: 0 auto;
  box-sizing: border-box;
  border: 1px solid #ccc;
}
</style>
