<template>
  <div
    @click="clickEmpty"
    id="app"
  >
    <div
      @click.stop
      class="drawWrap"
    >
      <p style="text-align:center;line-height:40px">click this blue box</p>
      <p>left:{{ posData.left }}</p>
      <p>top:{{ posData.top }}</p>
      <p>width:{{ posData.width }}</p>
      <p>height:{{ posData.height }}</p>
      <p>stick:{{ posData.stick }}</p>
      <p>rotate:{{ posData.rotate }}</p>

      <vdr
        :active="test.isActive"
        :activeable="true"
        :bg="testImage"
        :draggable="true"
        :h="test.h"
        :heightRange="[300, 20]"
        :lock="test.lock"
        :r="test.r"
        :resizeable="true"
        :rotateable="true"
        :sticks="['tl', 'tm', 'angle', 'tr', 'mr', 'ml', 'bl', 'bm', 'br']"
        :w="test.w"
        :widthRange="[300, 20]"
        :x="test.x"
        :y="test.y"
        @activated="activated"
        @dragging="dragging"
        @dragStart="dragStart"
        @resizeStart="resizeStart"
        @resizeStop="resizeStop"
        @resizing="resizing"
        @rotateStart="rotateStart"
        @rotating="rotating"
        class="test-vdr"
      ></vdr>

      <vdr
        :h="test2.h"
        :w="test2.w"
        :x="test2.x"
        :y="test2.y"
        :r="test2.r"
      >
        <vdr
          :h="test3.h"
          :w="test3.w"
          :x="test3.x"
          :y="test3.y"
        >
          <vdr
            :x="30"
            :y="50"
          ></vdr>
        </vdr>
      </vdr>
    </div>
  </div>
</template>
<script>
import testImage from "./img/test.jpg";
export default {
  data() {
    return {
      testImage,
      test: {
        id: "1",
        w: 192,
        h: 156,
        x: 170,
        y: 140,
        r: 0,
        lock: false,
        isActive: true
      },
      test2: {
        id: "2",
        w: 300,
        h: 300,
        x: 100,
        y: 350,
        r: 0,
        isActive: true
      },
      test3: {
        id: "3",
        w: 180,
        h: 180,
        x: 40,
        y: 60,
        r: 0,
        isActive: true
      },
      posData: {}
    };
  },
  computed: {},
  created() {
    let { w, h, x, y, r } = this.test;
    this.posData.width = w;
    this.posData.height = h;
    this.posData.left = x;
    this.posData.top = y;
    this.posData.rotate = r;
  },
  methods: {
    activated() {
      this.test.isActive = true;
      // console.log('active设为true:选中状态');
    },
    dragStart(pos) {
      // console.log('拖拽开始', pos);
    },
    resizeStart(pos) {
      // console.log('缩放开始', pos);
    },
    rotateStart(pos) {
      // console.log('旋转开始', pos);
    },

    dragging(pos) {
      this.posData = pos;
    },
    resizing(pos) {
      this.posData = pos;
    },
    rotating(pos) {
      this.posData = pos;
    },
    dragStop(pos) {
      // console.log('缩放结束', pos);
    },
    resizeStop(pos) {
      // console.log('缩放结束', pos);
    },
    rotateStop(pos) {
      // console.log('缩放结束', pos);
    },

    clickEmpty() {
      this.test.isActive = false;
      console.log("active设为false:移除选中状态");
    }
  }
};
</script>
<style lang="css">
@import "./style/public.css";
html,
body,
#app,
.page,
.pageWrap {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}

.drawWrap {
  width: 540px;
  height: 700px;
  position: relative;
  background-color: #fff;
  overflow: hidden;

  box-shadow: 2px 2px 10px 2px rgba(0, 0, 0, 0.2);
}
.vdr-slot p {
  width: 100%;
  line-height: 30px;
  font-size: 20px;
}
.vdr-slot {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.parentBox {
  position: absolute;
  width: 400px;
  height: 400px;
  top: 100px;
  left: 80px;
  border: 1px solid skyblue;
}
</style>
