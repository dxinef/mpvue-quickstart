<template>
  <div class="container" @click="clickHandle('test click', $event)">

    <div class="userinfo" @click="bindViewTap">
      <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" />
      <div class="userinfo-nickname">
        <card :text="userInfo.nickName"></card>
      </div>
    </div>

    {{#vant}}
    <van-tag>标签</van-tag>
    <van-tag type="danger">标签</van-tag>
    <van-tag type="primary">标签</van-tag>
    <van-tag type="success">标签</van-tag>
    {{/vant}}

    <div class="usermotto">
      <div class="user-motto">
        <card :text="motto"></card>
      </div>
    </div>

    <form class="form-container">
      <input type="text" class="form-control" v-model="motto" placeholder="v-model" />
      <input type="text" class="form-control" v-model.lazy="motto" placeholder="v-model.lazy" />
    </form>
    {{#if vuex}}
    <a href="/pages/counter" class="counter">去往Vuex示例页面</a>
    {{/if}}
  </div>
</template>

<script>
import card from '@/components/card'{{#if_eq lintConfig "airbnb"}};{{/if_eq}}

export default {
  mpType: 'page',

  data{{#unless_eq lintConfig "airbnb"}} {{/unless_eq}}() {
    return {
      motto: 'Hello World',
      userInfo: {
        nickName: 'mpvue',
        avatarUrl: 'http://mpvue.com/assets/logo.png'{{#if_eq lintConfig "airbnb"}},{{/if_eq}}
      }{{#if_eq lintConfig "airbnb"}},{{/if_eq}}
    }{{#if_eq lintConfig "airbnb"}};{{/if_eq}}
  },

  components: {
    card{{#if_eq lintConfig "airbnb"}},{{/if_eq}}
  },

  methods: {
    bindViewTap{{#unless_eq lintConfig "airbnb"}} {{/unless_eq}}() {
      const url = '/packageA/logs'{{#if_eq lintConfig "airbnb"}};{{/if_eq}}
      {{#if router}}
      this.$router.push(url){{#if_eq lintConfig "airbnb"}};{{/if_eq}}
      {{/if}}
      {{#if_eq router false}}
      mpvue.navigateTo({ url }){{#if_eq lintConfig "airbnb"}};{{/if_eq}}
      {{/if_eq}}
    },
    clickHandle{{#unless_eq lintConfig "airbnb"}} {{/unless_eq}}(msg, ev) {
      {{#lint}}
      // eslint-disable-next-line
      {{/lint}}
      console.log('clickHandle:', msg, ev){{#if_eq lintConfig "airbnb"}};{{/if_eq}}
    }{{#if_eq lintConfig "airbnb"}},{{/if_eq}}
  },

  created{{#unless_eq lintConfig "airbnb"}} {{/unless_eq}}() {

  }{{#if_eq lintConfig "airbnb"}},{{/if_eq}}
}{{#if_eq lintConfig "airbnb"}};{{/if_eq}}
</script>

<style scoped>
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

{{#if_eq vant false}}
.usermotto {
  margin-top: 150px;
}
{{/if_eq}}

.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}

{{#if vuex}}
.counter {
  display: inline-block;
  margin: 10px auto;
  padding: 5px 10px;
  color: blue;
  border: 1px solid blue;
}
{{/if}}
</style>
