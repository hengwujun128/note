## 1.how to use axios to download file?

``ex
dfa
fun
(){
  
 }
// export kmz
exportKMZ(gridId) {
return axios({
url: `${base.projectInstance}fileload/kmz/${gridId}`,
method: 'GET',
// responseType: 'blob',
responseType: 'arraybuffer',
})
},

```

```

//kmz
kmzExport() {
if (this.$parent.gridHaveData) {
// window.open(this.downLoadUrl.kmz);
program.exportKMZ(this.$parent.gridId).then(response => {
// if (response.code == 1) {
const url = window.URL.createObjectURL(new Blob([response]));
const link = document.createElement("a");
link.href = url;
link.setAttribute("download", "file.kmz"); //or any other extension
document.body.appendChild(link);
link.click();
// }
});
} else {
this.$message.error(this.$t("program.pleaseImport"));
return;
}
},

```
## 2.but this method is not working on IE11?

> 1.判断是否为 IE

[reference](https://my.oschina.net/u/195725/blog/1605565)
```

if (navigator.msSaveOrOpenBlob) {
navigator.msSaveOrOpenBlob(blob, fileName + "-kmz.zip"); // IE10-11
} else {
link.click();
}

```
完整代码如下:
```

program
.exportKMZ(item.id)
.then(response => {
const blob = new Blob([response], { type: "application/json" });
const url = window.URL.createObjectURL(blob);
const link = document.createElement("a");
let fileName = item.name;
link.href = url;
link.download = fileName + "-kmz.zip";
// link.setAttribute("download", fileName + "-kmz.zip"); //or any other extension
document.body.appendChild(link);
if (navigator.msSaveOrOpenBlob) {
navigator.msSaveOrOpenBlob(blob, fileName + "-kmz.zip"); // IE10-11
} else {
link.click();
}
// link.click();
loading.close();
})
.catch(error => {
console.log(error);
});
} else {
this.$message({
type: "warning",
message: this.$t("program.pleaseImport")
});
return;
}

```

```
