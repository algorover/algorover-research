# AlgoRover Research

AlgoRover Research 0.1.2 可搜索已发布的策略，并通过正式云端服务运行历史回测和下载报告。

[下载插件 ZIP](algorover-research-cloud-0.1.2.zip)

在终端依次安装并授权插件。

```bash
codex plugin marketplace add algorover/algorover-research
codex plugin add algorover-research-cloud@algorover-research-github
codex mcp login algorover-research --oauth-client-registration dcr --scopes research:read,research:run
```

最后一条命令会打开浏览器授权页。使用 AlgoRover 账号登录，确认读取研究结果和运行历史回测的权限，点击「允许授权」。终端提示授权成功后，在 Codex 新建一个对话，例如输入「使用 AlgoRover Research 搜索 EMA 回调策略」。

如果已经安装插件，但遇到 `OAuth authorization required`，执行上面的授权命令，再新建对话。
