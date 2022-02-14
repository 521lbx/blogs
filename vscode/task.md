### task

vscode可以自定义task完成一些代码或者项目生成，编译，测试，打包等的工作。通过这种方式完成代码生产自动化，可以在做这些事情时不用临时再敲命令，或者写代码。

1. 创建task任务

Terminal->Configure Tasks-> 随便点击一个就会生成 .vscode/tasks.json 文件

2. 修改tasks.json，创建监听typescript的task监听

```
{
	"version": "2.0.0",
	"tasks": [
    {
      "type": "typescript",
      "tsconfig": "tsconfig.json",
      "option": "watch",
      "problemMatcher": [
        "$tsc-watch"
      ],
      "group": {
        "kind": "build",
        "isDefault": true
      },
      "label": "tsc: watch - tsconfig.json"
    }
  ]
}
```

3. ctrl + shift + B启动任务