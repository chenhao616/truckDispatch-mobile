<template>
  <div>
    <app-header :show-select-dept="false"></app-header>
    <div style="overflow:hidden; background-color:#ebebeb;padding: 20px;">
      <div id="topArea" class="data-panel" :style="{height: topAreaHeight+'px',minHeight:'270px'}">
        <div
          style="height: 100%; width: 100%; display: flex; justify-content: center; align-items: center; flex-direction: column;"
        >
          <div
            style="line-height: 40px; font-size: 20px; height: 40px;color:#656565 ;background-color:#e4e4e4;width:100%;text-align:center"
            id="title_div"
          >{{deviceName}}</div>
          <div id="topChart" style="height:calc(100% - 80px);width: 100%;"></div>
          <div
            style="font-size: 20px; color: #b2b2b2; height: 40px; display: flex;  justify-content: space-between;  width: 100%;  padding-left: 20px; padding-right: 20px;"
          >
            <div>{{lastTimeStr}}</div>
            <div style="color:#656565;font-size: 16px; line-height: 30px;">
              <span style="color: #468EFD">瞬时</span>
              {{lastValue}}
            </div>
          </div>
        </div>
      </div>

      <div
        id="bottomArea"
        class="data-panel"
        :style="{marginTop:'20px',height: bottomAreaHeight+'px',minHeight:'230px'}"
      >
        <div
          style="height: 100%; width: 100%; display: flex; justify-content: center; align-items: center; flex-direction: column;"
        >
          <div class="change-header" style="background-color:#e4e4e4">
            <div class="chage-image chage-pre" @click="changeDay(-1)">
              <van-icon name="arrow-left" />
            </div>
            <div style="font-size: 20px; line-height: 40px;">{{selectedDate}}</div>
            <div class="chage-image chage-next" @click="changeDay(1)">
              <van-icon name="arrow" />
            </div>
          </div>
          <div style="width:100%;text-align:center" id="dataInfo"></div>

          <div id="bottomChart" style="height:calc(100% - 40px);width: 100%;"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Header from '../../main-header.vue'

