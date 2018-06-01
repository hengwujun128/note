## 1.how to use axios to download file?

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
