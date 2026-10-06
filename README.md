# COMO能量贴纸

一个将用户上传照片转成 COMO 能量主题贴纸的 Codex Skill。

Skill 会读取本轮提供的照片，并在 COMO 项目上下文中读取当前用户已有的能量字段。它保留照片中的主体关系，用对应能量色和图形氛围创作平面矢量贴纸。

蘑菇参照 [标准形态图](assets/como-mushroom-standard.png)，只作为留白边缘约 3–5% 画布宽、低存在感的水印式彩蛋；主体和能量构图始终优先。

## 使用

在 Codex 中调用 $como-energy-sticker-i2i，并提供要处理的照片。没有可读取的当前能量时，Skill 会说明情况，不会猜测或替用户选择。

仓库地址：https://github.com/lingskab/COMO-energy-sticker

克隆到 ~/.codex/skills/como-energy-sticker-i2i 后即可使用。Codex 若未立即发现新 Skill，可重新打开应用。

## 许可

本仓库内容按 CC BY-NC 4.0 发布。允许非商业用途的分享与改编，须提供适当署名、附许可证链接并标明改动；禁止商业用途。完整条款见 [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/legalcode.en)。
