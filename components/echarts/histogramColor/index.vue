<!--
author :"孙嘉辉"，
name :柱状图 （每个x轴上的坐标只有一个柱子 且颜色 不同）
 *简介：你觉的 有问题 请你自己去写一个，本人能力一般且时间有限
使用是直接引入就好，
传入参数；
*id:string// 必填
data：[],
Xtitle:string, // x坐标名称
Ytitle:string//  y 坐标名称
height:string+px  // eherts 的高度//
left：string+px   //柱状图上面可以点解的小圆点的位置
show :boolean // 是否显示小圆点
color ： array  //每根柱子的颜色
-->
<template>
  <div class="abc" :key="key">
    <div class="auto" :id="ids" :style="{ width: '100%', height: ht }"></div>
  </div>
</template>

<script>
export default {
  props: {
    datas: {},
    Xtitle: {
      default: "题目",
    },
    Ytitle: {
      default: "数量",
    },
    height: {
      default: "400px",
    },
    color: {
      default: ["#003366", "#006699", "#4cabce", "#e5323e"],
    },
    id: {
      default: "sun",
    },
    left: {
      default: "center",
    },
    show: {
      default: true,
    },
  },
  watch: {
    Xtitle: {
      handler(val) {
        this.xT = val;
        this.$nextTick(() => {
          this.drawLine();
        });
      },
      immediate: true,
    },
    height: {
      handler(val) {
        this.ht = val;
        this.$nextTick(() => {
          this.drawLine();
        });
      },
      immediate: true,
    },
    Ytitle: {
      handler(val) {
        this.yT = val;
        this.$nextTick(() => {
          this.drawLine();
        });
      },
      immediate: true,
    },
    datas: {
      handler(val) {
        this.dataArray = val;
        let arr = val;
        let arrLen = arr.map((el) => {
          return el.length;
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
    id: {
      handler(val) {
        this.ids = val;
        this.$nextTick(() => {
          this.drawLine();
        });
      },
      immediate: true,
    },
    key: {
      handler(val) {
        this.$nextTick(() => {
          this.drawLine();
        });
      },
      immediate: true,
    },
    left: {
      handler(val) {
        this.lf = val;
        this.$nextTick(() => {
          this.drawLine();
        });
      },
      immediate: true,
    },
    show: {
      handler(val) {
        this.flag = val;
        this.$nextTick(() => {
          this.drawLine();
        });
      },
      immediate: true,
    },
  },
  name: "hello",
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      xT: "",
      yT: "",
      ht: "",
      ids: "",
      key: 1,
      dataArray: [],
      clo: [],
      lf: "",
      seriesArr: [],
      flag: "",
    };
  },
  mounted() {
    this.drawLine();
    let that = this;
    window.onresize = function () {
      that.key++;
    };
  },
  destroyed() {
    window.onresize = null;
  },
  methods: {
    drawLine() {
      // 基于准备好的dom，初始化echarts实例
      let myChart = this.$echarts.init(document.getElementById(this.ids));
      // 绘制图表
      let that = this;
      myChart.setOption({
        color: "red",
        grid: {
          x: 30,
          y: 80,
          x2: 70,
          y2: 70,
          borderWidth: 1,
        },
        legend: {
          show: that.flag,
          icon: "circle", //  这个字段控制形状  类型包括 circle，rect ，roundRect，triangle，diamond，pin，arrow，none
          left: that.lf,
          top: "-5",
          itemWidth: 10, // 设置宽度
          itemHeight: 10, // 设置高度
          itemGap: 40, // 设置间距
        },

        dataset: {
          source: [...that.dataArray],
        },
        // { type: "category", name: that.xT }
        xAxis: [
          {
            name: that.xT,
            type: "category",
            axisLine: {
              lineStyle: {
                type: "solid",
                onZero: true,
                color: "#EAEDF1",
              },
            },

            axisLabel: {
              textStyle: {
                color: "#C2C5CB", //坐标值得具体的颜色
              },
            },
          },
        ],
        //
        yAxis: [
          {
            name: that.yT,
            axisLine: {
              lineStyle: {
                type: "solid",
                onZero: true,
                color: "rgba(225,225,225,0)",
              },
            },

            splitLine: {
              lineStyle: {
                color: "#EAEDF1",
              },
            }, //去除网格线
            splitArea: {
              lineStyle: {
                color: "#EAEDF1",
              },
            }, //保留网格区域
            axisLabel: {
              textStyle: {
                color: "#C2C5CB", //坐标值得具体的颜色
              },
            },
          },
        ],
        series: [
          {
            type: "bar",
            barWidth: 15,
            itemStyle: {
              normal: {
                color: function (params) {
                  let colorList = that.clo;
                  return colorList[params.dataIndex];
                },
              },
            },
          },
        ],
      });
    },
  },
};
</script>
<style lang='scss' scoped>
.auto {
}
</style>
