# jev-mcp (patched for thejevai.com)

Fork of [codaaiteam/jev-mcp](https://github.com/codaaiteam/jev-mcp) with two fixes for `sk_*` keys against [thejevai.com](https://thejevai.com):

1. Default `JEV_BASE_URL` for non-`jv_live_` keys is `https://thejevai.com/v1/systemone` (stock historically defaulted to `api.typesafe.ai` and 401'd).
2. Unwrap thejevai's success envelope `{ code, data: { result: { answers, usage, … } } }` before reading `answers.*` (stock expects a flat `{ answers }` body and crashes with `Cannot read properties of undefined (reading 'result')`).

## Cursor Cloud Agents (any repo)

Cloud agents **do not** read `~/.cursor/mcp.json` on the VM. Configure once at [cursor.com/agents](https://cursor.com/agents) → MCP → Add / Custom:

| Field | Value |
| --- | --- |
| Type | stdio |
| Name | `jev` (or `jev-mcp`) |
| Command | `npx` |
| Args | `-y` `github:abaljeu/jev-mcp` |
| Env | `TYPESAFE_API_KEY` = your `sk_…` key |
| Env | `JEV_BASE_URL` = `https://thejevai.com/v1/systemone` |

Enable it for Cloud. **Start a new** cloud agent after saving (existing runs keep the old MCP list).

For hosted `jv_live_…` keys, omit `JEV_BASE_URL` or set it to `https://jevtypesafeai.com/api/v1/decide`.

## Local / Grok Bot box

```bash
TYPESAFE_API_KEY=sk_… npx -y github:abaljeu/jev-mcp
```

## Tools

`jev_classify`, `jev_score`, `jev_check`, `jev_gate`, `jev_decide`
