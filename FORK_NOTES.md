# 当前镜像 Action 副本

[上游文档](./README.md) · [实际输入定义](./action.yml)

此仓库保留 Yikun/hub-mirror-action 的实现与署名。工作流写 `uses: Yikun/hub-mirror-action@master` 时使用的是上游，不是本副本；不要仅修改了本仓库就假定所有引用端已经使用新内容。

## 需要准确理解的参数

| 参数 | action.yml 当前值或行为 | 注意事项 |
| --- | --- | --- |
| force_update | 默认 false | 启用会使用强制推送，可能覆盖目标端独立提交 |
| debug | 默认 false | 详细命令日志需要额外检查敏感信息 |
| cache_path | `/github/workspace/hub-mirror-cache` | 原 README 参数段写空值；实际执行以 action.yml 为准 |
| timeout | 30m | 每个 Git 命令的超时，不是整项同步时限 |
| api_timeout | 60 秒 | API 请求超时，与 Git 超时分开 |
| mappings | 默认空 | 单次映射，不是传递式重命名规则 |
| lfs | 默认 false | 开启会产生额外的大文件获取与推送 |

## 同步前检查

明确源、目标、仓库白名单、名称映射和目标端现有提交。首先在自己的临时仓库验证，不将全部组织或个人仓库作为首次测试范围。不要为解决分支分歧自动开启 force_update。

目标密钥与创建仓库的 token 只放在受保护 Secret 中，权限与仓库范围尽量收窄。不能因一个工作流能读取源码就认为它有权向任意目标推送。

重命名、归档或删除本仓库前，需检查其他工作流中是否仍有 `uses` 引用。最后推送时间不能证明这个 Action 没被使用。

本次读取 README 与 action.yml，仅补充使用说明；未修改默认参数、执行镜像、访问目标仓库、推送 LFS 或更改外部凭据。原上游文档与许可完整保留。
