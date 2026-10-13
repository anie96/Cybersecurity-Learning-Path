# ELK SSH 暴力破解检测与告警平台
## 📌 项目简介
模拟企业安全运营场景，自主搭建日志分析与检测平台，实现对 SSH 暴力破解攻击的实时监控与告警。

## 🧱 技术架构
`/var/log/auth.log` → Filebeat → Logstash (Grok 解析) → Elasticsearch → Kibana (阈值告警)

## 🔧 核心工作
1. **环境部署**：使用 Docker Compose 部署 Elasticsearch、Logstash、Kibana。
2. **日志采集与解析**：配置 Filebeat 采集 Linux 认证日志，编写 Logstash Grok 正则，解析出 `ssh_ip`、`ssh_action`、`ssh_user` 等字段。
3. **攻击模拟**：使用 Hydra 对本地 SSH 服务发起暴力破解攻击。
4. **告警配置**：在 Kibana 中配置索引阈值规则，实现“5分钟内失败登录超过5次自动触发告警”。

## ⚠️ 踩坑记录
- **Kali 默认无 auth.log**：通过安装并启动 `rsyslog` 解决。
- **Grok 正则不匹配新版日志**：调整正则后成功解析。
- **Kibana 7.17 告警限制**：该版本阈值规则不支持字段分组，先用全局阈值跑通流程。
