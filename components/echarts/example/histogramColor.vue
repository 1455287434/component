<!--  -->
<template>
  <div>
    <zhuEcharts :datas="dataArray" Xtitle="数量" Ytitle="个数" />
  </div>
</template>

<script>
import zhuEcharts from "@/components/echarts/histogramColor";
export default {
  name: "hello",
  components: {
    zhuEcharts,
  },
  data() {
    return {
      dataArray: [
        ["1题", 43.3],
        ["2题", 83.1 ],
        ["3题", 86.4],
        ["4题", 72.4 ],
        ["5题", 72.4 ],
        ["6题", 72.4],
        ["7题", 72.4 ],
      ],
    };
  },
  mounted() {},
  methods: {},
};
</script>
<style lang='scss' scoped>
</style>
