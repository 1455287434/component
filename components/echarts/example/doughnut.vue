<!--  -->
<template>
  <div>
    <instrument
      id="shang"
      color1="#EAC36E"
      color2="#D98B65"
      target="0.25"
    ></instrument>
  </div>
</template>

<script>
// 先引入组件
import instrument from "@/components/echarts/instrument";
export default {
  data() {
    return {

    };
  },

  components: {
    // 然后在这里注册
    instrument
  },

  computed: {},

  methods: {},
};
</script>
<style lang='scss' scoped>
</style>
