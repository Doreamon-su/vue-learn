<template>
  <div id="slider-confirm">
    <!-- 绿色背景 -->
    <div id="dragBg" ref="dragBg"></div>
    <!-- 滑动容器文本 -->
    <div id="dragText"></div>
    <!-- 滑块 -->
    <div id="dragHandler" @mousedown="drag" ref="dragHandler">{{count}}</div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      count: 1,
    };
  },
  methods: {
    drag: function () {
      document.onmousemove = function () {
        document.querySelector("#dragHandler").style.left =
          event.clientX - 20 + "px";
        document.querySelector("#dragBg").style.width =
          event.clientX - 20 + "px";
      };
      document.onmouseup = function () {
        document.onmousemove = null;
        document.onmouseup = null;
      };
    },
  },
};
</script>
<style>
#slider-confirm {
  position: relative;
  display: block;
  background: #e8e8e8;
  width: 300px;
  height: 33px;
  border: 2px solid #e8e8e8;
}
#dragBg {
  position: absolute;
  background-color: #7ac23c;
  width: 0px;
  height: 100%;
}
/* 滑动验证容器文本 */
#dragText {
  position: absolute;
  width: 100%;
  height: 100%;
  /* 文字水平居中 */
  text-align: center;
  /* 文字垂直居中,这里不能用百分比,因为百分比是相对原始line-height的,而非div高度 */
  line-height: 33px;
  /* 文本不允许选中 */
  user-select: none;
  -webkit-user-select: none;
}
/* 滑块 */
#dragHandler {
  position: absolute;
  width: 40px;
  height: 100%;
  cursor: move;
  background: #fff;
}
</style>