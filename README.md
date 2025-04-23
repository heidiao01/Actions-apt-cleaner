🔄 APT Auto Cleaner
GitHub License GitHub Stars GitHub Workflow Status

专为 VPS/嵌入式设备设计的自动化清理工具，安全清理 APT 缓存和旧内核，节省磁盘空间。

✨ 功能特性
自动清理：每日执行 apt autoremove + apt clean
安全防护：
保留当前内核及最新2个版本
磁盘空间 <5GB 时自动终止
支持自定义包排除列表
多模式运行：
--dry-run 模拟运行
本地定时任务 / GitHub Actions 远程执行
日志管理：
清理前后空间对比
结构化日志 (保留14天)
🚀 一键安装
bash <(curl -L -s https://raw.githubusercontent.com/jzckk/Actions-apt-cleaner/main/install.sh)
🛠️ 使用指南
基础命令
# 手动执行清理
sudo apt-cleaner

# 模拟运行（不实际操作）
sudo apt-cleaner --dry-run

# 查看实时日志
tail -f /var/log/apt-cleaner/clean-$(date +%Y%m%d).log

# 卸载
sudo apt-cleaner-uninstall
高级配置
排除软件包
编辑 /etc/apt-cleaner/exclude.list：

# 格式：每行一个包名
linux-image-generic
docker-ce
nginx
调整定时任务
修改 /etc/cron.d/apt-cleaner：

# 每天UTC时间3:30执行
30 3 * * * root /usr/local/bin/apt-cleaner
日志管理

# 手动轮转日志
sudo logrotate -vf /etc/logrotate.d/apt-cleaner
🔒 安全机制
防护类型	实现方式	触发条件
内核保护	保留当前内核 + 最新2个版本	自动执行
磁盘保护	剩余空间 <5GB 时终止	df 检测
权限验证	强制 root 权限运行	脚本启动时检查
📜 开源协议
MIT License - 允许自由使用/修改/分发，无需署名

🤝 参与贡献
问题报告
新建 Issue

代码提交

git clone https://github.com/jzckk/Actions-apt-cleaner.git
fork 仓库后提交 Pull Request
开发规范

# 运行测试
bash tests/integration_test.sh

# 代码检查
shellcheck scripts/*.sh
⭐ 如果这个项目有帮助，请给个 Star 支持开发！


### 配套文件结构
. ├── LICENSE ├── README.md ├── config │ ├── exclude.list │ └── logrotate.conf ├── scripts │ ├── clean.sh │── install.sh └── .github └── workflows └── clean.yml
