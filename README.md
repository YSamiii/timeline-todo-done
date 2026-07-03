# Timeline Plan / Done PWA v12 — iPhone / iPad 可安装版

这是一个可以安装到 iPhone / iPad 主屏幕的 PWA 版本。它不是 App Store 原生 IPA；不需要 Mac 或 Apple Developer 账号。部署到 HTTPS 网址后，用 Safari 打开并选择“添加到主屏幕”即可像普通 app 一样从主屏幕启动。

## v12 新增

- 新增计划任务的类别默认改为“工作”。
- Direct Done 的类别默认改为“工作”。
- 新增计划或 Direct Done 后，类别会回到“工作”，不会继续沿用上一次选择。
- Service Worker 缓存更新为 v12。
- v11 数据会自动迁移到 v12。

## 核心功能保留

- 一天一个时间轴，通过日期切换查看不同日期。
- 左侧保留 Plan / To-do time block。
- 右侧生成 Actual / Done / Partial / Direct Done time block。
- Direct Done 支持手动选择开始/结束时间并自动计算持续时间。
- Direct Done 支持计时器。
- 计划任务支持计时器、暂停、继续、今天继续、记录完成。
- “今天继续”会在右侧生成本次 Partial time block，但左侧任务仍保留为继续中。
- Actual blocks 按实际开始时间排序。
- Actual 早/晚统计使用计划结束时间对比实际完成时间。
- Firebase 同步结构保留：同一账号可在手机、iPad、电脑同步。

## 文件

- `index.html`：主程序
- `manifest.json`：PWA 安装配置
- `sw.js`：离线缓存 Service Worker
- `icons/`：PWA / iOS 主屏幕图标
- `firestore.rules`：Firestore 安全规则示例

## 先本地测试

不要用 `file://` 直接测试 PWA。请在文件夹中运行：

```bash
cd timeline-plan-done-pwa-v12
python3 -m http.server 8080
```

然后打开：

```text
http://localhost:8080
```

## 部署到手机可访问的网址

把整个 `timeline-plan-done-pwa-v12` 文件夹部署到任一 HTTPS 静态托管，例如：

- Firebase Hosting
- Netlify
- Vercel
- Cloudflare Pages
- GitHub Pages

部署后得到一个 `https://...` 网址。

## 安装到 iPhone / iPad

1. 在 iPhone / iPad 上用 Safari 打开部署后的 HTTPS 网址。
2. 点击 Safari 的分享按钮。
3. 选择“添加到主屏幕”。
4. 名称保留为 `Plan Done` 或自行修改。
5. 点击“添加”。
6. 之后从主屏幕图标打开即可。

## Firebase 同步设置

1. 打开 Firebase Console，创建项目。
2. 添加 Web App，复制 Firebase config。
3. 开启 Authentication > Sign-in method > Email/Password。
4. 创建 Firestore Database。
5. 发布 `firestore.rules` 中的安全规则。
6. 部署本文件夹到 HTTPS 静态托管。
7. 打开 app，点“同步设置”，粘贴 Firebase config，保存。
8. 用邮箱注册/登录。另一台设备打开同一个网址并登录同一个账号即可同步。

## Firestore 数据位置

```text
users/{uid}/data/main
```

## 说明

PWA 可以安装到主屏幕并独立窗口运行，但它仍是 Web App。若需要发布到 App Store 的原生 iOS App，需要 Apple Developer 账号、签名证书、Xcode/云打包流程，以及 App Store 审核。
