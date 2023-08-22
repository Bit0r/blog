# 引入

vscode有个remote功能，但是官方文档地方写的不是很清楚，这里介绍一些小技巧。

# 技巧

## 环境变量未生效

因为vscode的remote server存在缓存，所以如果你在server上设置了新环境变量，但是在vscode中却发现环境变量未生效，可以尝试重启vscode server。

在vscode中，按下`F1`，输入`Remote-SSH: Kill VS Code Server on Host...`，选择你的server，然后重启vscode。

如果上面的方法不行，可以尝试在server上执行`pkill node`，然后重启vscode。

# 参考

- [stackoverflow 全局环境变量](https://stackoverflow.com/questions/66353196/set-global-environment-variables-in-vs-code-with-remote-ssh)
