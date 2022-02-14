### 设置responseType为blob后台返回json的处理

```
// response类型为blob实际返回为json的处理
  handlerResponseError (data) {
    const fileReader = new FileReader();
    fileReader.onload = () => {
      try {
        const jsonData = JSON.parse(fileReader.result); // 说明是普通对象数据，后台转换失败
        console.log('后台返回的信息', jsonData);
        if (jsonData.subMsg) {
          this.$message({
            showClose: true,
            message: jsonData.subMsg,
            type: 'error'
          });
        }
      } catch (err) { // 解析成对象失败，说明是正常的文件流
        console.log('success...');
      }
    };
    fileReader.readAsText(data);
  },
  printReport (printRes) { // 报告打印
    if (printRes && printRes.type === 'application/json') { // 返回的是json
      this.handlerResponseError(printRes);
      return false;
    }
    // 将后台返回的流文件先下载
    // 触发下载
    let blob = new Blob([printRes], { type: 'application/octet-stream' });
    let objectUrl = window.URL.createObjectURL(blob);
    var link = document.createElement('a');
    link.href = objectUrl;
    link.click();
    window.URL.revokeObjectURL(link.href);
    if (windowApp) { // 如在客户端中下载完成后执行打印操作
      // 开始下载
      if (window.downloadNotify) {
        window.downloadNotify = null;
      }
      window.downloadNotify = function (downloadInfo) {
        downloadInfo = JSON.parse(downloadInfo);
        console.log('下载信息', downloadInfo);
        if (downloadInfo.status === '1') { // 下载完毕
          // 调用客户端打印
          // windowApp.printXPSFile(downloadInfo.filename);
          console.log(3333, downloadInfo.filename);
          windowApp.printPDF(downloadInfo.filename);
        }
      };
    }
  },
```

