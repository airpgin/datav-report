<template>
  <common-card title="今日交易用户数" value="42,232">
    <template>
      <div id="today-users-chart" :style="{width: '100%', height: '100%'}"></div>
    </template>
    <template #footer>
      <span>退货率</span>
      <span class="emphasis">5.14%</span>
    </template>
  </common-card>
</template>

<script>
import commonCardMixin from '@/mixins/commonCardMixin'

export default {
  mixins: [commonCardMixin],
  mounted() {
    const chartDom = document.getElementById("today-users-chart");
    const chart = this.$echarts.init(chartDom);
    chart.setOption({
      color: ['#3398db'],
      series: {
        type: 'bar',
        data: ['988', '482', '514', '326', '562', '496', '561', '462', '245', '576', '685', '903'],
        barWidth: '50%'
      },
      xAxis: {
        show: false,
        type: 'category',
        data: ['01:00', '02:00', '03:00', '04:00', '05:00', '06:00', '07:00', '08:00', '09:00', '10:00', '11:00', '12:00']
      },
      yAxis: {
        show: false
      },
      grid: {
        top: 0,
        bottom: 0,
        left: 0,
        right: 0
      }
    })
  }
}
</script>

<style lang="scss" scoped>

</style>
