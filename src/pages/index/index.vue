<template>
  <div class="container" @click="toggleVerticalDialog">
    <ZanDialog v-bind="zanDialog"/>
  </div>
</template>

<script>
import card from '@/components/card'
import ZanDialog from '../../components/zan/dialog'
export default {
  components: {
    ZanDialog, card
  },
  data () {
    return {
      motto: 'Hello World',
      userInfo: {},
      zanDialog: {
        'name': '',
        'show': false,
        'title': '',
        'content': '',
        'buttons': [],
        'buttonsShowVertical': true,
        res: {}
      }
    }
  },

  methods: {
    ...ZanDialog.methods,
    bindViewTap () {
      const url = '../logs/main'
      wx.navigateTo({ url })
    },
    getUserInfo () {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              this.userInfo = res.userInfo
            }
          })
        }
      })
    },
    clickHandle (msg, ev) {
      console.log('clickHandle:', msg, ev)
      this.toggleVerticalDialog()
    },
    toggleVerticalDialog () {
      console.log(11)
      const obj = {
        title: '奇遇',
        content: '该如何抉择呢?',
        buttonsShowVertical: true,
        buttons: [{
          text: '救她',
          color: 'red',
          type: 'cash'
        }, {
          text: '无视她',
          color: '#3CC51F',
          type: 'wechat'
        }, {
          text: '容我再想想',
          type: 'cancel'
        }]
      }
      this.showZanDialog(obj).then(({type}) => {
        console.log('=== dialog with vertical buttons === type: ' + type)
      })
    }
  },

  created () {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo()
  }
}
</script>

<style scoped>
  .container {
    padding: 44rpx 0;
    box-sizing: border-box;
    width:100%;
    height:100%;
    min-height: 100vh;
    background:url("https://www.remapcity.com/fileserver/static/mini/yori/night.png") no-repeat;
    background-size:cover;
  }
</style>
