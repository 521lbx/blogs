### shell命令学习

1. 删除文件夹
rm -r node-modules

2. Bash

  |命令|说明|
  |:----|:----|
  | && | 顺序执行多条命令，当碰到执行出错的命令后将不执行后面的命令 |
  | & | 并行执行多条命令 |
  | || | 顺序执行多条命令，当碰到执行正确的命令后将不执行后面的命令 |
  | | | 管道符 |

3. echo: 用于字符串的输出, echo '' > config.js新建空文件

4. >: 输出重定向

```
// 向docs/index.md文件输出字符串# Hello VitePress，并且是覆盖输出
echo '# Hello VitePress' > docs/index.md
// 向docs/index.md文件输出字符串# Hello VitePress，并且是追加输出
echo '# Hello VitePress' >> docs/index.md

```

5. "mkdir && echo '# Hello VitePress' > docs/index.md"换成"mkdir docs ; echo '# Hello VitePress' > docs/index.md",新建docs/index.md并输出# Hello VitePress