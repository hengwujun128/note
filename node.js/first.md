> 1. vue 不是系统命令

```
 npm install --global vue-cli
 vue init mpvue/mpvue-quickstart my-project  // error
 // 提示vue不是系统命令
```

解决方案：
[参考方案](https://segmentfault.com/a/1190000005602881)

```
npm config set prefix "path/node_global"
npm config set cache "path/node_cache"


以上方法就可以，如果还是提示，则找到xxx/node_global/vue.cmd命令，设置环境变量
```
