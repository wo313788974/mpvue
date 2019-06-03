<template>
    <div class="userinfo">
      <img class="userinfo-avatar" v-if="hasUserInfo" :src="userInfo.avatarUrl" background-size="cover" />
      <button  class="btn" v-else open-type="getUserInfo" @getuserinfo="getUserInfo">获取用户信息</button>
      <div v-if="hasUserInfo" class="userinfo-nickname">
        Hello , {{userInfo.nickName}}
      </div>
      <button v-if="hasUserInfo" type="primary" class="start" @tap="start">Start Now</button>
    </div>
</template>

<script>

export default {
  data () {
    return {
      userInfo: {},
      hasUserInfo: false
    }
  },

  methods: {
    getUserDetailInfo() {
      wx.getUserInfo({
      success: (res) => {
        this.userInfo = res.userInfo
        this.hasUserInfo = true
      },
      fail: () => {
        this.hasUserInfo = false
        console.log('获取失败！')
      }
    })
    },
    getUserInfo(data) {
      if (data.target.userInfo) {
        // 获取授权
        this.getUserDetailInfo();
      }
    },
    start() {
      wx.navigateTo({url: '../home/main'})
    }
  },

  beforeMount() {
    this.getUserDetailInfo()
  }
}
</script>

<style>
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  margin-top: 50rpx;
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
  margin-top: 100rpx;
}

.usermotto,.start {
  margin-top: 100rpx;
}
.btn {
  
}

</style>
