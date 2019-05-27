<script>
export default {
  {{#vant}}
  globalConfig: {
    usingComponents: {
      'van-tag': 'vant-weapp/dist/tag/index'{{#if_eq lintConfig "airbnb"}},{{/if_eq}}
    }{{#if_eq lintConfig "airbnb"}},{{/if_eq}}
  },
  {{/vant}}
  created{{#unless_eq lintConfig "airbnb"}} {{/unless_eq}}() {
    // 调用API从本地缓存中获取数据
    /*
     * 平台 api 差异的处理方式:  api 方法统一挂载到 mpvue 名称空间, 平台判断通过 mpvuePlatform 特征字符串
     * 微信：mpvue === wx, mpvuePlatform === 'wx'
     * 头条：mpvue === tt, mpvuePlatform === 'tt'
     * 百度：mpvue === swan, mpvuePlatform === 'swan'
     * 支付宝(蚂蚁)：mpvue === my, mpvuePlatform === 'my'
     */
    let logs{{#if_eq lintConfig "airbnb"}};{{/if_eq}}
    if (mpvuePlatform === 'my') {
      logs = mpvue.getStorageSync({key: 'logs'}).data || []{{#if_eq lintConfig "airbnb"}};{{/if_eq}}
      logs.unshift(Date.now()){{#if_eq lintConfig "airbnb"}};{{/if_eq}}
      mpvue.setStorageSync({
        key: 'logs',
        data: logs
      }){{#if_eq lintConfig "airbnb"}};{{/if_eq}}
    } else {
      logs = mpvue.getStorageSync('logs') || []{{#if_eq lintConfig "airbnb"}};{{/if_eq}}
      logs.unshift(Date.now()){{#if_eq lintConfig "airbnb"}};{{/if_eq}}
      mpvue.setStorageSync('logs', logs){{#if_eq lintConfig "airbnb"}};{{/if_eq}}
    }
    {{#lint}}
    // eslint-disable-next-line
    {{/lint}}
    console.log('app created and cache logs by setStorageSync'){{#if_eq lintConfig "airbnb"}};{{/if_eq}}
  },
  log{{#unless_eq lintConfig "airbnb"}} {{/unless_eq}}() {
    console.log(`log at:${Date.now()}`){{#if_eq lintConfig "airbnb"}};{{/if_eq}}
  }
}{{#if_eq lintConfig "airbnb"}};{{/if_eq}}
</script>

<style>
.container {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  padding: 200rpx 0;
  box-sizing: border-box;
}
/* this rule will be remove */
* {
  transition: width 2s;
  -moz-transition: width 2s;
  -webkit-transition: width 2s;
  -o-transition: width 2s;
}
</style>
