# ZAP-Hosting VPS 自动续期脚本

自动登录 ZAP-Hosting 并访问 VPS 详情页，保持 Lifetime VPS 活跃。

## ⚠️ 免责声明

本项目仅供学习网页自动化技术使用。使用本脚本可能违反相关网站的服务条款，包括但不限于：
- 禁止使用自动化工具访问
- 禁止绕过安全验证措施（如 reCAPTCHA）

**使用本项目的风险由用户自行承担**，包括但不限于账号被封禁、服务被终止等后果。请在使用前仔细阅读相关网站的服务条款。

## 功能

- 支持多账号
- 自动登录
- 自动处理 Cloudflare 验证
- 自动解决 reCAPTCHA (YesCaptcha)
- 访问 VPS 详情页保活
- 会话持久化
- Telegram 通知

## 安装

```bash
# 安装系统依赖
sudo apt install -y xvfb  # Debian/Ubuntu

# 安装 uv
curl -LsSf https://astral.sh/uv/install.sh | sh

# 克隆项目
git clone https://github.com/donma033x/zap-renew.git
cd zap-renew

# 安装项目依赖
uv sync

# 安装 Playwright 浏览器
uv run playwright install chromium
```

## 配置

```bash
cp .env.example .env
nano .env
```

配置说明：
- `YESCAPTCHA_API_KEY`: YesCaptcha API Key (必需，用于解决 reCAPTCHA)
- `ACCOUNTS`: 账号配置，格式 `邮箱:密码`，多账号用逗号分隔
- `STAY_DURATION`: VPS 详情页停留时间 (秒)
- `TELEGRAM_BOT_TOKEN`: Telegram Bot Token (可选)
- `TELEGRAM_CHAT_ID`: Telegram Chat ID (可选)

## 运行

```bash
cd zap-renew
xvfb-run uv run python zap-renew.py
```

## 定时任务

建议每月运行一次即可保持 VPS 活跃。

```bash
# 使用 crontab
crontab -e

# 每月 1 号上午 10 点运行
0 10 1 * * cd /path/to/zap-renew && xvfb-run ~/.local/bin/uv run python zap-renew.py >> /tmp/zap-renew.log 2>&1
```

## 费用说明

本项目使用 YesCaptcha 解决 reCAPTCHA 验证码：
- 每次登录消耗约 **15 points**
- 充值 10 元可获得 **1000+ points**
- 每月运行一次，理论上可用 **5 年以上**

## 文件说明

- `zap-renew.py` - 主脚本
- `pyproject.toml` - 项目配置和依赖
- `.env.example` - 配置文件示例
- `sessions/` - 会话保存目录

## 许可证

MIT
