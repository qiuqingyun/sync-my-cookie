# SyncMyCookie

[![License](https://img.shields.io/github/license/qiuqingyun/sync-my-cookie.svg?style=flat-square)](LICENSE)
[![Manifest V3](https://img.shields.io/badge/Manifest-V3-blue.svg?style=flat-square)](https://developer.chrome.com/docs/extensions/mv3/intro/)

> 🔄 **基于最新的 Chrome Manifest V3 标准开发**，提供更安全、更高效的 Cookie 同步体验

SyncMyCookie 是一个 Chrome 扩展程序，用于在不同设备或浏览器之间同步网站 Cookie。

通过 SyncMyCookie，您可以指定同步任意网站的 Cookie，并可配置 `自动合并` 和 `自动推送` 规则，实现更智能的 Cookie 同步。

## Manifest V3 优势

本扩展程序基于最新的 [Chrome Manifest V3](https://developer.chrome.com/docs/extensions/mv3/intro/) 标准开发，可在新版本Chrome浏览器中正常使用。

## 核心功能

- **Cookie 同步**：在不同设备或浏览器之间同步网站 Cookie
- **自动合并**：浏览器启动时自动合并已保存的 Cookie
- **自动推送**：Cookie 发生变化时自动推送到云端存储
- **智能规则**：可配置自动推送规则，只在关键 Cookie 变化时触发
- **安全保障**：使用 AES-128-CBC 加密算法保护 Cookie 安全
- **跨平台**：基于 GitHub Gist 实现跨平台数据存储
- **Manifest V3**：采用最新的 Chrome 扩展标准，提供更好的性能和安全性

## 安装方式

### 1. 预编译版本
- [预编译版本 (Manifest V3)](https://github.com/qiuqingyun/sync-my-cookie/releases/download/v3.0.0/sync-my-cookie-mv3.zip)

### 2. 源码构建

```bash
git clone https://github.com/qiuqingyun/sync-my-cookie.git
cd sync-my-cookie
yarn            # 或 npm install
yarn build      # 或 npm run build
```

构建完成后，加载 `build` 文件夹到 Chrome 扩展程序中即可。

## 使用场景

### 1. 避免频繁登录
某些网站的登录状态 Cookie 在浏览器关闭后会失效，导致我们需要频繁登录。

您可以在登录后保存该网站的 Cookie 并启用 `自动合并` 功能。这样即使浏览器关闭，网站的登录状态也不会消失。

### 2. 账号共享
您可能有以下需求：
- 与朋友共享账号
- 突破单点登录限制
- 在多个浏览器间同步登录状态

使用 SyncMyCookie 可以轻松满足以上需求。

您可以在一个浏览器上登录并启用 `自动推送` 功能，在其他浏览器上启用 `自动合并` 功能，这样您的登录状态就会在这些浏览器间同步。
  
## 配置说明

为了在设备间共享 Cookie，本扩展程序会加密您的 Cookie 并将其保存在 GitHub Gist 中，这要求您拥有一个 GitHub 账号。

如果您有关于使用其他类型存储方式的建议，请在 [这里](https://github.com/qiuqingyun/sync-my-cookie/issues) 提交 Issue。

### 生成 GitHub 访问令牌

GitHub 访问令牌（简称 token）允许扩展程序修改您的 Gist。您可以点击 [此处](https://github.com/settings/tokens/new) 生成新的令牌。

**注意事项：**

![token scopes](./assets/docs/token_scopes.jpg)

SyncMyCookie 只需要 Gist 权限，为了您的账户安全，请不要勾选其他不必要的权限。

### 配置扩展程序

右键点击扩展程序图标，选择 `选项`。

![right click](./assets/docs/right_click.jpg)

输入您的令牌和密码来加密数据。

![options](./assets/docs/options.jpg)

现在就可以自由使用此扩展程序了。

注意：如果忽略可选的 `Gist ID` 和 `文件名` 字段，扩展会创建一个新的 Gist 来存储数据。如果您想在两个浏览器间同步 Cookie，两个浏览器上的扩展程序必须具有相同的配置，即 `GitHub 访问令牌`、`密码`、`Gist ID` 和 `文件名` 这四个字段必须完全一致。插件提供了导入和导出配置的功能来帮助您完成这项工作。

## 使用方法

### 推送 Cookie
要在浏览特定网站时将该网站的 Cookie 推送到 Gist 存储中，只需打开扩展程序并点击 `推送` 按钮。

![push](./assets/docs/push.jpg)

### 合并 Cookie
要从 Gist 读取特定网站的已保存 Cookie 并让 Chrome 使用它们，只需从列表中选择该网站并点击 `合并` 按钮。

![merge](./assets/docs/merge.jpg)

### 自动合并
当为某个网站开启 `自动合并` 功能后，扩展程序会在**每次浏览器启动时**自动从 Gist 读取该网站的已保存 Cookie 并进行合并。

![Auto Merge](./assets/docs/auto_merge.jpg)

当浏览器启动时，您可以看到扩展程序图标上显示红色徽章，指示成功执行 `自动合并` 的网站数量。

![Auto Merge Badge](./assets/docs/auto_merge_badge.jpg)

### 自动推送
当为某个网站开启 `自动推送` 功能后，扩展程序会在这些 Cookie **发生变化时**自动将其推送到 Gist。

![Auto Push](./assets/docs/auto_push.jpg)

您可以看到扩展程序图标上显示绿色徽章，指示成功执行 `自动推送` 的网站数量。

![Auto Push Badge](./assets/docs/auto_push_badge.jpg)

#### 配置自动推送规则
通常，Cookie 中只有一小部分值是关键的。配置 `自动推送` 规则可以让扩展程序仅在指定值更新时执行 `自动推送`。

将鼠标悬停在 `推送` 图标上，点击出现的配置按钮。

![Config Auto Push Entry](./assets/docs/config_auto_push_entry.jpg)

选择或输入您希望在发生变化时触发 `自动推送` 的 Cookie 名称：

![Config Auto Push](./assets/docs/config_auto_push.jpg)

## 安全说明

由于 Cookie 是非常重要的安全凭证，请谨慎使用此扩展程序。

本扩展程序通过使用 `HTTPS` 和 `AES-128-CBC` 加密算法，确保您的 Cookie 在传输和存储过程中的安全，但您仍需要注意以下事项：

- 为了保证 Cookie 的安全，请不要泄露您的配置信息，特别是密码。这会导致您的 Cookie 完全暴露给他人。
- 本扩展程序保证只会使用 GitHub 访问令牌的 Gist 权限。为了防止潜在的安全问题，请在生成令牌时只勾选 Gist 权限。
- 理论上，多个设备使用相同的 Cookie 可以同时使用某些服务，但这与服务提供商的检测机制有关。因此，使用此扩展程序进行账号共享存在不确定的风险。

## 开源协议

[MIT](LICENSE) © qiuqingyun