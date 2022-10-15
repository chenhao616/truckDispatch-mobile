<!-- 卡车列表 -->
<template>
  <div class="monitor" :style="{ height: fullHeight + 'px' }">

    <DateShiftPicker :default-date="selectedDate" :default-shift="selectedShift" @con-change='onConditionChange'></DateShiftPicker>

    <el-table :data="list" class="monitor-data" :height="fullHeight - 72" >
      <el-table-column fixed prop="truck_name"  min-width="85" label="卡车" />
      <el-table-column  prop="truck_type" label="车型"  min-width="85" align="center"/>
      <el-table-column prop="ore" label="矿石"  min-width="85" align="right" header-align="right"/>
      <el-table-column prop="rock" label="岩石" min-width="85" align="right" header-align="right"/>
      <el-table-column prop="oreamount" label="矿石产量" min-width="85" align="right" header-align="right"/>
      <el-table-column prop="averageDistanceOre" label="矿平运距" min-width="85" align="right" header-align="right"/>
      <el-table-column prop="oredistances" label="矿总运距" min-width="85" align="right" header-align="right"/>
      <el-table-column prop="orerpk" label="矿周转量" min-width="85" align="right" header-align="right"/>
      <el-table-column prop="rockamount" label="岩石产量" min-width="85" align="right" header-align="right"/>
      <el-table-column prop="averageDistanceRock" label="岩平运距" min-width="85" align="right" header-align="right"/>
      <el-table-column prop="rockdistances" label="岩总运距" min-width="85" align="right" header-align="right"/>
      <el-table-column prop="rockrpk" label="岩周转量" min-width="85" align="right" header-align="right"/>
      <el-table-column prop="total" label="总运次" min-width="85" align="right" header-align="right"/>
      <el-table-column prop="amount" label="总产量" min-width="85" align="right" header-align="right"/>
      <el-table-column prop="averageDistance" label="平均运距" min-width="85" align="right" header-align="right"/>
      <el-table-column prop="distances" label="总运距" min-width="85" align="right" header-align="right"/>
      <el-table-column prop="rpk" label="总周转量" min-width="85" align="right" header-align="right"/>
<!--      <el-table-column prop="deviceName" label="合计" width="90" />-->
<!--      <el-table-column prop="uploadTime" label="上报时间"  width="120" align="center" :formatter="formatterTime"/>-->
    </el-table>
  </div>
</template>

<script>
  import Vue from 'vue'
  import {Col, Grid, GridItem, Image as VanImage, Row, Swipe, SwipeItem} from 'vant'
  import DateShiftPicker from './common/date-shift-picker'

  Vue.use(VanImage)
  Vue.use(Col)
  Vue.use(Row)
  Vue.use(Grid)
  Vue.use(GridItem)
  Vue.use(Swipe)
  Vue.use(SwipeItem)

  export default {
    name: 'main-monitor',
    components: {
      'DateShiftPicker': DateShiftPicker
    },
    data () {
      return {
        list: [],
        loading: false,
        finished: false,
        refreshing: false,
        intervalId: null,

        selectedDate: '',
        selectedShift: ''
      }
    },
    computed: {
      fullHeight: {
        get () {
          let scrHeight = this.$store.state.common.documentClientHeight
          return scrHeight - 110
        }
      }
    },
    created () {
      this.selectedDate = this.formatDate(new Date(), 'yyyy-MM-dd')
      this.selectedShift = 'morning_shift'

      this.loadData()
    },
    destroyed () {
      // 在页面销毁后，清除计时器
      this.clear()
    },
    methods: {
      // 定时刷新数据函数
      startRefreshTimer () {
        // 计时器正在进行中，退出函数
        if (this.intervalId != null) {
          return
        }
        // 计时器为空，操作(十分钟)
        this.intervalId = setInterval(() => {
          this.loadData()
        }, 1000 * 60 * 10)
      },
      // 停止定时器
      clear () {
        clearInterval(this.intervalId)
        this.intervalId = null
      },
      formatterTime (row, column, cellValue) {
        return cellValue ? this.formatDate(cellValue, 'MM-dd hh:mm') : ''
      },
      onConditionChange (date, shift) {
        this.selectedDate = date
        this.selectedShift = shift
        this.loadData()
      },
      getSummaries (param) {
        const { columns, data } = param
        const sums = []
        columns.forEach((column, index) => {
          if (index === 0) {
            sums[index] = '总价'
            return
          }
          const values = data.map(item => Number(item[column.property]))
          if (!values.every(value => isNaN(value))) {
            sums[index] = values.reduce((prev, curr) => {
              const value = Number(curr)
              if (!isNaN(value)) {
                return prev + curr
              } else {
                return prev
              }
            }, 0);
            sums[index] += ' 元'
          } else {
            sums[index] = 'N/A'
          }
        })
        return sums
      },
      loadData () {
        this.loading = false
        this.finished = true

        this.$http({
          url: this.$http.adornUrl(`/mobile/external/multipleTruckList`),
          method: 'get',
          params: this.$http.adornParams({
            days: this.selectedDate,
            classes: this.selectedShift
          })
        }).then(({data}) => {
          if (data && data.code === 0) {
            this.list = data.list
            this.loading = false
            this.finished = true
          } else {
          }
        })
      }
    }
  }
</script>

<style scoped>

  .monitor {
    width: 100%;
    padding-left:0px;
    padding-top: 0px;
    padding-right: 0px;
    overflow-y: auto;
    margin: 0 auto;
  }
  .monitor-data{
    overflow-y: auto;
  }

  div /deep/ .van-grid-item__content {
    background: none;
    padding: 8px;
  }

  .history-list-item {
    padding-left: 24px;
  }

  div /deep/ .van-grid-item__content::after {
    border-width: 0;
  }

  .van-image {
    box-shadow: 0 0 4px rgba(0, 0, 0, 0.3);
  }

  .tag-value {
    width: 50px;
    text-align: right;
  }

  .tag-time {
    font-size: 12px;
    transform: scale(0.8);
    /*color: #a3a6bd;*/
    padding-top: 5px;
    overflow: hidden;
    height: 21px;
  }
  .el-table /deep/ .warning-row {
    color: #cf0000;
  }
  .monitor /deep/ .el-table th{
    background-color: #e4e4e4;
    color: #555658;
    border-right: 2px solid #faf7f7;
  }
  .monitor /deep/ .el-table th:last-child{
    border: none;
  }
  .monitor /deep/ .van-radio__label{
    color: white;
  }
</style>
