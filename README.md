# shadcn-cursor-rules

The official [shadcn/ui](https://ui.shadcn.com) skill, converted to a Cursor rule. Drop the `.cursor/` directory into any project to give Cursor's agent shadcn component knowledge, composition rules, and CLI workflow.

## What's here

```
.cursor/rules/
  shadcn.mdc                     # main rule (agent-decided)
  shadcn-reference/              # verbatim reference docs the rule links to
    base-vs-radix.md
    cli.md
    composition.md
    customization.md
    forms.md
    icons.md
    mcp.md
    registry.md
    styling.md
```

## Activation

`shadcn.mdc` uses `alwaysApply: false` with a `description`, so Cursor's agent loads it when the task involves shadcn/ui, a `components.json` project, registries, or `--preset` codes. It stays out of unrelated work.

## What changed from the source skill

This is adapted, not copied. The upstream skill is a Claude Code skill; two pieces don't work in Cursor and were changed:

- **`allowed-tools` frontmatter dropped.** That field is Claude-Code-only. The CLI commands the rule references (`npx shadcn@latest ...`) are unchanged — the agent runs them in your project as normal.
- **Auto-injected project context rewritten as a manual step.** The source skill embedded a command that Claude Code auto-executes to inject `components.json` context. Cursor has no equivalent, so the rule now instructs you to run `npx shadcn@latest info --json` yourself and use the output as source of truth.

The skill's own guardrails are preserved verbatim: never `--overwrite` without approval, never guess a registry, always confirm before destructive preset switches, always review added component files.

The `shadcn-reference/` files are exact copies from the source skill (Incorrect/Correct code pairs and CLI reference), with only intra-repo relative links adjusted to resolve in this folder layout. Links in `shadcn.mdc` resolve to them.

## Source & license

This Cursor rule adapts material from [shadcn-ui/ui → skills/shadcn](https://github.com/shadcn-ui/ui/tree/main/skills/shadcn). The upstream project is MIT licensed; see [LICENSE](LICENSE) for the preserved upstream license and copyright notice.

The underlying shadcn documentation and skill content are the work of the shadcn/ui authors. Only the Cursor packaging and the adaptations described above are maintained by Michael McCollough ([Sciontut](https://github.com/Sciontut)). Component knowledge tracks the upstream skill at the time of conversion; for the latest, re-pull from source.
