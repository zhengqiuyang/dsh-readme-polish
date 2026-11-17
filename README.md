<a id="top"></a>

<div align="center">

# 📝 dsh-readme-polish

**A DeepSeek Harness plugin that puts the `readme-polish` skill into your profile's skill catalog — install once, every agent in that profile can use it.**

把 `readme-polish` 技能打包进 DeepSeek Harness：装一次，profile 里所有 agent 都能用。把已有 README 升级到同生态头部仓库的水准。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![Stars](https://img.shields.io/github/stars/zhengqiuyang/dsh-readme-polish?style=flat-square&color=0969da)](https://github.com/zhengqiuyang/dsh-readme-polish/stargazers)

```bash
dsh plugin add dsh-readme-polish
```

[What it does](#what) · [Why a plugin](#why) · [Usage](#usage) · [Verification](#verification) · [Structure](#structure)

**If this helps you, please give it a star** — it helps others find it.

</div>

---

<a id="what"></a>

## What it does / 它做什么

The bundled `readme-polish` skill upgrades an **existing** README to the standard of the top repositories in its own ecosystem:

1. **Ecosystem calibration** — samples two or three head repositories in the same category and picks an archetype: minimal typographic or full-component.
2. **Component selection** — a decision table for badges, mermaid, callouts, `<details>`, heroes and banners, with the condition under which each earns its place.
3. **Rewrite** — one-line value proposition, explicit anchors, comparison tables where they beat prose, bilingual structure where needed.
4. **Deterministic gate** — `scripts/check_readme.py` checks dead local links, broken images, Chinese anchor drift, mermaid node count, table width, badge count, and whether an install command is above the fold.

<a id="why"></a>

## Why a plugin / 为什么做成插件

The skill alone only needs a directory under `~/.agents/skills/`. The plugin buys the profile-level lifecycle: one install command, the skill appears in the Plugins inventory with its own entry and detail page, updates go through the plugin manager, and it is removed cleanly with the bundle.

<a id="usage"></a>

## Usage / 用法

Ask in natural language; there is no slash command:

```text
把我的 README 打磨一下
this README looks plain, compare it with popular repos
add badges / mermaid / callouts to the README
```

When the content is already good the correct output is small — the skill is calibrated to say so rather than pad the page.

## How it works / 工作原理

`index.js` registers a skill provider with `ctx.skills.registerProvider`. At catalog time the provider reads `skills/readme-polish/SKILL.md` from the package and returns it as a bundled candidate whose resource base is the skill directory, so `references/` and `scripts/` resolve. No network calls, no dependencies, no model calls of its own.

<a id="verification"></a>

## Verification / 验证

- **Provider logic** — `npm test` registers the provider against a stub context, asserts the candidate metadata and loads the skill body.
- **Install** — installed into a DSH profile as bundle `dsh-readme-polish` 0.1.2; the installer reported `application: applied` with no warnings.
- **Skill catalog** — verify in a new session: a running session builds its catalog at start, so the plugin's skill appears only after reopening.

<a id="structure"></a>

## Structure / 结构

```
package.json          # manifest + dsh.bundle.patch
cordis.patch.yml      # inserts the plugin row into the profile
index.js              # skill provider
locale/{en,zh}.json   # Plugins title / description / detail
icon.svg
docs/DETAIL.md
skills/readme-polish/ # bundled skill (SKILL.md, references, scripts)
test/provider.test.mjs
```

## Source / 来源

The skill lives in its own repository, [zhengqiuyang/readme-polish](https://github.com/zhengqiuyang/readme-polish), and is copied into `skills/readme-polish/` here so the package is self-contained.

## License

MIT
