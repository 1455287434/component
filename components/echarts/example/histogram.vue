<!--  -->
<template>
  <div>
    <zhuEcharts :datas="dataArray" Xtitle="数量" Ytitle="个数" />
  </div>
</template>

<script>
import zhuEcharts from "@/components/echarts/histogram";
export default {
  name: "hello",
  components: {
    zhuEcharts,
  },
  data() {
    return {
      dataArray: [
        ["product", "A", "B", "C", "D"],
        ["1题", 43.3, 85.8, 93.7],
        ["2题", 83.1, 73.4, 55.1],
        ["3题", 86.4, 65.2, 82.5],
        ["4题", 72.4, 53.9, 39.1],
        ["5题", 72.4, 53.9, 39.1, 68],
        ["6题", 72.4, 53.9, 39.1, 68],
        ["7题", 72.4, 53.9, 39.1, 68],
      ],
    };
  },
  mounted() {},
  methods: {},
};
</script>
<style lang='scss' scoped>
</style>
