## 1.多语言来自于后端，要保证多语言全部加载完成，才能动态改变语言种类

```
...
const appBody = window.top == window.self
data () {
    return {
      appBody: appBody,
      hasLoaded: false
    }
  },
  computed: {},
  created () {
    // not embed
    if (this.appBody) {
      this.initI18n()
    } else {
      // embed
      this.hasLoaded = true
    }
  },
  methods: {
    initI18n () {
      let v = 'en-US' // 默认值
      if (util.getStore('languageToken')) {
        v = util.getStore('languageToken')
      } else {
        util.setStore('languageToken', v)
      }
      this.$store.dispatch('setLanguage', v).then(param => {
        let languages = JSON.parse(util.getStore('language'))
        v = v.split('-')[0]
        this.$i18n.mergeLocaleMessage(v, languages)
        this.$i18n.locale = v
        this.hasLoaded = true
      })
    }
  },
  ...
```

> 1.hasLoaded 一是保证多语言加载完毕才放开路由出口；二是如果被嵌套了，也要放开(第三方应用要导到目标页面)
