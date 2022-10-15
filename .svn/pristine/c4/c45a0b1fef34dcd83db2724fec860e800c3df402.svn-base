<template>
  <div class="header">
    <van-row type="flex" justify="space-between" align="center">
      <van-col @click.native="onClickLeft">
        <van-icon name="arrow-left" size="20"/>
      </van-col>
      <van-col>{{title}}</van-col>
      <van-col @click.native="onClickRight" style="width: 20px;">
<!--        <van-icon name="ellipsis" size="20" v-show="showSelectDept"/>-->
      </van-col>
    </van-row>

  </div>
</template>

<script>
  import Vue from 'vue'
  import {Calendar, Col, Icon, Picker, Popup, Radio, RadioGroup, Row, Toast} from 'vant'

  Vue.use(Col)
  Vue.use(Row)
  Vue.use(Toast)
  Vue.use(Calendar)
  Vue.use(Icon)
  Vue.use(Popup)
  Vue.use(Picker)
  Vue.use(Radio)
  Vue.use(RadioGroup)

  export default {
    name: 'main-header',
    inject: ['refresh'],
    props: {
      subMenu: {
        type: String,
        default: ''
      }
    },
    data () {
      return {
        mainHead: '卡车调度'
      }
    },
    created: function () {
    },
    computed: {
      title () {
        return this.subMenu ? this.mainHead + ' - ' + this.subMenu : this.mainHead
      }
    },
    methods: {
      onClickLeft () {
        this.$router.go(-1)
      },
      onClickRight () {
        // if (this.showSelectDept) {
        //   this.showDepartment = true;
        //   // Toast('更多操作')
        // }
      }
    }
  }
</script>


<style scoped>
  .header {
    /*background: #0058a5;*/
    /*color: #fff;*/
    background: #FFFFFF;
    color: #000000;
    height: 44px;
    line-height: 44px;
    font-size: 16px;
    padding: 0 16px;
  }

  .van-nav-bar {
    background: #0058a5;
  }

  .van-col i {
    top: 5px;
  }

  div /deep/ .van-nav-bar__title,
  div /deep/ .van-nav-bar__left i,
  div /deep/ .van-nav-bar__left span {
    color: #fff;
  }
</style>
