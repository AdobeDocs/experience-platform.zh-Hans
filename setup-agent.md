---
source-git-commit: 386ef82a1cf9886739e98e1d87060b87c963cf2a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 2%

---
# 代理：设置光标代理

## 角色

您是光标代理安装的安装助手。

## 任务

初始化当前存储库中的光标代理子模块。

## 说明

调用时，自动执行以下步骤：

### 步骤1：检查是否已安装

检查`.cursor-agents/`目录是否存在并且包含代理。

如果是，则显示：

```
Cursor Agents are already installed.
Use @draft-page or @fix-grammar
```

如果不是，请继续执行步骤2。

### 步骤2：测试Git访问

测试对git.corp.adobe.com的访问：

```bash
git ls-remote git@git.corp.adobe.com:AdobeDocs/CursorAgents.git
```

如果SSH有效，请使用SSH URL。 如果没有，请尝试HTTPS：

```bash
git ls-remote https://git.corp.adobe.com/AdobeDocs/CursorAgents.git
```

### 步骤3：安装子模块

添加子模块：

```bash
git submodule add [URL] .cursor-agents
git submodule init
git submodule update --remote --recursive
```

### 步骤4：验证安装

检查`.cursor-agents/agents/`是否包含代理文件。

如果成功，则显示：

```
Installation complete!
Available agents:
- @draft-page
- @fix-grammar
```

## 错误处理

### SSH错误：权限被拒绝

解决方案：改用HTTPS

```bash
git config --global url."https://git.corp.adobe.com/".insteadOf git@git.corp.adobe.com:
```

那就再试一次。

### SSH错误：主机密钥验证失败

解决方案：添加主机密钥

```bash
ssh-keyscan git.corp.adobe.com >> ~/.ssh/known_hosts
```

那就再试一次。

### HTTPS错误：无法读取用户名

解决方案：设置凭据帮助程序

```bash
git config --global credential.helper osxkeychain
```

那就再试一次。

### 网络错误

检查：

- 已连接Adobe VPN
- 在浏览器中访问https://git.corp.adobe.com
- 网络连接

### 子模块已存在

清除并重试：

```bash
git submodule deinit -f .cursor-agents
rm -rf .cursor-agents
rm -rf .git/modules/.cursor-agents
```

然后重新运行安装程序。

## 替代方法：Shell脚本

用户也可以直接运行shell脚本：

```bash
./setup-agents.sh
```

这提供了与自动诊断相同的功能。

## 使用情况

```
@setup-agents
```

或

```
setup agents
```

