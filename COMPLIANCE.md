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

4. **标注来源,商业分发前完成改名**
   - 已公开的其他 fork(如 `fcitx5-android-bibi-keyboard`、`fcitx5-android-t9-phone`)多数只
     改了**仓库名**,应用名仍是 `Fcitx5`、包名仍是 `org.fcitx.fcitx5.android`。这些是个人
     分发的非商业 fork,风险敞口小;**预装到硬件对外销售不适用同一套做法**。
   - 上游未随仓库提供商标许可文件;`fcitx` 名称与 logo 的权利状态(是否已注册)需自行核实。
     稳妥做法:应用名、包名、图标全部换掉(见第三节),彻底避免混淆与冒用指控。
   - 在「关于」页标明:本产品基于 fcitx5-android 修改,附原项目链接与许可入口。

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

## 七、谁承担合规义务:分发者(distributor)

LGPL 的义务落在**向第三方分发二进制的那个人**身上,而不是「写代码的人」。因此要分清三种角色:

| 角色 | 行为 | 合规义务 |
|---|---|---|
| 开发者 / 受托修改者 | 改代码、提交、在公开仓库发布**源码** | 源码本身须保持 LGPL 且带变更声明;这是本仓库已满足的部分 |
| 分发者(公司) | 把 APK 打包进设备、出厂、销售、提供 OTA | 提供对应源码、LICENSE、NOTICE、允许替换 `.so`、改名避商标 |
| 纯内部测试 | 只在自己设备上装 | 基本无对外义务 |

**结论:只要最终 APK 由公司烧录/销售,公司就是分发者,对外义务与责任在公司。**
但有两种情况会把义务拉回个人:

1. 个人账号**公开发布 APK**(GitHub Release、网盘、商店)→ 个人也构成分发者;
2. 公开仓库挂在**个人 GitHub 账号**下并由个人运营 → 个人是该发布行为的名义主体
   (GitHub 服务条款下账号所有者对账号活动负责)。

因此最干净的结构是:**修改产出的著作权与对外发布主体都归公司**(迁移到公司组织仓库或由公司
出具授权),个人只作为受托开发者。对应的合同文本见 `D:\AI\legal\`(不在本公开仓库内)。

## 八、源码提供方式(分发时必须二选一以上)

- **随附源码**:设备/发布页同时给出与本二进制**同 commit** 的源码地址与构建说明;
- **书面要约**:随附一份「可向下列地址索取对应源码」的书面声明,有效期不少于三年。

本仓库做法:源码公开在 fork 分支,`NOTICE.md` 记录改动清单与日期;
若后续改名,需保证改名后的版本也在同一公开仓库有对应 commit。
