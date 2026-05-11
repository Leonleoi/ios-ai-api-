# iPhone 尺寸适配方案

## 概览
已为 AI Chat 应用完成全面的 iPhone 尺寸适配，支持从 iPhone SE（小屏）到 iPhone 16 Pro Max（大屏）的所有设备。

## 适配策略

### 1. 屏幕尺寸分类
- **小屏幕 (< 375pt)**：iPhone SE, iPhone 6/7/8
- **标准屏幕 (375-428pt)**：iPhone 12/13, iPhone 14, iPhone 15
- **大屏幕 (≥ 428pt)**：iPhone 14/15 Plus, Pro Max 系列
- **横屏紧凑模式**：任何设备在横屏模式

### 2. 主要改动

#### ✅ ChatView
- 根据屏幕宽度调整消息间距 (8-12pt)
- 输入框高度适配 (40-48pt)
- 输入框字体自动缩放 (14-16pt)
- 空状态图标动态调整 (36-48pt)
- 空状态文字 padding 自适应 (16-32pt)

#### ✅ MessageBubbleView
- 气泡最大宽度智能计算：
  - 横屏紧凑: 55%屏幕宽度
  - 小屏幕: 75%屏幕宽度
  - 其他: 78%屏幕宽度
- 气泡内边距自适应 (12-16pt 水平, 8-10pt 竖直)
- 圆角半径优化 (16-20pt)

#### ✅ SettingsView & LanguagePickerView
- List 样式统一为 .insetGrouped
- 列表行高在横屏紧凑模式自动调整 (56pt)
- 支持小屏幕显示优化

#### ✅ ProviderConfigView
- 添加横屏紧凑模式检测
- Form 间距动态调整

#### ✨ 新增 LayoutGuide.swift
- 集中管理所有响应式设计数据
- 未来可扩展使用 (可选)

## 支持的适配

| 特性 | 小屏 | 标准 | 大屏 | 横屏 |
|------|------|------|------|------|
| 自适应 padding | ✓ | ✓ | ✓ | ✓ |
| 自适应字体大小 | ✓ | ✓ | ✓ | ✓ |
| 自适应间距 | ✓ | ✓ | ✓ | ✓ |
| 自适应按钮大小 | ✓ | ✓ | ✓ | ✓ |
| 列表优化 | ✓ | ✓ | ✓ | ✓ |

## 技术实现

- 使用 `UIScreen.main.bounds.width` 获取屏幕宽度
- 使用 `@Environment(\.horizontalSizeClass)` 检测设备方向
- 根据条件计算动态值，无需硬编码
- 充分利用 SwiftUI 的响应式特性

## 测试建议

1. 在不同 iPhone 型号上运行应用
2. 测试竖屏和横屏模式
3. 验证消息气泡宽度和位置
4. 检查输入框的可用性
5. 确认设置页面的列表显示效果

## 文件变更

- `ChatView.swift` - 优化布局和字体大小
- `MessageBubbleView.swift` - 动态气泡宽度和样式
- `SettingsView.swift` - 列表行高和样式优化
- `LanguagePickerView.swift` - 列表行高优化
- `ProviderConfigView.swift` - 添加屏幕检测
- `LayoutGuide.swift` - 新增响应式设计 Helper (可选使用)

## 后续优化方向

1. 可在 LayoutGuide.swift 中统一管理所有响应式数值
2. 考虑 iPad 横屏模式的特殊适配
3. 添加动态字体大小支持 (使用 @ScaledMetric)
4. 测试无障碍功能 (Large Text 等)
