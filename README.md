# AI Chat

多 API 提供商的 AI 聊天 iOS 客户端，支持多语言切换。

## 功能

- 多 API 提供商支持（可配置）
- 多语言界面（简体中文 / English）
- 消息记录管理
- 适配所有 iPhone 屏幕尺寸（SE ~ 16 Pro Max）

## 构建要求

- Xcode 16.4+
- iOS 17.0+
- Swift 6.0

## 构建步骤

### 1. 用 Xcode（推荐）

打开项目，选择 target 为 `AI_Chat`，连接设备后 Run：

```bash
open AI_Chat.xcodeproj
```

### 2. 命令行构建 IPA

```bash
# Release 构建（不签名）
xcodebuild clean build \
  -project AI_Chat.xcodeproj \
  -target AI_Chat \
  -sdk iphoneos \
  -configuration Release \
  CODE_SIGNING_ALLOWED=NO \
  CODE_SIGNING_REQUIRED=NO

# 打包为 IPA
mkdir -p Payload
cp -R build/Release-iphoneos/AI_Chat.app Payload/
zip -ry AI_Chat.ipa Payload/
rm -rf Payload
```

### 3. 安装到设备

IPA 未签名，需使用以下工具自签安装：

- [AltStore](https://altstore.io)
- [Sideloadly](https://sideloadly.io)
- SideStore
- 爱思助手
- TrollStore

## 项目结构

```
AI_Chat/
├── AI_ChatApp.swift          # App 入口，语言切换
├── ContentView.swift         # 主视图
├── Info.plist
├── Models/
│   ├── ChatMessage.swift     # 消息模型
│   ├── APIConfiguration.swift
│   └── APIProvider.swift     # API 提供商枚举
├── Services/
│   ├── AIService.swift       # API 调用服务
│   └── SettingsStorage.swift # 设置持久化
├── ViewModels/
│   └── ChatViewModel.swift   # 聊天逻辑
├── Views/
│   ├── ChatView.swift
│   ├── MessageBubbleView.swift
│   ├── SettingsView.swift
│   ├── ProviderConfigView.swift
│   └── LanguagePickerView.swift
└── Utils/
    └── LayoutGuide.swift     # 屏幕适配工具
```

## 配置

在 app 设置中配置你的 API 地址和密钥即可使用。
