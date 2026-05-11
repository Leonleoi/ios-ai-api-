# AI Chat iOS 应用 - IPA 部署指南

## 📦 IPA 文件信息

**文件位置**: `/Users/leonlei/Documents/ipa test/AI Chat/build/output/AI_Chat.ipa`

**文件大小**: 118 KB (未签名版本)

**构建配置**:
- Build Configuration: Release
- Platform: iOS (arm64)
- Minimum Deployment Target: iOS 17.0
- Swift Version: 5.9+

## 📱 应用功能

### 核心特性
- ✅ 多 AI 提供商支持 (OpenAI, Ollama, Claude 等)
- ✅ 流式响应显示
- ✅ 多语言支持 (中文 & English)
- ✅ 设置管理和提供商配置
- ✅ 聊天记录管理

### 适配特性 ✨ 新增
- ✅ 全面的 iPhone 尺寸适配（SE 到 Pro Max）
- ✅ 竖屏和横屏双向支持
- ✅ 自适应布局和字体大小
- ✅ 小屏幕优化显示

## 📋 应用参数

**Bundle Identifier**: `com.aichat.app`

**Supported Devices**: 
- iPhone SE (2nd generation and later)
- iPhone XS, XS Max, XR
- iPhone 11, 11 Pro, 11 Pro Max
- iPhone 12, 12 mini, 12 Pro, 12 Pro Max
- iPhone 13, 13 mini, 13 Pro, 13 Pro Max
- iPhone 14, 14 Plus, 14 Pro, 14 Pro Max
- iPhone 15, 15 Plus, 15 Pro, 15 Pro Max
- iPhone 16, 16 Plus, 16 Pro, 16 Pro Max

**Supported Orientations**: 
- Portrait
- Landscape

## ⚠️ 重要说明

### 代码签名
此 IPA 文件**未签名**（Unsigned），这意味着：

1. **无法直接安装到 iPhone**
   - 需要 Apple 开发者账号和有效的签名证书才能部署到真实设备
   - 可以在 iOS 模拟器上直接运行

2. **如何使用模拟器**
   ```bash
   # 在 Xcode 中打开项目
   xed "/Users/leonlei/Documents/ipa test/AI Chat/AI_Chat.xcodeproj"
   
   # 选择模拟器为 target
   # 按 Cmd+R 运行应用
   ```

3. **要签名应用**
   需要：
   - Apple 开发者账号 ($99/年)
   - 有效的签名证书和 provisioning profile
   - Team ID 配置

## 🔧 如何生成签名版本

### 方法 1: 使用 Xcode (推荐)
1. 打开项目: `open AI_Chat.xcodeproj`
2. 在 Signing & Capabilities 中设置 Team
3. Product → Archive
4. Distribute App → App Store Connect (或其他选项)

### 方法 2: 命令行
```bash
cd "/Users/leonlei/Documents/ipa test/AI Chat"

# 设置 Team ID（替换为你的 Team ID）
TEAM_ID="YOUR_TEAM_ID"

# 构建并导出
xcodebuild archive \
  -scheme AI_Chat \
  -configuration Release \
  -archivePath "./build/AI_Chat.xcarchive" \
  -destination generic/platform=iOS \
  DEVELOPMENT_TEAM=$TEAM_ID

xcodebuild -exportArchive \
  -archivePath "./build/AI_Chat.xcarchive" \
  -exportOptionsPlist "./build/ExportOptions.plist" \
  -exportPath "./build/output"
```

## 🛠️ 技术详情

### 项目结构
```
AI Chat/
├── AI_Chat/
│   ├── Views/              # SwiftUI 视图
│   ├── ViewModels/         # MVVM 视图模型
│   ├── Models/             # 数据模型
│   ├── Services/           # 业务逻辑
│   ├── Utils/              # 工具类（新增 LayoutGuide）
│   ├── ContentView.swift    # 主视图
│   └── AI_ChatApp.swift     # 应用入口
└── AI_Chat.xcodeproj       # Xcode 项目
```

### 依赖项
- SwiftUI (内置)
- URLSession (内置)
- Foundation (内置)

## 📚 构建文件

| 文件 | 用途 |
|-----|------|
| `AI_Chat.ipa` | 最终应用包 |
| `AI_Chat.xcarchive/` | 构建归档文件 |
| `ExportOptions.plist` | 导出配置文件 |

## ✅ 验证清单

- [x] 源代码编译成功
- [x] Release 构建完成
- [x] Archive 创建成功
- [x] IPA 包已生成
- [x] iPhone 尺寸适配完成
- [ ] 代码签名（需开发者账号）
- [ ] 在实体设备上测试（需签名）

## 📞 后续支持

如需进一步支持：
1. 代码签名配置
2. App Store 提交
3. TestFlight 分发
4. 功能扩展开发

请告知需求！

---

**构建时间**: 2026-05-11 17:08
**构建系统**: macOS + Xcode 16
