<template>
  <div id="slider-confirm">
    <div id="slider-img">
      <img src="../assets/confirm.png" alt id="img" />
      <img src="../assets/patch.png" alt id="patch" />
    </div>
    <div id="slider-bar">
      <!-- 绿色背景 -->
      <div id="dragBg" ref="dragBg"></div>
      <!-- 滑动容器文本 -->
      <div id="dragText" v-if="isPass">验证通过</div>
      <!-- 滑块 -->
      <div id="dragHandler" @mousedown="drag">{{count}}</div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      count: 0, //显示百分比
      isPass: false, //是否通过验证
    };
  },
  methods: {
    drag: function () {
      var patch = document.querySelector("#patch");
      var dragHandler = document.querySelector("#dragHandler");
      var fixX = event.clientX - dragHandler.offsetLeft;
      var self = this;
      document.onmousemove = function () {
        var distanceX = event.clientX - fixX;
        if (distanceX < 0) {
          distanceX = 0;
        } else if (distanceX > 300) {
          distanceX = 300;
        }
        dragHandler.style.left = distanceX + "px";
        patch.style.left = distanceX + "px";
        document.querySelector("#dragBg").style.width = distanceX + "px";
        self._data.count = parseInt((distanceX / 300) * 100);
      };
      document.onmouseup = function () {
        if (self._data.count == 72) {
          self._data.isPass = true;
        } else {
          self._data.isPass = false;
          self._data.count = 0;
          dragHandler.style.left = 0 + "px";
          patch.style.left = 0 + "px";
          document.querySelector("#dragBg").style.width = 0 + "px";
        }
        document.onmousemove = null;
        document.onmouseup = null;
      };
    },
  },
};
</script>
<style>
#slider-img {
  position: relative;
}
#img {
  width: 330px;
  position: relative;
  left: -2px;
}
#patch {
  position: absolute;
  border: 1px solid black;
  left: 0px;
  top: 72.6px;
  width: 33px;
}
#slider-bar {
  position: relative;
  display: block;
  background: #e8e8e8;
  width: 330px;
  height: 30px;
  border: 2px solid #e8e8e8;
}
#dragBg {
  position: absolute;
  background-color: #00aeff;
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
  width: 30px;
  height: 100%;
  cursor: move;
  background: #fff;
  user-select: none;
  line-height: 33px;
}
</style>