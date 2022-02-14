### npm发布包到私服

- 通过设置package.json将包发布到本地仓库

```
"publishConfig" : {
    "registry" : "http://localhost:8081/repository/npm-hosted/"
}
```

- 通过命令行将包发布到本地仓库

```
npm publish --registry=http://localhost:8081/repository/npm-hosted/
```

- 通过设置.npmrc文件，发布包时免登录

```
// 设置npm源
registry=http://test.radonline.cn:8010/repository/npm-group/
email=admin@example.org
always-auth=true
// _auth='用户名:密码(base64编码)'
_auth="YWRtaW46aG1nc29mdA=="
```


