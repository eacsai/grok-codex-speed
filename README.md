# grok-codex-speed

测 Grok / Codex 的 **thinking + writing tokens/s**，不计工具墙钟。默认 prompt 大约 2000 output tokens。

- `grok-speed`：关工具，用 `duration_api_ms`
- `codex-speed`：只读 sandbox，用 `turn.started → turn.completed`
- `clash-port`：探测本机 ClashX mixed-port（`codex-speed` 依赖它）

## 安装

需要 macOS、`python3`、`~/.local/bin` 在 `PATH` 里。Grok 走已安装的 `grok`；Codex 走 ChatGPT.app 里的 CLI（避开 PATH 上的 cmux shim）。

```bash
git clone https://github.com/eacsai/grok-codex-speed.git
cd grok-codex-speed
install -m 755 grok-speed codex-speed clash-port ~/.local/bin
```

ClashX 要在跑。`clash-port` 只认 `*:port` / `127.0.0.1:port`，不读 Clash Verge yaml。

## 用法

```bash
grok-speed
codex-speed

grok-speed 3
codex-speed --effort high
grok-speed -m grok-4.6 --effort xhigh
codex-speed --effort low "Do not use tools. Reply with only: DONE"
```

默认模型 / effort 分别来自 `~/.grok/config.toml` 和 `~/.codex/config.toml`。看结果里的 `output=` 才是实际长度。停测：Ctrl+C。

每次调用会消耗对应产品的额度。
