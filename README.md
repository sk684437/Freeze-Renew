# 🎮 FreezeHost 自动续期

使用 Playwright + GitHub Actions 每天自动续期 FreezeHost 免费服务器。

## ⚙️ 配置步骤

### 1️⃣ Fork 或上传此仓库到 GitHub

### 2️⃣ 添加 Secrets

进入仓库 → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**：

| 🔑 Secret 名称 | 📝 格式 | ✅ 必填 |
|---|---|---|
| `DISCORD_TOKEN` | `Discord Token (多个用逗号 , 隔开)` | ✅ |
| `TG_BOT` | `chat_id,bot_token` | ✅ |
| `GOST_PROXY` | `socks5://host:port` | 可选 |

> **💡 如何获取 Discord Token？**
> 1. 在电脑浏览器中登录 [Discord 网页版](https://discord.com/app)。
> 2. 按 `F12` 打开开发者工具，切换到 **Network (网络)** 面板。
> 3. **关键步骤**：在 Network 面板的过滤选项卡中，选中 **"Fetch/XHR"**。
> 4. 保持面板打开，回到 Discord 页面并**随便点击左侧的其他服务器或频道**。
> 5. 这时 Network 列表会出现一些名为 `science`、`messages` 或 `typing` 的请求记录，随便点开其中一个。
> 6. 在右侧弹出的 **Headers (标头)** 标签页里向下滑，找到 **Request Headers (请求标头)** 区域。
> 7. 在里面寻找名叫 `Authorization` 的字段，它后面的那一串复杂字符就是您的 Token！直接复制下来即可。

### 3️⃣ 启用 Actions

进入 **Actions** 标签页，点击 **Enable GitHub Actions**。

### 4️⃣ 手动触发测试

**Actions** → **🎮 FreezeHost 自动续期** → **Run workflow**

## 🕐 运行时间

自动任务配置为 **每 3 天**（即 1, 4, 7... 号）的 **UTC 08:00**（北京时间 16:00）运行一次。
少于 7 天续期后，服务器时间会重置回 14 天。因此每 3 天检查一次（14 -> 11 -> 8 -> 5天触发续防）完美契合机制，且避免资源浪费。
可在 `.github/workflows/freeze.yml` 的 `cron` 表达式中修改。

## 📊 续期结果说明

| 状态 | 说明 |
|---|---|
| ✅ passed | 续期成功，TG 已推送通知 |
| ⚠️ skipped | 余额不足，待赚够金币后下次自动重试 |
| ❌ failed | 登录失败或脚本异常，查看 failure-screenshots |
