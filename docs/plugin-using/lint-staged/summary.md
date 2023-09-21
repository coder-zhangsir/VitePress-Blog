# Lint Staged
>这是一个可以防止垃圾代码存入仓库的repo,通常可以搭配Git钩子+Linters(代码格式化)实现很好的效果。

&nbsp;&nbsp;例如在`pre-commit`时调用`lint-staged` bin可执行文件，那么每当我们提交文件到暂存区之前就会出现类似下面执行步骤
```
$ git commit

✔ Preparing lint-staged...
❯ Running tasks for staged files...
  ❯ packages/frontend/.lintstagedrc.json — 1 file
    ↓ *.js — no files [SKIPPED]
    ❯ *.{json,md} — 1 file
      ⠹ prettier --write
  ↓ packages/backend/.lintstagedrc.json — 2 files
    ❯ *.js — 2 files
      ⠼ eslint --fix
    ↓ *.{json,md} — no files [SKIPPED]
◼ Applying modifications from tasks...
◼ Cleaning up temporary files...
```

## 如何安装和配置？
![Alt text](image.png)

### step2: 需要注册`git`钩子去运行`lint-staged`
推荐我们使用`husky`，那我们就用它，

>`Husky`提高了你的代码提交质量还有更多。
当您提交或推送时，您可以使用它来检查提交消息、运行测试、检查代码等。Husky 支持[所有客户端Git钩子](https://git-scm.com/docs/githooks)。

快速初始化`husky`
```shell
npx husky-init && npm install
```

::: details 它将做以下事情：
1. 添加`prepare`脚本到`package.json`，
>当首次拉取仓库到本地需要先执行`npm run prepare`来做预备工作
```
{
  "scripts": {
    "prepare": "husky install"
  },
}
```
2. 创建一个普通`pre-commit`钩子，你能编辑它（默认在你提交时会执行`npm test`）
3. 配置Git hooks路径

使用`husky add`去添加其他钩子，例如：
```shell
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit "$1"'
```
:::


因为我们要用`lint-staged`所以可以修改.husky/pre-commit文件为如下内容：
```shell{4}
#!/usr/bin/env sh
. "$(dirname "$0")/_/husky.sh"

npx lint-staged
```
亦或者只将`npm test`改为`npx lint-staged`


### step3: 安装linter --> `Prettier`
- 首先将`Prettier`安装到本地
```shell
npm install --save-dev --save-exact prettier
```

- 然后创建一个空的配置文件，让编译器和其他工具知道你正在使用`prettier`

::: warning
调用`node -e|--eval run-script`可以执行node环境下一些函数
:::

```shell
node --eval "fs.writeFileSync('.prettierrc','{}\n')"
```

- 下一步，创建一个`.prettierignore`文件让 `Prettier CLI` 和编译器知道哪些文件不需要格式化。这里有一个案例：
```
# prettier doesn't respect newlines between chained methods
# https://github.com/prettier/prettier/issues/7884
**/*.spec.js
**/*.spec.ts
**/dist
# https://github.com/prettier/prettier/issues/5246
**/*.html
```