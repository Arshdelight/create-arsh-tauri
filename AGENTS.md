# AGENTS.md

本仓库是 `create-arsh-tauri`（npm 脚手架包）。改动的验收标准：

- CLI 改动后必须本地跑一次真实生成验证：`node index.js <name> --yes`（必要时加参数），检查生成项目的 `.gitignore` / appId / productName / Cargo crate 与 lib 名 / 窗口标题，再进项目跑 `npm install`、`npm run lint`、`npx tsc --noEmit`、`npm test` 全绿；动到模板依赖、构建配置或 Rust 侧时，另进 `src-tauri` 跑 `cargo check`
- 模板目录用无点命名（`gitignore` / `temp/`），CLI 拷贝后补点——npm 发布会剔除树里的 `.gitignore` / `.npmrc`，别把点文件直接放回 template
- 验收以 `npm pack --dry-run` 的产物为准，不以源码目录为准
- 前端依赖版本与 `create-arsh-electron` 模板保持同步（react/vite/typescript/tailwind/eslint 一族），改一边要想着另一边

## 发布清单

1. `template/` 里 `npm install --package-lock-only` 刷新锁文件（每次发布都做，防止依赖树过期）
2. 根目录版本号 +1，同步 package-lock（`npm install --package-lock-only`）
3. `npm pack --dry-run` 核对文件清单（gitignore/temp 必须在列，src-tauri/icons 不得缺失）
4. commit + push（CI 不拦本仓库，发布以人工核对为准）
5. `npm publish`（人工执行）
