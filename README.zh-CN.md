# AlgoRover Research

[English](README.md) | 简体中文

AlgoRover Research 帮助你在对话中查找已发布的交易策略，使用公开市场数据运行历史回测，并查看成交记录和研究报告。回测在 AlgoRover Research 云端服务中执行。

本仓库提供 0.1.2 版本的 Codex 插件及安装包。插件连接 `https://research.algorover.ai/mcp`，无需在本机安装 Python、Docker、AlgoRover 主程序或本地 Runtime。

[下载插件 ZIP](algorover-research-cloud-0.1.2.zip)

## 功能

- 搜索策略，查看发布版本、策略包许可证和可运行的预设。
- 按策略支持的市场和预设准备回测，选择 90 天或 365 天的历史窗口，并在启动前查看配置。
- 运行回测，查看任务进度，取消尚未完成的任务。
- 查看自己的回测指标、成交明细和历史任务，下载研究报告；按需获取已发布策略包的下载链接。
- 按用户请求删除指定回测结果或全部 Research 数据。删除操作需要单独授权。

可用的策略、市场和预设以服务返回的内容为准。需要解析预设的策略会先进入准备流程；准备失败时，插件会显示服务返回的原因。

## 安装与登录

在支持插件的 Codex 客户端中使用。通过终端安装时，依次执行：

```bash
codex plugin marketplace add algorover/algorover-research
codex plugin add algorover-research-cloud@algorover-research-github
codex mcp login algorover-research --oauth-client-registration dcr --scopes research:read,research:run
```

最后一条命令会打开浏览器授权页。使用 AlgoRover 账号登录，核对申请的权限后点击「允许授权」。

在 Codex 里选择 `@AlgoRover Research`，说「我想开始用 AlgoRover Research」。聊天里会打开可操作的策略目录卡片。在卡片中选择策略，即可查看详情并准备回测。如果当前对话无法使用 Research 工具，新建对话后再选一次插件。

已从本仓库安装过插件的用户，可以刷新插件市场并重新安装。

```bash
codex plugin marketplace upgrade algorover-research-github
codex plugin add algorover-research-cloud@algorover-research-github
```

搜索策略和准备回测配置可以公开访问。启动回测、查看个人任务和下载个人报告需要登录。上述命令申请的权限为：

| 权限 | 用途 |
| --- | --- |
| `research:read` | 读取当前账号的研究任务、结果和报告。 |
| `research:run` | 启动和取消当前账号的回测任务。 |

删除数据需要额外的 `research:delete` 权限，上面的登录命令没有申请此权限。需要使用删除功能时，请通过客户端重新授权并包含该权限，或前往 [Research 网页](https://research.algorover.ai/)管理自己的数据。

登录和授权均在浏览器中完成。请勿在对话中提供密码、访问令牌或交易所 API 密钥。

## 使用示例

- 「使用 AlgoRover Research 搜索 EMA 回调策略，查看可运行的预设。」
- 「选择一个可用的 ETH 预设，准备最近 90 天的回测，先给我看配置。」
- 「按刚才的配置启动回测，并查看任务进度。」
- 「查看我最近一次成功回测的指标和成交记录，给我报告下载链接。」
- 「取消我刚才启动的回测。」

## 数据与权限

插件将执行任务所需的策略引用、市场、预设和回测时间范围发送到 AlgoRover Research 服务。登录后的任务和研究结果归当前账号所有，更换对话后仍可查询。插件按账号权限访问个人数据。

你可以请求删除指定回测结果，或明确请求删除全部 Research 数据。删除全部 Research 数据与删除登录所用的身份账号是两个操作。数据收集、使用和保留规则见[隐私政策](https://www.algorover.ai/privacy/)。

AlgoRover Research 仅支持历史研究，不连接交易所账户，也不执行交易订单。历史回测结果不能证明未来收益。

## 连接问题

出现 `OAuth authorization required` 时，重新执行上面的登录命令，完成浏览器授权后新建对话。

服务连接失败时，请检查网络及客户端的 MCP 连接状态。联系支持时提供错误信息和请求编号，避免附上密码或令牌。

## 发布方与支持

发布方：Rivendell Holdings Investment Limited。

- [AlgoRover 官网](https://www.algorover.ai/)
- [帮助与支持](https://www.algorover.ai/en/help/)
- [隐私政策](https://www.algorover.ai/privacy/)
- [服务条款](https://www.algorover.ai/terms/)
