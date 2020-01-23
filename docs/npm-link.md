## Use Cases

主仓库一个 repo，比如`~/src/main`，依赖的包一个或者多个 repo`~/src/package`。当你在开发依赖包时，可能会使用到主 app 来进行 E2E 测试，测试成功后才去发布。
如果没有`npm link`，你可以有两种方式来进行测试

- 在依赖包的仓库中完成代码，打包，然后把打出的包手动拷贝到主 repo 的`node_modules`目录中，完成测试
- 每次修改完依赖包，都发布，然后再主仓库中使用包管理工具更新。

这两种方法，要么太过麻烦，要么会产生很多无用的中间版本。

## How to use `npm link`

- 在子仓库下运行`npm link`。本质上他的作用就是在全局的`node_modules`目录（默认是`/usr/local/lib/node_modules`）下建立一个当前仓库的软连接（Symbol link）。
- 然后再主仓库下运行`npm link <packageName>`（`packageName`就是 package.json 文件中的`name`属性对应的值）。这样在主仓库中使用对应包(`import ... from <packageName>`)的时候就会通过软连接从子仓库中拉取文件。

## How to recover

- 当你的依赖包测试完毕，发布以后，主仓库应该使用真正的发布包，而非软连接对应的本地宝。首先，切断主仓库中的`node_modules/packageName`下的软连接

```sh
cd ~/src/main
npm uninstall --no-save <packageName> && npm install # 删除node_modules下的包（软连接），重新安装（从远端拉真实的包）
```

- 当然你也可能想要清除全局`node_modules`下的软连接（上一步之后，这里即使不清除也不会对主仓库有什么影响了）

```sh
cd ~/src/package
npm uninstall
```

## Refs

- [Understanding npm-link](https://medium.com/dailyjs/how-to-use-npm-link-7375b6219557)
- [npm docs](https://docs.npmjs.com/cli/link.html)
