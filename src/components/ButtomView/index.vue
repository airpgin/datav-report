<template>
  <div class="bottom-view">
    <div class="view">
      <el-card shadow="hover">
        <template #header>
          <div class="title-wrapper">
            关键词搜索
          </div>
        </template>
        <template>
          <div class="chart-wrapper">
            <div class="chart-inner">
              <div class="chart">
                <div class="chart-title">
                  搜索用户数
                </div>
                <div class="chart-data">
                  93,634
                </div>
                <v-chart :option="searchUserOption" />
              </div>
              <div class="chart">
                <div class="chart-title">
                  搜索量
                </div>
                <div class="chart-data">
                  183,232,312
                </div>
                <v-chart :option="searchUserOption" />
              </div>
            </div>
            <div class="table-wrapper">
              <el-table :data="tableData">
                <el-table-column
                  prop="rank"
                  label="排名"
                  width="180"
                />
                <el-table-column
                  prop="keyword"
                  label="关键词"
                  width="180"
                />
                <el-table-column
                  prop="count"
                  label="总搜索量"
                  align="center"
                />
                <el-table-column
                  prop="users"
                  label="搜索用户数"
                  align="center"
                />
              </el-table>
              <el-pagination
                layout="prev, pager, next"
                :total="100"
                :page-size="4"
                background
                @current-change="onPageChange"
              />
            </div>
          </div>
        </template>
      </el-card>
    </div>
    <div class="view">
      <el-card shadow="hover">
        <template #header>
          <div class="title-wrapper">
            <div class="title">
              分类销售排行
            </div>
            <div class="radio-wrapper">
              <el-radio-group
                v-model="radioSelect"
                size="small"
              >
                <el-radio-button label="品类" />
                <el-radio-button label="商品" />
              </el-radio-group>
            </div>
          </div>
        </template>
        <template>
          <div class="chart-wrapper">
            <v-chart :option="categoryOption" />
          </div>
        </template>
      </el-card>
    </div>
  </div>
</template>

<script>

export default {
  data () {
    return {
      searchUserOption: {
        xAxis: {
          type: 'category',
          boundaryGap: false
        },
        yAxis: {
          show: false,
          min: 0,
          max: 1000
        },
        series: [{
          type: 'line',
          data: [300, 200, 800, 500, 300, 400],
          areaStyle: {
            color: 'rgba(95, 187, 255, .5)'
          },
          lineStyle: {
            color: 'rgb(95, 187, 255)'
          },
          itemStyle: {
            opacity: 0
          },
          smooth: true
        }],
        grid: {
          top: 0,
          left: 0,
          bottom: 0,
          right: 0
        }
      },
      searchNumberOption: {},
      categoryOption: {},
      tableData: [
        { id: 1, rank: 1, keyword: '北京', count: 100, users: 90, range: '90%' },
        { id: 2, rank: 2, keyword: '北京', count: 100, users: 90, range: '90%' },
        { id: 3, rank: 3, keyword: '北京', count: 100, users: 90, range: '90%' },
        { id: 4, rank: 4, keyword: '北京', count: 100, users: 90, range: '90%' }
      ],
      radioSelect: '品类'
    }
  },
  mounted () {
    this.renderPieChart()
  },
  methods: {
    onPageChange (page) {
      console.log(page)
    },
    renderPieChart () {
      const mockData = [
        {
          legendname: '粉面粥店',
          value: 67,
          percent: '15.40%',
          itemStyle: {
            color: '#e7e702'
          },
          name: '粉面粥店 | 15.40%'
        },
        {
          legendname: '简餐便当',
          value: 97,
          percent: '33.30%',
          itemStyle: {
            color: '#8d7fec'
          },
          name: '简餐便当 | 33.30%'
        },
        {
          legendname: '汉堡披萨',
          value: 92,
          percent: '21.15%',
          itemStyle: {
            color: '#5085f2'
          },
          name: '汉堡披萨 | 21.15%'
        }
      ]
      this.categoryOption = {
        title: [{
          text: '品类分布',
          textStyle: {
            fontSize: 14,
            color: '#666'
          },
          left: 20,
          top: 20
        }, {
          text: '累计订单量',
          subtext: '322',
          x: '34.5%',
          y: '42.5%',
          textAlign: 'center',
          textStyle: {
            fontSize: 14,
            color: '#999'
          },
          subtextStyle: {
            fontSize: 28,
            color: '#333'
          }
        }],
        series: [{
          type: 'pie',
          name: '品类分布',
          data: mockData,
          label: {
            show: true,
            position: 'outter',
            formatter: params => params.data.legendname
          },
          labelLine: {
            show: true
          },
          itemStyle: {
            borderWidth: 4,
            borderColor: '#fff'
          },
          center: ['35%', '50%'],
          radius: ['45%', '60%']
        }],
        legend: {
          type: 'scroll',
          orient: 'vertical',
          height: 250,
          left: '70%',
          top: 'middle',
          textStyle: {
            color: '#8c8c8c'
          }
        },
        tooltip: {
          trigger: 'item',
          formatter: params => params.seriesName + '<br />' + params.marker + params.data.legendname
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.bottom-view {
  display: flex;
  width: 100%;
  box-sizing: border-box;
  .view {
    flex: 1;
    &:first-child {
      padding: 0 10px 0 0;
    }
    &:last-child {
      padding: 0 0 0 10px;
    }
    .title-wrapper {
      display: flex;
      align-items: center;
      height: 60px;
      border-bottom: 1px solid #eee;
      font-size: 14px;
      font-weight: 500;
      padding: 0 0 0 20px;
      .radio-wrapper {
        flex: 1;
        display: flex;
        justify-content: flex-end;
        padding-right: 20px;
      }
    }
    .chart-wrapper {
      display: flex;
      flex-direction: column;
      height: 452px;
      .chart-inner {
        display: flex;
        padding: 0 10px;
        margin-top: 20px;
        .chart {
          flex: 1;
          padding: 0 10px;
          .chart-title {
            color: #999;
            font-size: 14px;
          }
          .chart-data {
            font-size: 22px;
            color: #333;
            font-weight: 500;
            letter-spacing: 2px;
          }
          .echarts {
            height: 50px;
          }
        }
      }
    }
    .table-wrapper {
      flex: 1;
      margin: 20px 0;
      padding: 0 20px 20px;
      .el-pagination {
        display: flex;
        justify-content: flex-end;
        margin-top: 25px;
      }
    }
  }
}
</style>
