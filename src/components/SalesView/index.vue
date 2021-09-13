<template>
  <div class="sales-view">
    <el-card
      shadow="hover"
      :body-style="{ paddingBottom: '20px' }"
    >
      <template #header>
        <div class="menu-wrapper">
          <el-menu
            :default-active="activeIndex"
            mode="horizontal"
            class="sales-view-menu"
            @select="onMenuSelect"
          >
            <el-menu-item index="1">
              销售额
            </el-menu-item>
            <el-menu-item index="2">
              访问量
            </el-menu-item>
          </el-menu>
          <div class="menu-right">
            <el-radio-group
              v-model="radioSelect"
              size="small"
            >
              <el-radio-button label="本日" />
              <el-radio-button label="本周" />
              <el-radio-button label="本月" />
              <el-radio-button label="本年" />
            </el-radio-group>
            <el-date-picker
              v-model="date"
              type="daterange"
              range-separator="至"
              start-placeholder="开始日期"
              end-placeholder="结束日期"
              size="small"
              unlink-panels
              :picker-options="pickerOptions"
              class="date-picker"
            />
          </div>
        </div>
      </template>
      <template>
        <div class="sales-view-chart-wrapper">
          <v-chart :option="option" />
          <div class="sales-view-list">
            <div class="sales-view-title">
              排行榜
            </div>
            <div class="list-item-wrapper">
              <div
                v-for="item in rankData"
                :key="item.no"
                class="list-item"
              >
                <div :class="['list-item-no', +item.no <= 3 ? 'top-no' : '']">
                  {{ item.no }}
                </div>
                <div class="list-item-name">
                  {{ item.name }}
                </div>
                <div class="list-item-money">
                  {{ item.money }}
                </div>
              </div>
            </div>
          </div>
        </div>
      </template>
    </el-card>
  </div>
</template>

<script>
import { use } from 'echarts/core'
import { CanvasRenderer } from 'echarts/renderers'
import { BarChart } from 'echarts/charts'
import { TitleComponent } from 'echarts/components'

use([CanvasRenderer, BarChart, TitleComponent])

export default {
  data () {
    return {
      rankData: [
        {
          no: 1,
          name: '麦当劳',
          money: '23,221'
        },
        {
          no: 2,
          name: '麦当劳',
          money: '23,221'
        },
        {
          no: 3,
          name: '麦当劳',
          money: '23,221'
        },
        {
          no: 4,
          name: '麦当劳',
          money: '23,221'
        },
        {
          no: 5,
          name: '麦当劳',
          money: '23,221'
        },
        {
          no: 6,
          name: '麦当劳',
          money: '23,221'
        },
        {
          no: 7,
          name: '麦当劳',
          money: '23,221'
        }
      ],
      chartOption: {},
      pickerOptions: {
        shortcuts: [
          {
            text: '最近一周',
            onClick (picker) {
              const start = new Date()
              const end = new Date()
              start.setTime(start.getTime() - 1000 * 60 * 60 * 24 * 7)
              picker.$emit('pick', [start, end])
            }
          },
          {
            text: '最近一个月',
            onClick (picker) {
              const start = new Date()
              const end = new Date()
              start.setTime(start.getTime() - 1000 * 60 * 60 * 24 * 30)
              picker.$emit('pick', [start, end])
            }
          },
          {
            text: '最近三个月',
            onClick (picker) {
              const start = new Date()
              const end = new Date()
              start.setTime(start.getTime() - 1000 * 60 * 60 * 24 * 30 * 3)
              picker.$emit('pick', [start, end])
            }
          }
        ]
      },
      date: null,
      activeIndex: '1',
      radioSelect: '今日',
      option: {
        title: {
          text: '年度销售额',
          textStyle: { fontSize: 12, color: '#666' },
          left: 25,
          top: 20
        },
        series: [
          {
            name: 'Traffic Sources',
            type: 'bar',
            barWidth: '35%',
            center: ['10%', '60%'],
            data: [
              '988',
              '482',
              '514',
              '326',
              '562',
              '496',
              '561',
              '462',
              '245',
              '576',
              '685',
              '903'
            ]
          }
        ],
        xAxis: {
          type: 'category',
          data: [
            '1月',
            '2月',
            '3月',
            '4月',
            '5月',
            '6月',
            '7月',
            '8月',
            '9月',
            '10月',
            '11月',
            '12月'
          ],
          axisTick: {
            alignWithLabel: true,
            lineStyle: {
              color: '#999'
            }
          },
          axisLine: {
            lineStyle: {
              color: '#999'
            }
          },
          axisLabel: {
            color: '#333'
          }
        },
        yAxis: {
          axisTick: {
            show: false
          },
          axisLine: {
            show: false
          },
          splitLine: {
            lineStyle: {
              type: 'dotted',
              color: '#eee'
            }
          }
        },
        color: ['#3398db'],
        grid: {
          top: 70,
          left: 60,
          right: 60,
          bottom: 50
        }
      }
    }
  },
  methods: {
    onMenuSelect (index) {
      this.activeIndex = index
      console.log(this.activeIndex)
    }
  }
}
</script>

<style lang="scss" scoped>
.sales-view {
  margin-top: 20px;
  height: 400px;
  .menu-wrapper {
    position: relative;
    display: flex;
    .sales-view-menu {
      width: 100%;
      padding-left: 20px;
      .el-menu-item {
        height: 50px;
        line-height: 50px;
        margin: 0 20px;
      }
    }
    .menu-right {
      position: absolute;
      height: 50px;
      top: 0;
      right: 20px;
      display: flex;
      align-items: center;
      justify-content: flex-end;
      .date-picker {
        margin-left: 20px;
      }
    }
  }
  .sales-view-chart-wrapper {
    display: flex;
    height: 270px;
    .echarts {
      flex: 0 0 70%;
      width: 70%;
      height: 100%;
    }
    .sales-view-list {
      flex: 1;
      width: 100%;
      height: 100%;
      overflow: hidden;
      .sales-view-title {
        margin-top: 20px;
        font-size: 12px;
        color: #666;
        font-weight: 500;
      }
      .list-item-wrapper {
        margin-top: 15px;
        .list-item {
          display: flex;
          align-items: center;
          font-size: 12px;
          height: 20px;
          padding: 6px 20px 6px 0;
          .list-item-no {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 20px;
            height: 20px;
            color: #333;
            &.top-no {
              border-radius: 50%;
              background-color: #333;
              color: #eee;
              font-weight: 500;
            }
          }
          &-name {
            margin-left: 10px;
            color: #333;
          }
          &-money {
            flex: 1;
            text-align: right;
          }
        }
      }
    }
  }
}
</style>
