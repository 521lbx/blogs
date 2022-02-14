### 处理iframe内存泄漏

```
let iframe = el.contentWindow;
if (el) {
  el.src = 'about:blank';
  try{
    iframe.document.write('');
    iframe.document.clear('');
    iframe.close('');
  }catch(e) {}
  const p = el.parentNode;
  if (p) {
    p.removeChild(el);
  }
  try{
    window.CollectGarbage();
  }catch() {}
  el = null;
}
```

