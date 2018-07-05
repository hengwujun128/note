> 1.  el-date-picker is not rendering in IE11

```
  <el-form-item :label="$t('license.cutOffDate')" prop="cutOffDate">
    <el-date-picker style="width:202px" :editable="false" v-model="formData.cutOffDate" type="date" :placeholder="$t('public.chooseData')"      format="yyyy-MM-dd" value-format="yyyy-MM-dd" :picker-options="pickerOptions">
    </el-date-picker>
  </el-form-item>
```

**solve method**

remove placeholder

```
<el-form-item :label="$t('license.cutOffDate')" prop="cutOffDate">
    <el-date-picker style="width:202px" :editable="false" v-model="formData.cutOffDate" type="date"      format="yyyy-MM-dd" value-format="yyyy-MM-dd" :picker-options="pickerOptions">
    </el-date-picker>
  </el-form-item>
```

> 2.  IE11 会缓存 get 请求数据
>     具体表现：login 页面跳转到 w3 sso 登录，重定向回来之后，又跳转到 login 页面；打卡控制台可以跳转到首页

```
原因: 在根路由对应的index.vue 中 路由守卫中，获取用户信息（getUserInfo）,在获取项目列表，都是get请求；
sso回来之后，IE11没有发起这些请求，导致调用其他后续接口会返回401，从而跳转到登录页
```

index.vue 代码如下

```
  beforeRouteEnter(to, from, next) {
    async function init(params) {
      try {
        // 用户信息
        let { msg, code, result } = await user.getUserInfo();
        if (code != "1") {
          next({ path: "/login" });
          return;
        } else {
          store.commit("UPDATE_USER", result.userInfo);
        }
        // 项目列表

...
```

how to solve the problem
**remove cache control**

Cache-Control = "no-cache";
Pragma = "no-cache"

```
axios.interceptors.request.use(config => {
  // let projectcode = JSON.parse(util.getStore("userInfo")) ? JSON.parse(util.getStore("userInfo"))["lastAccessProjectCode"] : "00000000";
  let projectcode = sessionStorage.getItem("projectCode") ? sessionStorage.getItem("projectCode") : ''
  let lang = util.getStore("languageToken");
  // filter
  if (config.url.includes("/project/mylist")) {
    // config.headers['projectcode'] = '';
  } else {
    config.headers["projectcode"] = projectcode;
  }
  config.headers["language"] = lang;
  config.headers["Cache-Control"] = 'no-cache';
  config.headers['Pragma'] = 'no-cache';
  // language
  return config;
});
```

当然：还可以为每个请求加上时间戳:new Date().getTime()
