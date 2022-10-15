<template>
  <div>
    <app-header />
    <div>{{this.deviceName}}</div>
  </div>
</template>

<script>
import Header from '../../main-header.vue'

export default {
  name: 'alert-detail',
  components: {
    'app-header': Header,
  },
  data() {
    return {
      alertDetail: '',
      alertId: '',
      deviceName: '',
      deviceId: '',
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
    this.deviceId = this.$route.query.deviceId
    this.deviceName = this.$route.query.deviceName
    this.alertId = this.$route.query.alertId
    console.log(this.deviceName, this.deviceId, this.alertId)
    this.loadData()
  },

  methods: {
    loadData() {
      let fetchDeviceId = this.deviceId
      this.$http({
        url: this.$http.adornUrl(
          `/app/alert/listToday?deviceId=${fetchDeviceId}`
        ),
        method: 'get',
        data: this.$http.adornData(
          {
            deviceId: this.deviceId,
          },
          true,
          'form'
        ),
      }).then(({ data }) => {
        if (data && data.code === 0) {
          this.alertDetail = data
          console.log(data)
        } else {
        }
      })
    },
  },
}
</script>

<style>
</style>
