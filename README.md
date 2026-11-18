# heyunl Devin marketplace

Personal Devin plugin marketplace, using the same layout as
[CognitionAI/devin-marketplace](https://github.com/CognitionAI/devin-marketplace).
The root `.devin-plugin/plugin.json` is a meta-plugin that lists every offering
under `optionalPlugins`.

| Plugin | What it does |
|---|---|
| [`haina`](plugins/haina) — 海纳-什么值得买 MCP | 什么值得买 deals, product search, specs, SKUs and reviews |
| [`siyuan-sisyphus`](plugins/siyuan-sisyphus) — SiYuan Sisyphus MCP | Read and safely edit local SiYuan notes (Desktop/CLI only; needs `SIYUAN_TOKEN`) |

## Installing in Devin

Customize → Plugins → Add plugin → **From repository**, enter
`heyunl/devin-marketplace`:

* leave the subdirectory empty to install the whole marketplace, or
* set it to `plugins/<slug>` to install a single plugin.

Then open Customize → MCPs and **Connect** the server, entering its credential
(for `haina`: `HAINA_API_KEY`, the 海纳 open-platform API key). Credentials live
in Devin only; nothing in this repo holds one.

Merging to `main` is the release: run **Plugin settings → Reindex plugins** in
Customize and start a new session.

## Adding a plugin

See [`.agents/skills/adding-a-plugin/SKILL.md`](.agents/skills/adding-a-plugin/SKILL.md).

* **Your own plugin**: create `plugins/<slug>/.devin-plugin/plugin.json` and add
  `"./plugins/<slug>"` to `optionalPlugins`.
* **An official plugin**: add a pinned reference to `optionalPlugins` instead of
  copying it:

  ```json
  {
    "source": "git-subdir",
    "url": "https://github.com/CognitionAI/devin-marketplace.git",
    "path": "plugins/notion",
    "sha": "<40-hex commit>"
  }
  ```

Run `python3 scripts/validate.py --fix` (and `--fetch` to check upstream pins)
before committing; CI runs the same check.

## License

[MIT](LICENSE)
