# 版权与来源声明(Notice / Attribution)

## 本项目

本产品是基于开源项目 **fcitx5-android** 的衍生版本(修改版)。

- 原项目:https://github.com/fcitx5-android/fcitx5-android
- 原项目许可:**LGPL-2.1-or-later**(全文见 `LICENSE`)
- 原项目版权:**Copyright 2021-2026 Fcitx5 for Android Contributors**
- 本修改版源码:https://github.com/yxg123/fcitx5-android (branch `feature/force-landscape`)

### 我方修改内容

下表列出本修改版相对上游的全部代码改动。所有改动均以 **LGPL-2.1-or-later** 发布,
修改过的源文件保留原 SPDX 版权头,并追加 `Modified <日期>` 变更声明。

| 文件 | 改动 |
|---|---|
| `app/build.gradle.kts` | 裁剪内置输入法表,仅保留拼音与英文(keyboard-us) |
| `data/prefs/AppPrefs.kt` | 相关默认值调整 |
| `input/FcitxInputMethodService.kt` | 系统竖屏时整体旋转 90° 强制横屏显示;调整 insets 与可触摸区域 |
| `input/InputView.kt` | 键盘高度百分比以屏幕短边为基准(横屏基准) |
| `input/candidates/expanded/ExpandedCandidateLayout.kt` | 固定使用横屏边距参数 |
| `input/candidates/expanded/window/GridExpandedCandidateWindow.kt` | 固定使用横屏网格列数 |
| `input/candidates/horizontal/HorizontalCandidateComponent.kt` | 固定使用横屏候选栏最大列数 |
| `input/keyboard/KeyDefPreset.kt` | 字母键去掉右上角小字与长按弹窗;逗号键改为纯文字(移除表情图标);新增九宫格数字键定义 |
| `input/keyboard/KeyView.kt` | 固定按横屏计算边距与布局 |
| `input/keyboard/NumberKeyboard.kt` | 九宫格数字键盘布局:底行「ABC / 0 / 删除」等宽对齐 |
| `input/keyboard/TextKeyboard.kt` | 字母键盘布局微调 |

修改日期:2026-10-29

## 第三方组件许可清单

以下组件随本产品分发,许可文本见各组件仓库或其许可文件。

| 组件 | 版本 | 许可 | 来源 |
|---|---|---|---|
| fcitx5 | 5.1.21 | LGPL-2.1-or-later | https://github.com/fcitx/fcitx5 |
| libime | 1.1.15 | LGPL-2.1-or-later | https://github.com/fcitx/libime |
| fcitx5-lua | 5.0.17 | LGPL-2.1-or-later | https://github.com/fcitx/fcitx5-lua |
| fcitx5-chinese-addons | 5.1.13 | GPL-2.0-or-later / LGPL-2.1-or-later | https://github.com/fcitx/fcitx5-chinese-addons |
| boost | 1.90.0 | BSL-1.0 | https://www.boost.org/ |
| zstd | 1.5.7 | BSD-3-Clause / GPL-2.0-only | https://www.zstd.net |
| OpenCC | 1.2.0 | Apache-2.0 | https://opencc.byvoid.com/ |
| lua | 5.4.7 | MIT | https://www.lua.org/ |
| libuv | 1.52.0 | MIT | https://libuv.org/ |
| libintl-lite | edbb306 | BSL-1.0 | https://github.com/j-jorge/libintl-lite |

> 完整、逐项许可文本可通过本产品「设置 → 关于 → 开源许可」页面查看(应用内置展示)。

## 商标声明

- 本产品**不是** Fcitx / fcitx5-android 官方发行版,未获得 Fcitx 项目或其贡献者的
  商标使用许可、背书或担保。
- 若本产品最终仍需在名称、包名或图标中使用 `fcitx` 字样,该使用仅用于**事实性描述**
  (说明本产品派生自该项目,即 nominative/描述性使用),不得暗示官方身份。
- 正式对外销售前建议完成改名(见 `COMPLIANCE.md` 第三节),彻底避免混淆。