export default {
  name: 'device-density',
  components: {
    'app-header': Header,
  },
  provide () {
    return {
      // 刷新
      refresh () {
      }
    }
  },
  data() {
    return {
      topChart: null,
      bottomChart: null,
      deviceId: null,
      deviceName: '强磁前大井3#泵管道',
      lastTimeStr: '',
      lastValue: '',
      selectedDate: '',
      list: [],
      loading: false,
      finished: false,
      refreshing: false,
      intervalId: null,
    }
  },
  computed: {
    topAreaHeight: {
      get() {
        let scrHeight = this.$store.state.common.documentClientHeight
        let heightSep = (scrHeight - 40 - 20 - 44) / 10
        return heightSep * 5.5
      },
    },
    lastDivHeight: {
      get() {
        let scrHeight = this.$store.state.common.documentClientHeight
        let heightSep = (scrHeight - 40 - 20 - 44) / 10
        return heightSep * 5.5 - 60
      },
    },
    bottomAreaHeight: {
      get() {
        let scrHeight = this.$store.state.common.documentClientHeight
        let heightSep = (scrHeight - 40 - 20 - 44) / 10
        return heightSep * 4.5
      },
    },
  },
  created() {},

  mounted() {
    this.selectedDate = new Date().format2('yyyy-MM-dd')
    this.deviceId = this.$route.query.deviceId
    this.deviceName = this.$route.query.deviceName

    this.$nextTick(() => {
      this.creatTopChart()
      this.loadData()
      this.dataRefreh()
    })
  },

  destroyed() {
    // 在页面销毁后，清除计时器
    this.clear()
  },
  methods: {
    // 定时刷新数据函数
    dataRefreh() {
      // 计时器正在进行中，退出函数
      if (this.intervalId != null) {
        return
      }
      // 计时器为空，操作
      this.intervalId = setInterval(() => {
        this.loadData()
      }, 5000)
    },
    // 停止定时器
    clear() {
      clearInterval(this.intervalId) //清除计时器
      this.intervalId = null //设置为null
    },
    changeDay(num) {
      let dateTime = new Date(Date.parse(this.selectedDate))
      dateTime = dateTime.setDate(dateTime.getDate() + num)
      this.selectedDate = this.formatDate(dateTime, 'yyyy-MM-dd')
    },
    loadData() {
      this.loadLast()
      this.loadList()
    },
    creatTopChart() {
      let dataArr = 0
      let colorSet = {
        color: '#468EFD',
      }
      let option = {
        backgroundColor: '#ffffff',
        tooltip: {
          formatter: '{a} <br/>浓度值 : {c}%',
        },
        series: [
          {
            name: this.deviceName,
            type: 'gauge',
            // center: ['20%', '50%'],
            radius: '40%',
            splitNumber: 10,
            axisLine: {
              lineStyle: {
                color: [
                  [50 / 100, colorSet.color],
                  [1, '#d5d5d5'],
                ],
                width: 8,
              },
            },
            axisLabel: {
              show: false,
            },
            axisTick: {
              show: false,
            },
            splitLine: {
              show: false,
            },
            itemStyle: {
              show: false,
            },
            detail: {
              formatter: function (value) {
                if (value !== 0) {
                  return value.toFixed(1) + '%'
                } else {
                  return 0
                }
              },
              offsetCenter: [0, 82],
              textStyle: {
                padding: [0, 0, 0, 0],
                fontSize: 18,
                fontWeight: '700',
                color: '#656565',
              },
            },
            title: {
              //标题
              show: true,
              offsetCenter: [-40, 82], // x, y，单位px
              textStyle: {
                color: colorSet.color,
                fontSize: 14, //表盘上的标题文字大小
                fontWeight: 400,
                fontFamily: 'PingFangSC',
              },
            },
            data: [
              {
                name: 'Avg',
                value: dataArr,
              },
            ],
            pointer: {
              show: true,
              length: '75%',
              radius: '20%',
              width: 10, //指针粗细
            },
            animationDuration: 4000,
          },
          {
            name: '外部刻度',
            type: 'gauge',
            //  center: ['20%', '50%'],
            radius: '75%',
            min: 0, //最小刻度
            max: 100, //最大刻度
            splitNumber: 10, //刻度数量
            startAngle: 225,
            endAngle: -45,
            axisLine: {
              show: true,
              lineStyle: {
                width: 1,
                color: [[1, 'rgba(0,0,0,0)']],
              },
            }, //仪表盘轴线
            axisLabel: {
              show: true,
              color: '#4d5bd1',
              distance: 25,
              formatter: function (v) {
                switch (v + '') {
                  case '0':
                    return '0'
                  case '10':
                    return '10'
                  case '20':
                    return '20'
                  case '30':
                    return '30'
                  case '40':
                    return '40'
                  case '50':
                    return '50'
                  case '60':
                    return '60'
                  case '70':
                    return '70'
                  case '80':
                    return '80'
                  case '90':
                    return '90'
                  case '100':
                    return '100'
                }
              },
            }, //刻度标签。
            axisTick: {
              show: true,
              splitNumber: 7,
              lineStyle: {
                color: colorSet.color, //用颜色渐变函数不起作用
                width: 1,
              },
              length: -8,
            }, //刻度样式
            splitLine: {
              show: true,
              length: -15,
              lineStyle: {
                color: colorSet.color, //用颜色渐变函数不起作用
              },
            }, //分隔线样式
            detail: {
              show: false,
            },
            pointer: {
              show: false,
            },
          },
        ],
      }
      this.topChart = this.$echarts.init(document.getElementById('topChart'))
      this.topChart.setOption(option)

      window.addEventListener('resize', () => {
        this.topChart.resize()
      })
    },

    setTopChartData(data) {
      if (!this.topChart) {
        return
      }

      let value = (data / 100).toFixed(1)
      //	console.log(value)
      let option = this.topChart.getOption()
      option.series[0].data[0].value = value
      option.series[0].axisLine.lineStyle.color = [
        [value / 100, '#468EFD'],
        [1, '#d5d5d5'],
      ]

      this.topChart.setOption(option, true)
    },

    createBottomChart(data) {
      let option_data = {
        name: '浓度值',
        type: 'line',
        color: 'rgba(43, 103, 202)',
        smooth: true,
        areaStyle: {
          normal: {
            color: new echarts.graphic.LinearGradient(
              0,
              0,
              0,
              1,
              [
                {
                  offset: 0,
                  color: 'rgba(43, 103, 202, 0.3)',
                },
                {
                  offset: 0.8,
                  color: 'rgba(43, 103, 202, 0)',
                },
              ],
              false
            ),
            shadowColor: 'rgba(0, 0, 0, 0.1)',
            shadowBlur: 10,
          },
        },
        itemStyle: {
          normal: {
            lineStyle: {
              width: 1, //设置线条粗细
            },
          },
        },
        symbol: 'circle',
        symbolSize: 0,
        data: data ? data.yData : [0],
      }

      let lineY = [option_data]
      let option = {
        tooltip: {
          trigger: 'axis',
          position: function (pos, params, dom, rect, size) {
            var obj = { top: 0 }
            obj[['left', 'right'][+(pos[0] < size.viewSize[0] / 2)]] = 5
            return obj
          },
          formatter: '{b0}     {c0}',
        },
        legend: {
          data: ['00:00'],
          textStyle: {
            fontSize: 12,
            color: '#151619',
          },
          right: '4%',
        },
        grid: {
          top: '10%',
          left: '4%',
          right: '5%',
          bottom: '4%',
          containLabel: true,
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: data ? data.xData : ['00:00'],
          axisLabel: {
            textStyle: {
              color: '#151619',
            },
          },
          axisTick: { show: false },
          axisLine: {
            lineStyle: {
              width: 1,
              color: '#cccccc',
            },
          },
        },
        yAxis: {
          name: '',
          type: 'value',
          axisTick: { show: false },
          axisLine: { show: false },
        },
        series: lineY,
      }

      this.bottomChart = echarts.init(document.getElementById('bottomChart'))
      this.bottomChart.setOption(option)
      window.addEventListener('resize', () => {
        this.bottomChart.resize()
      })
    },

    setBottomChartData(data) {
      if (!this.bottomChart) {
        this.createBottomChart(data)
        return
      }

      let option = this.bottomChart.getOption()
      option.xAxis[0].data = data.xData
      option.series[0].data = data.yData

      this.bottomChart.setOption(option, true)
    },

    loadLast() {
      let fetchDeviceId = this.deviceId
      this.$http({
        url: this.$http.adornUrl(
          `/app/density/getLast?deviceId=${fetchDeviceId}`
        ),
        method: 'get',
        data: this.$http.adornData(
          {
            deviceId: fetchDeviceId,
          },
          true,
          'form'
        ),
      }).then(({ data }) => {
        if (data && data.code === 0) {
          if(data.last) {
            this.lastTimeStr = this.formatDate(
              data.last.tagTime,
              'yyyy-MM-dd hh:mm:ss'
            )
            this.lastValue = (data.last.tagValue / 100).toFixed(1) + '%'
          }else{
            this.lastTimeStr=''
            this.lastValue = '0.0%'
          }

          let avgValue = data.avg.tagValue?data.avg.tagValue:0;
          this.setTopChartData(avgValue)
        } else {
        }
      })
    },

    loadList() {
      let fetchDeviceId = this.deviceId
      this.$http({
        url: this.$http.adornUrl(`/app/density/getDayList`),
        method: 'post',
        data: this.$http.adornData(
          {
            deviceId: fetchDeviceId,
            date: this.selectedDate,
          },
          true,
          'form'
        ),
        headers: {
          'content-type': 'application/x-www-form-urlencoded;charset=utf-8',
        },
      }).then(({ data }) => {
        if (data && data.code === 0) {
          this.setBottomChartData(data)
        } else {
        }
      })
    },
  },
}
</script>

<style scoped>
.update-img {
  height: 328px;
  width: 300px;
}

.data-panel {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #ffffff;
  border-radius: 10px;
  box-shadow: 0 0 5px #0000003a;
}

.change-header {
  height: 40px;
  color: #656565;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  justify-items: center;
  width: 100%;
}

.chage-image {
  width: 40px;
  height: 40px;
  text-align: center;
  align-items: center;
  justify-content: center;
  display: flex;
  font-size: 20px;
  cursor: pointer;
}
</style>
