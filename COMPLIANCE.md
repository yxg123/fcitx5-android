# 合规使用说明(LGPL-2.1-or-later)

> 本文档供「基于 fcitx5-android 修改后打包 APK、预装到自研设备销售」场景使用。
> 它不是法律意见;正式商用前请让公司法务/律师复核。

## 一、许可证结论

- **应用层代码(你要改的 UI 部分,`app/` 下的 Kotlin)**:`LGPL-2.1-or-later`
  版权:`Copyright 2021-2023 Fcitx5 for Android Contributors`
- **原生组件**:以 `LGPL-2.1-or-later` 及宽松许可(MIT / BSD-3-Clause / Apache-2.0 / BSL-1.0)为主。
  完整清单见同目录 `NOTICE.md`。

LGPL 是「宽松」版 GPL,**允许商业使用,且不要求你开源自己的专有代码**。

## 二、必须做的 4 件事

1. **保留许可证与版权声明**
   - 保留根目录 `LICENSE`(LGPL-2.1 原文),不要删除。
   - 保留源码文件头的 SPDX 声明(如 `SPDX-License-Identifier: LGPL-2.1-or-later`)。

2. **开源你改动过的 LGPL 组件**
   - 你修改了哪部分 LGPL 代码,那部分改动必须以 **LGPL-2.1-or-later** 开源,并在文件头标注你修改的日期与内容。
   - 你**自己新写**的、仅「调用」该库的专有代码,**无需开源**。
   - 建议做法:在 GitHub 开一个 fork 仓库,把改动 push 上去即可(仓库 README 模板见第四节)。

3. **允许用户替换/重新链接 LGPL 库**
   - Android 上原生库以 `.so` 动态链接分发,天然满足「允许重新链接」的要求。
   - 不要做阻止用户替换 `.so` 的技术手段(如签名校验锁死、混淆原生符号)。

4. **改名 + 标注来源,避免商标误导**
   - "fcitx" 及 logo 是商标,不得冒用。应用名、包名、图标必须换掉(见第三节)。
   - 在「关于」页标明:本产品基于 fcitx5-android 修改,附原项目链接。

## 三、改名清单(具体文件)

| 位置 | 现值 | 改成 |
|---|---|---|
| `app/build.gradle.kts:13` `namespace` | `org.fcitx.fcitx5.android` | 自己的,如 `com.<公司>.<产品>` |
| `app/build.gradle.kts:16` `applicationId` | `org.fcitx.fcitx5.android` | 同上 |
| `app/src/main/res/values/strings.xml:3` `app_name_release` | `Fcitx5` | 自己的产品名 |
| `app/src/main/res/values/strings.xml:4` `app_name_debug` | `Fcitx5 (Debug)` | 自己的产品名 |
| `app/src/main/res/mipmap-*/ic_launcher*` | fcitx logo | 换成自己的图标 |
| 关于页 `app/src/main/java/.../ui/main/AboutFragment.kt` | — | 增加「基于 fcitx5-android」来源说明与许可入口 |

> 注意:改 `applicationId` 后,内部 R 类包名、`BuildConfig` 引用会跟着 `namespace` 走,一般无需手动改;
> 若有用到硬编码 `org.fcitx` 字符串的地方,全局搜索替换即可。

## 四、fork 仓库 README 模板

对外分发时,把下面的 README 放在你的 fork 仓库根目录(与 `LICENSE`、`NOTICE.md` 并列):

```markdown
# <你的产品名> 输入法

本项目是基于 [fcitx5-android](https://github.com/fcitx5-android/fcitx5-android) 的衍生版本。

## 修改内容
- 默认横屏布局
- (其他 UI 调整……)

## 许可
- 本项目遵循与原项目相同的 **LGPL-2.1-or-later** 许可,见 [LICENSE](LICENSE)。
- 我们对 LGPL 组件的修改同样以 LGPL-2.1-or-later 发布。
- 版权与第三方组件许可详见 [NOTICE.md](NOTICE.md)。

## 原项目
- 仓库:https://github.com/fcitx5-android/fcitx5-android
- 版权:Fcitx5 for Android Contributors
```

## 五、关于双许可的 GPL 组件(建议法务确认)

- `fcitx5-chinese-addons` 声明为 `GPL-2.0-or-later + LGPL-2.1-or-later`;
- `zstd` 声明为 `BSD-3-Clause + GPL-2.0-only`。
  二者均提供非 GPL 的选择(可选用 LGPL / BSD 一侧)。为避免触发 GPL 的更强传染义务,
  建议让法务确认「按 LGPL-2.1 / BSD-3-Clause 一侧使用」是否成立,并在产品文档中记录所选的许可侧。

## 六、交付前自检清单

- [ ] `LICENSE` 文件保留在仓库与 APK 中
- [ ] 源码 SPDX 版权头未被删除
- [ ] 改名完成(包名 / 应用名 / 图标)
- [ ] 关于页有来源声明与许可入口
- [ ] fork 仓库已公开,含 `LICENSE`、`NOTICE.md`、README
- [ ] 我方对 LGPL 组件的改动已按 LGPL-2.1-or-later 开源
- [ ] 法务已确认双许可组件所选许可侧
