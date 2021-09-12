<template>
  <div class="sales-view">
    <v-chart :options="data"></v-chart>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: {
        title: {
          text: 'dkfjdkjfk'
        },
        xAxis: {
          type: 'category'
        },
        yAxis: {},
        series: [
          {
            type: 'line',
            data: [100, 200, 300]
          }
        ]
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.sales-view {
  width: 100%;
  height: 100%;
}
</style>
