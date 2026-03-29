# 03 — Copilot + Worker 架构流程图

> **用途：** "核心架构" 区块的视觉说明
> **尺寸：** 1600×600
> **文件名：** architecture-flow.png

## Prompt

A horizontal workflow diagram on a warm cream background (#FAF9F0), illustrating an AI task orchestration system:

From left to right:
1. A person icon (simple geometric, dark gray) with label "管理者" (Manager)
2. An arrow pointing right
3. A prominent hexagonal node in amber (#F59E0B) labeled "Copilot" with a brain icon inside — this is the central coordinator
4. The Copilot node branches out into 4 parallel paths (using smooth curved lines in teal #0D9488)
5. Each path leads to a rounded rectangle labeled "Worker" with different task icons:
   - Worker 1: document icon + "数据采集"
   - Worker 2: magnifying glass + "分析研判"
   - Worker 3: pencil + "文档生成"
   - Worker 4: plug/connector + "系统对接"
6. All 4 Worker paths converge into a single arrow pointing to a checkmark circle in green/teal labeled "结果交付"

Style: Flat, geometric, minimal. Lines are clean with slight rounded ends. The Copilot node is visually dominant (larger, amber fill). Worker nodes are smaller (teal outline, white fill). Connection lines have subtle animated-flow dots suggestion (static dots along the path suggesting data movement). No gradients except very subtle ones on the Copilot node. Chinese labels in clean sans-serif font.

## 用途说明
解释 SudoClaw 的核心工作原理：用户给 Copilot 一个意图，Copilot 拆解后 Worker 并行执行。这张图需要一眼就能传达"一个指令 → 多个 AI 并行干活 → 结果交付"。
