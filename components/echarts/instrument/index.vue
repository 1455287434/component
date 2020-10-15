<!--
author :"孙嘉辉"，
name :柱状图
使用是直接引入就好，
传入参数；
target：floor, // 0.5 这种 相当于50%
color:string, // 圆环的颜色
color1:string, // 圆环的渐变色起始
color2:string, //  圆环的渐变色结束
id:string//
-->
<template>
  <div id="instrument">
    <div :id="ids" :style="{ width: '300px', height: '400px' }"></div>
  </div>
</template>

<script>
export default {
  name: "hello",
  props: {
    target: {
      default: 0.5,
    },
    color: {
      default: "yellow",
    },
    id: {},
    color1: {},
    color2: {},
  },
  watch: {
    target: {
      handler(val) {
        let f = +val;
        this.tar = f * 100 + "%";
        let right = f * 180;
        this.right = right;
        this.left = 180 - right;
        this.$nextTick(() => {
          this.drawLine();
        });
      },
      immediate: true,
    },
    id: {
      handler(val) {
        this.ids = val;
        this.$nextTick(() => {
          this.drawLine();
        });
      },
      immediate: true,
    },
    color: {
      handler(val) {
        this.clo = val;
        this.$nextTick(() => {
          this.drawLine();
        });
      },
      immediate: true,
    },
    color1: {
      handler(val) {
        this.clo1 = val;
        this.$nextTick(() => {
          this.drawLine();
        });
      },
      immediate: true,
    },
    color2: {
      handler(val) {
        this.clo2 = val;

        this.$nextTick(() => {
          this.drawLine();
        });
      },
      immediate: true,
    },
  },
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      tar: "",
      ids: "",
      clo: "",
      left: 90,
      right: 90,
      clo1: "",
      clo2: "",
    };
  },
  mounted() {
    this.drawLine();
  },
  methods: {
    drawLine() {
      // 基于准备好的dom，初始化echarts实例
      let that = this;
      let clo1 = this.clo1;
      let clo2 = this.clo2;
      if (clo1 == null) {
        clo1 = this.clo;
      }
      if (clo2 == null) {
        clo2 == this.clo;
      }
      let myChart = this.$echarts.init(document.getElementById(this.ids));
      // 绘制图表
      myChart.setOption({
        tooltip: {
          trigger: false,
          formatter: "{a} <br/>{b}: {c} ({d}%)",
        },

        graphic: {
          elements: [
            {
              type: "text",
              left: "130", // 相对父元素居中
              top: "80", // 相对父元素上下的位置
              style: {
                fill: "#333333",
                text: [that.tar],
                font: "24px Arial Normal",
              },
            },
          ],
        },

        series: [
          {
            type: "pie",
            radius: ["68%", "78%"],
            center: ["50%", "30%"],
            avoidLabelOverlap: false,
            legendHoverLink: false,
            hoverAnimation: false,
            startAngle: 180,
            selectedOffset: 0,
            labelLine: {
              show: false,
            },
            data: [
              {
                value: that.right,
                itemStyle: {
                  color: {
                    type: "linear",
                    x: 0,
                    y: 0,
                    x2: 0,
                    y2: 1,
                    colorStops: [
                      {
                        offset: 0,
                        color: clo1, // 0% 处的颜色
                      },
                      {
                        offset: 1,
                        color: clo1, // 100% 处的颜色
                      },
                    ],
                    global: false, // 缺省为 false
                  },
                },
              },
              {
                value: this.left,
                itemStyle: {
                  color: "rgba(128, 128, 128,.2)",
                },
              },
              {
                value: 180,
                name: "",
                itemStyle: {
                  color: "rgba(128, 128, 128, 0)",
                },
              },
            ],
          },
        ],
      });
    },
  },
};
</script>

<style>
#instrument {
  overflow: hidden;
  width: 300px;
  height: 130px;
  margin: 0 auto;
}
</style>
