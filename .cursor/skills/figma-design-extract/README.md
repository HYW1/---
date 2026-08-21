# figma-design-extract

> Get the real design out of Figma — exact tokens, sizes, and structure — into a build-ready spec table, instead of eyeballing a screenshot.

This is the **first** of two composable skills. It reads a Figma node via the Figma MCP and produces a **design-spec table** (`element | property | exact value | repo token | source component`) that becomes your build contract — and the input to [`design-fidelity-verify`](../design-fidelity-verify), which proves the running app matches it.

## What it does

- Resolves the Figma node (handles stale ids, dark-mode mirror pages, token cost).
- Reads **structured values**, not pixels: `get_variable_defs` (tokens = source of truth), `get_metadata` (sizes/positions), `get_design_context` (structure/auto-layout only), `get_screenshot` (visual reference only — never measured). Reaches for `search_design_system` before concluding no token exists, and `use_figma` (read-only) for unbound gradients that `get_variable_defs` won't return.
- Maps each Figma variable to **your** design-token system, audits existing components for reuse, and logs design-system drift instead of hardcoding.
- Converts `letterSpacing` from Figma's **percent** before it reaches the table — `-2` means `-0.02em`, not `-2px`, and reading it literally makes every downstream verify report a false PASS.

## Requirements

- The **Figma MCP server** (Dev Mode MCP) connected in your client.
- A frontend repo with some design-token system (Tailwind/NativeWind/Restyle/CSS variables — all shown as adaptable examples).

## Use it

Share a `figma.com/...node-id=...` URL or say "implement this Figma component", "extract the Figma values", or "match the Figma". See [`SKILL.md`](SKILL.md) for the full workflow and [`examples/worked-example.md`](examples/worked-example.md) for a concrete run.

This is the **design→code** direction. To push code *into* Figma, use Figma's own `figma-generate-design` skill instead — it ships with the [Figma MCP server](https://developers.figma.com/docs/figma-mcp-server/). The two are complements, not competitors.

> **Tip:** Figma recommends locking the workflow in by adding a `# Figma MCP` rules block to your project's agent rules (`CLAUDE.md` / `AGENTS.md`) — see [Figma's custom-rules docs](https://developers.figma.com/docs/figma-mcp-server/add-custom-rules/).
