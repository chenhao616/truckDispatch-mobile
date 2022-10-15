<template>
  <div class="ds-picker-container">
    <div style="width: 110px;display: flex;margin-left: 10px;" @click="onClickDate">
      <div class="iconfont iconfont-riqi" style="margin-left: 0px;cursor: pointer;font-size: 24px; line-height: 22px;" ></div>
      <div style="font-size: 15px;text-align: left;font-weight: bold;min-width: 88px">{{date}}</div>
    </div>
    <div style="width: 60px;display: flex;margin-left: 10px;" @click="onClickShift">
      <div class="iconfont iconfont-banci" style="margin-left: 5px;cursor: pointer;font-size: 24px; line-height: 22px;" ></div>
      <div style="width: 30px;font-size: 15px;text-align: left;font-weight: bold">{{shiftName}}</div>
    </div>
    <div style="width: 60px;display: flex;margin-left: 10px;"  @click="onClickPoint">
      <div class="iconfont iconfont-xiedian" style="margin-left: 5px;cursor: pointer;font-size: 24px; line-height: 22px;"></div>
      <div style="width: 30px;font-size: 15px;text-align: left;font-weight: bold">{{pointName}}</div>
    </div>
    <div style="flex: 1;display: flex;justify-content: flex-end;padding-right: 10px">
      <div style="width: auto;font-size: 18px;text-align: left;font-weight: bold;color: #25f325;text-align: right">{{countData}}次</div>
    </div>

    <van-calendar v-model="showDatePicker" style="height: 488px" get-container="body"
                  @confirm="onConfirm" :max-date="maxDate" :min-date="minDate"></van-calendar>
    <van-popup v-model="shiftShow" position="bottom" get-container="body">
      <van-picker :show-toolbar="true" :columns="shiftColumns"
                  @confirm="onShiftConfirm" @cancel="onShiftCancel" :default-index="0"/>
    </van-popup>
    <van-popup v-model="pointShow" position="bottom" get-container="body">
      <van-picker :show-toolbar="true" :columns="pointColumns"
                  @confirm="onPointConfirm" @cancel="onPointCancel" :default-index="0"/>
    </van-popup>
  </div>
</template>

<script>
  import Vue from 'vue'
  import {Calendar, Col, Icon, Picker, Popup, Radio, RadioGroup, Row} from 'vant'

  Vue.use(Col)
  Vue.use(Row)
  Vue.use(Calendar)
  Vue.use(Icon)
  Vue.use(Popup)
  Vue.use(Picker)
  Vue.use(Radio)
  Vue.use(RadioGroup)

  export default {
    name: 'date-shift-picker',
    props: {
      defaultDate: {
        type: String,
        default: ''
      },
      defaultShift: {
        type: String,
        default: ''
      },
      defaultPoint: {
        type: String,
        default: ''
      },
      countData: {
        type: Number,
        default: 9999
      }
    },
    watch: {
      defaultShift (to, from) {
        this.shift = to
        if (this.shift === 'morning_shift') {
          this.shiftName = '早班'
        } else if (this.shift === 'night_shift') {
          this.shiftName = '晚班'
        } else {
          this.shiftName = '班次'
        }
      },
      defaultPoint (to, from) {
        this.point = to
        if (this.point === 'AA') {
          this.pointName = '岩破'
        } else if (this.point === 'BB') {
          this.pointName = '北破'
        } else {
          this.pointName = '班次'
        }
      }
    },
    data () {
      return {
        showDatePicker: false,
        date: this.defaultDate,
        maxDate: new Date(),
        minDate: new Date(),
        shiftShow: false,
        shiftColumns: ['早班', '晚班'],
        shift: 'morning_shift',
        shiftName: '早班',
        pointShow: false,
        pointColumns: ['岩破', '北破'],
        point: 'AA',
        pointName: '岩破'
      }
    },
    created: function () {
      const today = new Date()
      this.minDate = new Date(today.getFullYear(), today.getMonth() - 1, 1)
    },
    methods: {
      onClickDate () {
        this.showDatePicker = true
      },
      onConfirm (date) {
        this.showDatePicker = false
        this.date = this.formatDate(date, 'yyyy-MM-dd')
        this.$emit('con-change', this.date, this.shift, this.point)
      },

      onClickShift () {
        this.shiftShow = true
      },
      onShiftConfirm (value, index) {
        this.shiftName = value

        if (value === '早班') {
          this.shift = 'morning_shift'
        } else if (value === '晚班') {
          this.shift = 'night_shift'
        } else {
          this.shift = ''
        }
        this.shiftShow = false
        this.$emit('con-change', this.date, this.shift, this.point)
      },
      onShiftCancel () {
        this.shiftShow = false
      },
      onClickPoint () {
        this.pointShow = true
      },
      onPointConfirm (value, index) {
        this.pointName = value
        if (value === '岩破') {
          this.point = 'AA'
        } else if (value === '北破') {
          this.point = 'BB'
        } else {
          this.point = ''
        }
        this.pointShow = false
        this.$emit('con-change', this.date, this.shift, this.point)
      },
      onPointCancel () {
        this.pointShow = false
      }
    }
  }
</script>

<style scoped>
  .ds-picker-container {
    width: calc(100% - 32px);
    background-color: #0058a5;
    color: #ffffff;
    display: flex;
    flex-direction: row;
    height: 40px;
    align-items: center;
    border-radius: 5px;
    margin: 16px;
    justify-content: space-between;
  }
</style>
