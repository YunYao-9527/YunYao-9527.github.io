# 王登政的项目作品集

展示五个项目的实现、验证依据和运行入口。项目介绍页部署在 GitHub Pages，Python 应用独立部署。

## 在线系统

- [AgentOps 评测与 Trace](https://yunyao-agentops.onrender.com/evaluations)
- [事务型客服业务工作台](https://yunyao-customer-service.onrender.com/)
- [气象证据工作台](https://yunyao-weather.onrender.com/)
- [CAD 真实轻量检索](https://yunyao-cad-visual.onrender.com/)

以上四个服务已在新加坡区域以 Free 创建，并通过公网健康与业务流程检查。AR 项目仍为技术档案，不提供虚构的运行入口。

## 免费应用部署

仓库的 `render.yaml` 可以在 Render 中作为 Blueprint 导入，四个服务均明确使用 `plan: free`：

| 服务 | 内容 | 健康检查 |
| --- | --- | --- |
| AgentOps | 仪表盘、数据集、规则评测、Trace 与结果存储 | `/health` |
| 客服 Agent | 订单工具、退款确认与补偿、可选模型对话 | `/health` |
| 气象多智能体 | 真实观测适配器、证据融合与预测 | `/api/v1/health` |
| CAD 轻量检索 | 真实图片密度与边缘特征检索，非 CLIP | `/health` |

导入入口：<https://dashboard.render.com/select-repo?type=blueprint>。选择此仓库并保留 Free 方案，不创建收费数据库或磁盘。服务真正启动并通过健康检查后，才将其实际 URL 接入项目页。

免费服务可能休眠，首次请求需要等待；本地 SQLite、上传图片等临时文件可能在休眠、重启或重新部署后丢失。此配置用于作品演示，不用于存放唯一的数据副本。模型 API 费用不属于免费托管。当前线上实例已通过 Render 服务端环境变量接入 DeepSeek，Blueprint 与公开代码不包含密钥。

客服、AgentOps、气象分别限制为每实例每日 40、20、20 次模型调用；还限制输入长度、单次输出和模型评测批次。计数按 UTC 日计算，休眠、重启或部署后可能重置，因此是应用防滥用措施，不是供应商账单的硬性金额上限。

CAD 完整 CLIP 服务保留在原仓库 `Dockerfile.full`，需要另行准备训练权重及运行资源。公开轻量服务不会冒充完整模型。AR 仓库缺少原应用源码，仅展示真实技术路线与贡献说明。

## 验证记录

2026-10-22：气象 45 项、AgentOps 16 项、客服 36 项、CAD 轻量检索 3 项测试通过，共 100 项。五个界面的桌面与 390px 手机视口均通过基础验收；公网 API 已验证评测评分及 Trace 落库、订单查询和确认拦截、气象预测与审计、图纸稳定检索及公开管理边界。DeepSeek 实际调用已验证：客服模型到订单工具闭环、AgentOps 模型任务得分 1.0、气象结构化影子证据卡。

网站设计参考 Anthropic 官方 `frontend-design` 技能；保持响应式布局、键盘焦点和真实运行状态标注。
