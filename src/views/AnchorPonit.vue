<template>
  <div>
    <!--锚点导航-->
    <ul class="md">
      <li @click="tabClick('#floor0')">000000</li>
      <li @click="tabClick('#floor1')">000000</li>
      <li @click="tabClick('#floor2')">000000</li>
      <li @click="tabClick('#floor3')">000000</li>
    </ul>
    <!--展示锚点-->
    <div class="comTitle" id="floor0">
      <div class="rebox">
        <div class="t1"></div>
        <div class="t2"></div>
        <div class="outTitle">行业通用数据集---0</div>
      </div>
    </div>
    <div>展示的内容</div>
    <div class="comTitle" id="floor1">
      <div class="rebox">
        <div class="t1"></div>
        <div class="t2"></div>
        <div class="outTitle">行业通用数据集---1</div>
      </div>
    </div>
    <div>展示的内容</div>
    <div class="comTitle" id="floor2">
      <div class="rebox">
        <div class="t1"></div>
        <div class="t2"></div>
        <div class="outTitle">行业通用数据集---2</div>
      </div>
    </div>
    <div>展示的内容</div>
    <div class="comTitle" id="floor3">
      <div class="rebox">
        <div class="t1"></div>
        <div class="t2"></div>
        <div class="outTitle">行业通用数据集---3</div>
      </div>
    </div>
    <div>展示的内容</div>
  </div>
</template>
<script>
export default {
  data() {
    return {
    };
  },
  methods: {
    // Tab点击
    tabClick(index) {
      this.goAnchor(index);
    },
    //锚点跳转
    goAnchor(selector) {
      var anchor = this.$el.querySelector(selector); //获取元素
      let total;
      let disFixed = document.getElementsByClassName('vux-fixed')[0];
      if (disFixed) {
        total = anchor.offsetTop - 40;
      } else {
        total = anchor.offsetTop - 80;
      }
      let distance = document.documentElement.scrollTop || document.body.scrollTop;
      // 计算每一小段的距离
      let step = total / 6;
      (function smoothDown() {
        if (distance < total) {
          distance += step;
          // 移动一小段
          document.body.scrollTop = distance;
          document.documentElement.scrollTop = distance;
          // 设定每一次跳动的时间间隔为10ms
          setTimeout(smoothDown, 10);
        } else {
          // 限制滚动停止时的距离
          document.body.scrollTop = total;
          document.documentElement.scrollTop = total;
        }
      })();
    },
  },
};
</script>
<style>
.rebox {
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
}
.t1 {
  width: 240px;
  height: 1px;
  background: #b8b2b2;
}
.t2 {
  width: 220px;
  height: 1px;
  background: #6b6b6b;
  margin-top: 6px;
  margin-left: 10px;
}
.outTitle {
  width: 114px;
  font-size: 16px;
  font-weight: bold;
  background: white;
  padding: 6px;
  position: absolute;
  top: -14px;
  left: calc((100% - 114px) / 2);
  text-align: center;
}
.comTitle {
  display: flex;
  justify-content: center;
  width: 100%;
  margin: 20px 0;
}
</style>
