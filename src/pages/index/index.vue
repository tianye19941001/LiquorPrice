<template>
  <div class="container" @click="clickHandle('test click', $event)">
    <!-- 头像获取 -->
    <!-- <div class="userinfo" @click="bindViewTap">
      <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" />
      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
      </div>
    </div> -->
    <div class="title">
      <card :text="title"></card>
    </div>
    <cardJiu></cardJiu>
    <div class="search-bar">
      <input type="text" placeholder="输入你想查询的酒名" v-model="jiuName">
      <p>Message is: {{ jiuName }}</p>
      <button @click="searchJiu">查询</button>
    </div>
    <img class="cj" src="../../images/cj.jpg" mode="widthFix" alt="">
    <form class="form-container">
      <input type="text" class="form-control" v-model="motto" placeholder="v-model" />
      <input type="text" class="form-control" v-model.lazy="motto" placeholder="v-model.lazy" />
    </form>
  </div>
</template>

<script>
import card from '@/components/card';
import cardJiu from './cardJiu';

export default {
  data() {
    return {
      title: '酱香白酒吧查价工具v1.0 图片版',
      userInfo: {},
      jiuName: '茅台王子酒',
    };
  },
  components: {
    card,
    cardJiu,
  },
  methods: {
    bindViewTap() {
      const url = '../logs/main';
      wx.navigateTo({ url });
    },
    getUserInfo() {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              this.userInfo = res.userInfo;
            },
          });
        },
      });
    },
    clickHandle(msg, ev) {
      console.log('clickHandle:', msg, ev);
    },
    searchJiu() {
      console.log();
    },
  },

  created() {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo();
  },
};
</script>

<style scoped>
.cj{
  width: 100%;
}
.search-bar input{
  height: 40px;
  line-height: 40px;
  padding: 0 12px;
  border-radius: 6px;
  border: 1rpx solid #ddd;
}
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 6rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}

.counter {
  display: inline-block;
  margin: 10px auto;
  padding: 5px 10px;
  color: blue;
  border: 1px solid blue;
}
</style>
