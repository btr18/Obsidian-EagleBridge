<p align="center">
  <img src="../logo/OEbridge.svg" alt="EagleBridge Plus" width="120" height="120">
</p>

# Obsidian EagleBridge Plus

【[中文](../README.md) / EN】

A personal fork of [Obsidian EagleBridge](https://github.com/zyjGraphein/Obsidian-EagleBridge).

The original plugin is developed by [zyjGraphein](https://github.com/zyjGraphein). **Features, installation, usage and development docs all live in the upstream repository:**

> **https://github.com/zyjGraphein/Obsidian-EagleBridge**

This page only covers **what is different here**.

## What is different

### 1. File names are sanitized before insertion

Eagle item names often contain square brackets:

```text
[おろなみんもんすたぁ (犬飼りっぽ)] ＃嫉妬系アイドル (学園アイドルマスター) [中国翻訳]
```

The original writes that straight into `![name|width](url)`. Obsidian ends the alt text at the first `]`, so the whole embed breaks — no image, just a fragment of dead Markdown.

This fork cleans the name first. Four modes, under **Settings → Upload → Image file name**:

| Mode | Result |
| --- | --- |
| Strip (default) | `おろなみんもんすたぁ 犬飼りっぽ ＃嫉妬系アイドル 学園アイドルマスター 中国翻訳.webp` |
| Replace | `【おろなみんもんすたぁ （犬飼りっぽ）】 ＃嫉妬系アイドル （学園アイドルマスター） 【中国翻訳】.webp` |
| Note title - index | note title + index |
| Custom | your own `from=>to` rules, comma-separated |

Default is **Strip**, so the fix works out of the box. Names without dangerous characters come back unchanged, and names already using full-width brackets are left alone.

### 2. Insert width follows the aspect ratio

The original has a single fixed width, so a 4000×800 banner and a 600×1200 portrait end up with the same number.

This fork reads width/height from Eagle's `metadata.json` (served by the plugin's own local server — **Eagle does not need to be running**) and scales landscape / square / portrait separately.

For the old behaviour, set **Settings → Viewer → Size mode** to "Fixed size".

### 3. Chinese settings panel

121 entries, switchable in the top-right corner of the settings panel. Default is English, so existing users see no change.

### 4. Settings panel layout fixes

Obsidian 1.14 renders every setting as a card, and the original's `padding: 12px 0` left labels and controls flush against the card edge. The custom-rules field is also nested under "Naming mode" with an indent and a left rule, matching how "Replace Eagle tags" is presented upstream.

## Download

| Version | Based on | Notes |
| --- | --- | --- |
| [0.3.4-plus](https://github.com/btr18/Obsidian-EagleBridge/releases/tag/0.3.4-plus) | Upstream release 0.3.4 | Stable baseline, recommended |
| [0.3.5-plus](https://github.com/btr18/Obsidian-EagleBridge/releases/tag/0.3.5-plus) | Upstream master (unreleased) | Adds logo, port sharing across vaults, backlink copy from Eagle |

## Installation

**Manual**: download `main.js`, `manifest.json` and `styles.css` from one of the releases above into
`.obsidian/plugins/eaglebridge-plus/`, then restart Obsidian or reload the plugin.

**BRAT**: add `btr18/Obsidian-EagleBridge`, then pick a version.

## Notes

- The plugin id is `eaglebridge-plus`, so it **does not overwrite** the upstream plugin. Both can be installed.
- They **cannot be enabled at the same time** — both bind port 6061.
- Only tested on Windows; macOS untested.

## Credits

[Obsidian EagleBridge](https://github.com/zyjGraphein/Obsidian-EagleBridge) is developed by [zyjGraphein](https://github.com/zyjGraphein). Copyright and the [GPL-3.0](../LICENSE) licence belong to the original author.

This fork only makes local modifications, submitted upstream as a PR.
