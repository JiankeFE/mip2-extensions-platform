<template>
  <div class="wrapper"/>
</template>

<script>
import base from '../../common/utils/base'
export default {
  props: {
    globaldata: {
      type: Object,
      default: function () { return {} }
    }
  },
  data () {
    return {}
  },
  created () {
    console.log('创建数据')
    base.setHtmlRem()
    console.log(this.globaldata)
  },
  mounted () {
    console.log('这里是选择城市页面 !')

    this.$element.customElement.addEventAction('setcity', (event, str) => {
      let obj = {
        ordercity: str,
        kilometer: 0,
        moveInAddress: {
          localtion: {
            address: '',
            city: '',
            province: '',
            lat: '',
            lng: '',
            title: ''
          },
          address: '',
          phone: ''
        },
        moveOutAddress: {
          localtion: {
            address: '',
            city: '',
            province: '',
            lat: '',
            lng: '',
            title: ''
          },
          address: '',
          phone: ''
        }
      }
      let datas = base.mipExtendData(this.globaldata, obj)
      base.mipSetGlobalData(obj)

      console.log('查看数据:' + JSON.stringify(datas, null, 2))
      base.setSession(datas)

      setTimeout(() => {
        MIP.viewer.page.back()
      }, 200)
    })
  },
  methods: {}
}
</script>

<style scoped>
.mip-group-selection-content {
  overflow-x: hidden;
  overflow-y: scroll;
  -webkit-overflow-scrolling: touch;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  padding: 0 8px 0 8px;
  color: #333;
}

.mip-group-selection-group {
  margin-top: 18px;
}

.mip-group-selection-title {
  font-weight: bold;
  color: #38f;
  padding: 0 10px;
}

.mip-group-selection-part-history {
  display: none;
}

.mip-group-selection-btn {
  height: 38px;
  line-height: 38px;
  text-align: center;
  background: #f8f8f8;
}

.mip-group-selection-item {
  height: 39px;
  border-bottom: 1px solid #eee;
  line-height: 39px;
  padding: 0 10px;
  display: block;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0.1);
}
.mip-group-selection-item.down {
  background: rgba(0, 0, 0, 0.1);
}

.mip-group-selection-sidebar-wrapper {
  top: 0;
  right: 10px;
  bottom: 0;
  margin: 10px 0;
}

.mip-group-selection-sidebar {
  z-index: 50;
  right: 7px;
  overflow: scroll;
  -webkit-overflow-scrolling: touch;
  box-sizing: border-box;
  max-height: 100%;
  padding: 20px 0;
  border: 1px solid rgba(0, 0, 0, 0.05);
  text-align: center;
  color: #666;
  border-radius: 10px;
  background: rgba(255, 255, 255, 0.5);
}

.mip-group-selection-link {
  display: block;
  padding: 0 10px;
  font-size: 13px;
  font-weight: bold;
  line-height: 3;
  color: #38f;
  border-radius: 50%;
}

.mip-group-selection-letter-top {
  position: absolute;
  z-index: 40;
  top: 44px;
  left: 0;
  display: none;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  width: 100%;
  height: 50px;
  padding-left: 16px;
  line-height: 50px;
  background: #fff;
}

.mip-group-selection-large-char {
  position: absolute;
  top: 50%;
  left: 50%;
  display: none;
  width: 78px;
  height: 78px;
  margin-top: -39px;
  margin-left: -39px;
  font-size: 36px;
  line-height: 78px;
  text-align: center;
  color: #fff;
  border-radius: 3px;
  background: rgba(51, 51, 51, 0.4);
}
</style>
