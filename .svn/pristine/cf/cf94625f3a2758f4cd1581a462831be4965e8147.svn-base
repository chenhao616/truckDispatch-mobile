<template>
  <div id="app" :style="{height:fullHeight+'px',background:'#f2f2f2'}">
    <app-header class="app-header" :sub-menu="activeTabName"></app-header>
    <div class="tabBar">
      <van-tabbar route fixed v-model="active" active-color="#0058a5">
        <van-tabbar-item replace to="/overview" class="iconfont iconfont-zonglan">
          <span>总览</span>
        </van-tabbar-item>
        <van-tabbar-item replace to="/truckList" class="iconfont iconfont-liebiao_kache">
          <span>卡车列表</span>
        </van-tabbar-item>
        <van-tabbar-item replace to="/exList" class="iconfont iconfont-liebiao_dianchan">
          <span>电铲列表</span>
        </van-tabbar-item>
        <van-tabbar-item replace to="/outsource" class="iconfont iconfont-liebiao_waiwei">
          <span>外委车辆</span>
        </van-tabbar-item>
      </van-tabbar>
    </div>
    <div class="main-view" v-if="!$store.state.common.contentIsNeedRefresh" style="position: fixed;top:0px;left: 0px;right: 0px;">
      <router-view/>
    </div>
  </div>
</template>

<script>
  import Header from './main-header'

  export default {
    provide () {
      return {
        // 刷新
        refresh () {
          this.$store.commit('common/updateContentIsNeedRefresh', true)
          this.$nextTick(() => {
            this.$store.commit('common/updateContentIsNeedRefresh', false)
          })
        }
      }
    },
    data () {
      return {
        active: 0
      }
    },
    computed: {
      fullHeight: {
        get () {
          let scrHeight = this.$store.state.common.documentClientHeight
          return scrHeight
        }
      },
      activeTabName: {
        get () {
          if (this.$route.name === 'overview') {
            return ''
          } else {
            return this.$route.meta.title
          }
        }
      }
    },
    components: {
      'app-header': Header
    },
    mounted () {
      this.tabbarActive()
    },
    watch: {
      $route (to, from) {
        // 对路由变化作出响应
        this.tabbarActive()
      }
    },
    methods: {
      tabbarActive () {
        // const href = window.location.href.split('#/')[1]
        // for (let i = 0; i < 4; i++) {
        //   if (href === this.tabbar[i]) {
        //     // this.active=i;
        //   }
        // }
      }
    }
  }
</script>

<style scoped>
  div /deep/ .van-tabbar-item__text {
    font-size: 14px;
    margin-top: 4px;
  }

  .van-tabbar {
    background-color: #f8f8f8;
    box-shadow: 0 -2px 4px rgba(0, 0, 0, 0.1);
    height: 64px;
  }

  .van-tabbar-item--active {
    background-color: #f8f8f8;
  }

  .iconfont {
    font-size: 28px;
  }

  .app-header {
    position: fixed;
    top: 0px;
    width: 100%;
    z-index: 888;
  }

  .main-view {
    padding-top: 44px;
    padding-bottom: 64px;
    overflow: hidden;
  }
</style>
