### 流文件预览pdf

```
// 需在请求中设置{responseType: 'blob'}
let resPreview = await reportpreview({
  snapshotPath: '',
  pdfParam
});
if (resPreview) { // 预览
  let blob = new Blob([resPreview], { type: 'application/pdf' });
  let objecturl = window.URL.createObjectURL(blob);
  this.iframeSrc = objecturl;
  this.showIframe = true;
}
```

