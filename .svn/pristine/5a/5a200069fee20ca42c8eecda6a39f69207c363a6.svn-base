<template>
  <div class="ds-picker-container">
    <div style="width: calc(100% - 150px);display: flex">
      <div style="margin-left: 20px;font-size: 14px;text-align: right;padding-right: 10px" flex>日期</div>
      <div style="font-size: 15px;text-align: left;font-weight: bold;min-width: 88px">{{date}}</div>
      <div class="iconfont iconfont-a-rili" style="margin-left: 5px;cursor: pointer" @click="onClickDate"></div>
    </div>
    <div style="width: 150px;font-size: 15px;text-align: left;font-weight: bold">
      <van-radio-group v-model="shift" direction="horizontal" @change="onChangeShift">
        <van-radio name="morning_shift">早班</van-radio>
        <van-radio name="night_shift">晚班</van-radio>
      </van-radio-group>
    </div>

    <van-calendar v-model="showDatePicker" style="height: 488px" get-container="body"
                  @confirm="onConfirm" :max-date="maxDate" :min-date="minDate">
    </van-calendar>
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
        default: 'morning_shift'
      }
    },
    data () {
      return {
        shift: this.defaultShift,
        showDatePicker: false,
        date: this.defaultDate,
        maxDate: new Date(),
        minDate: new Date()
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
        this.$emit('con-change', this.date, this.shift)
      },
      onChangeShift () {
        this.$emit('con-change', this.date, this.shift)
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
  }
</style>
