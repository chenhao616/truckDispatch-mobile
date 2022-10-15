<template>
  <transition name="fade">
    <router-view></router-view>
  </transition>
</template>

<script>
  export default {
    mounted() {
      this.setClientHeight()
    },
    beforeCreate() {
      this.$http({
        url: this.$http.adornUrl(`/mobile/external/getUnlodad`),
        method: 'get',
        params: this.$http.adornParams({
        })
      }).then(({data}) => {
        if (data && data.code === 0) {
          const unloads = data.unloads
          this.$store.commit('common/updateUnloads', unloads)
        } else {
        }
      })
    },
    methods: {
      setClientHeight() {
        // 设置==页面文档可视高度(随窗口改变大小)
        let val = document.documentElement['clientHeight']
        this.$store.commit('common/updateDocumentClientHeight', val)
        console.log('初始化页面可视高度=' + val)

        window.onresize = () => {
          let val = document.documentElement['clientHeight']
          this.$store.commit('common/updateDocumentClientHeight', val)
        }
      },
      loadBaseData () {

      }
    }
  }
</script>

<style>
body {
  background-color: #f2f2f2;
}
</style>
