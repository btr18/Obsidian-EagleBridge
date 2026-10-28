<p align="center">
  <img src="./logo/OEbridge.svg" alt="EagleBridge Plus" width="120" height="120">
</p>

# Obsidian EagleBridge Plus

【中文 / [EN](./doc/ReadmeEN.md)】

[Obsidian EagleBridge](https://github.com/zyjGraphein/Obsidian-EagleBridge) 的个人修改版。

原插件由 [zyjGraphein](https://github.com/zyjGraphein) 开发。**功能说明、安装步骤、使用教程、开发文档都以原仓库为准**：

> **https://github.com/zyjGraphein/Obsidian-EagleBridge**

这个 README 只写**和原版不一样的地方**，重复的就不抄了。

## 和原版相比多了什么

### 1. 插入图片前先清洗文件名

Eagle 里的素材名经常带方括号，比如：

```text
[おろなみんもんすたぁ (犬飼りっぽ)] ＃嫉妬系アイドル (学園アイドルマスター) [中国翻訳]
```

原版把它原样塞进 `![文件名|宽度](地址)`，Obsidian 在第一个 `]` 处就判定 alt 结束，整行嵌入失效 —— 图片不显示，笔记里只留一段废掉的 Markdown。

这个版本在插入前先处理文件名，四种方式可选（**设置 → 上传设置 → 图片文件名**）：

| 方式 | 上面那个文件名会变成 |
| --- | --- |
| 去除（默认） | `おろなみんもんすたぁ 犬飼りっぽ ＃嫉妬系アイドル 学園アイドルマスター 中国翻訳.webp` |
| 替代 | `【おろなみんもんすたぁ （犬飼りっぽ）】 ＃嫉妬系アイドル （学園アイドルマスター） 【中国翻訳】.webp` |
| 编号 | 笔记标题 + 序号 |
| 自定义 | 自己写 `原=>新` 规则，逗号分隔 |

默认「去除」，装上去就生效。本来没有危险字符的文件名原样返回；已经用全角括号的不会被重复处理。

### 2. 插入宽度按宽高比自适应

原版只有一个固定宽度，4000×800 的长图和 600×1200 的竖图用同一个值。

这个版本从 Eagle 的 `metadata.json` 读宽高（插件自己的本地服务直接读盘，**不需要打开 Eagle**），按横图 / 方图 / 竖图分别乘不同倍率。

想退回原版的一刀切，把 **设置 → 预览设置 → 宽度模式** 改成「固定大小」即可。

### 3. 设置面板中文化

121 条词条，右上角可切中英文。默认英文，原来用英文的人升级后界面不变。

### 4. 设置面板排版整理

Obsidian 1.14 把设置项渲染成卡片后，原版的 `padding: 12px 0` 会让标题和控件贴死卡片边缘；另外「自定义规则」用缩进 + 左侧竖线标成「命名方式」的子项，和「覆盖 Eagle 标签」用的是同一套表达。

## 下载

| 版本 | 基于 | 说明 |
| --- | --- | --- |
| [0.3.4-plus](https://github.com/btr18/Obsidian-EagleBridge/releases/tag/0.3.4-plus) | 作者发布版 0.3.4 | 稳定基线，推荐 |
| [0.3.5-plus](https://github.com/btr18/Obsidian-EagleBridge/releases/tag/0.3.5-plus) | 作者 master（尚未发版） | 多出 logo、多库端口共享、Eagle 面板回链复制 |

## 安装

**手动**：从上面任一版本的 release 页下载 `main.js`、`manifest.json`、`styles.css` 三个文件，放进
`.obsidian/plugins/eaglebridge-plus/`，重启 Obsidian 或在设置里重载插件。

**BRAT**：添加仓库 `btr18/Obsidian-EagleBridge`，再选版本。

## 注意

- 插件 id 是 `eaglebridge-plus`，**不会覆盖原版**，两个可以同时安装。
- 但**不能同时启用** —— 都要占用 6061 端口，二选一。
- 只在 Windows 上验证过；macOS 未测试。

## 致谢

原插件 [Obsidian EagleBridge](https://github.com/zyjGraphein/Obsidian-EagleBridge) 由 [zyjGraphein](https://github.com/zyjGraphein) 开发，版权与 [GPL-3.0](./LICENSE) 许可均归原作者。

本仓库仅在其基础上做局部修改，改动已作为 PR 提交给原作者。
