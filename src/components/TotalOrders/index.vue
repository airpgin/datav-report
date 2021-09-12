<template>
  <common-card title="累计订单量" value="3,231,343">
    <template>
      <div id="total-orders-chart" :style="{ width: '100%', height: '100%' }" />
    </template>
    <template #footer>
      <span>昨日订单量</span>
      <span class="emphasis">2,000,000</span>
    </template>
  </common-card>
</template>

<script>
import commonCardMixin from "@/mixins/commonCardMixin";

export default {
  mixins: [commonCardMixin],
  mounted() {
    const chartDom = document.getElementById("total-orders-chart");
    const chart = this.$echarts.init(chartDom);
    chart.setOption({
      xAxis: {
        type: "category",
        show: false,
        boundaryGap: false
      },
      yAxis: {
        show: false,
      },
      series: [
        {
          type: "line",
          data: [
            "134",
            "332",
            "906",
            "583",
            "422",
            "316",
            "412",
            "710",
            "136",
            "751",
          ],
          areaStyle: {
            color: "purple",
          },
          smooth: true,
          lineStyle: {
            width: 0
          },
          itemStyle: {
            opacity: 0
          }
        },
      ],
      grid: {
        top: 0,
        right: 0,
        bottom: 0,
        left: 0
      }
    });
  },
};
</script>
