## 1.smartODN 代码仓库:

- [WebPortal-VUE](http://sd-dev-git.huawei.com/SmartODN/WebPortal-VUE)
- [webPortal-admin](http://sd-dev-git.huawei.com/SmartODN/webPortal-admin)
- [smartodn-web-db-scripts](http://sd-dev-git.huawei.com/SmartODN/smartodn-web-db-scripts)

## 2.jenkins 项目构建：

[前端构建](http://10.68.50.129:8080/view/smartodn_web/job/smartodn_web_ci/view/webportal_vue/)

## 3.国际化

> 1.首先要从 dev 后台添加国际化 [后台国际化地址](http://sd-smartodn-dev.huawei.com:38000/#/system/language)

> 2.然后要在代码中使用刚才加入的 key，如下显示 public.yes,public.no 都属于 key

```
  <el-radio-group v-model="usePon">
    <el-radio :label="true">{{$t('public.yes')}}</el-radio>
    <el-radio :label="false">{{$t('public.no')}}</el-radio>
  </el-radio-group>
```

> 3.加完之后，就会根据语言进行正常切换，但这些都是发生在 Dev 环境

> 4.如果项目要上 sit 等其他环境，还要刷国际化脚本，具体步骤：

1. clone 仓库[smartodn-web-db-scripts](http://sd-dev-git.huawei.com/SmartODN/smartodn-web-db-scripts)到本地 , (其中，language/init_data.sql) 就是国际化数据库脚本
2. 导出 dev 环境数据库（odn_language）表 (t_local_value)中的数据到本地，命名 xxx.sql
3. 然后用本地的数据 xxx.sql 替换 smartodn-web-db-scripts/language/init_data.sql
4. 替换完成之后，就可以 push 到远程仓库，等待发布
5. 如果要发到 sit 等其他环境，就可以告诉运维刷新脚本

## 4.bug 管理

1. 首先登陆[网址](http://sd-smartmgr.huawei.com/zentao/index.php?m=bug&f=browse),用户名：域账号；密码：123456
2. 如果登录不进去，请联系美华总，帮你开通

## 5.项目功能介绍

```
- src 业务代码
-- api 调用后台接口业务
-- assets 存放项目中的图片字体等
-- common 项目中一些公共函数
-- components 项目中的公共组件
-- directive 项目中用到的指令
-- mixin 项目中的混合，用于拆分组件，进行代码复用
-- router 项目中的路由
-- views 项目中的视图部分
-- vues  状态管理
```
