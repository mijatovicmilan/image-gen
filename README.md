# image-gen

A Claude Code skill that generates or edits images by handing your prompt to the
[Codex CLI](https://github.com/openai/codex) and its built-in `$imagegen` skill.
Claude shows you the resulting images in chat.

## Requirements

- [Claude Code](https://claude.com/claude-code)
- [Codex CLI](https://github.com/openai/codex), installed and logged in (`codex login`).
  The skill runs `codex exec`, so check that works in your terminal first.

## Install

Pick one.

**As a plain skill** (via [skills.sh](https://skills.sh)):

```bash
npx skills add mijatovicmilan/image-gen
```

Then use `/image-gen`.

**As a Claude Code plugin** (gets updates through the plugin system):

```bash
claude plugin marketplace add mijatovicmilan/image-gen
claude plugin install image-gen@image-gen
```

Then use `/image-gen:image-gen`.

## Usage

```
/image-gen a watercolor fox sleeping under a pine tree
```

To edit an image or use one as a reference, mention its path in your request:

```
/image-gen make the sky in ~/Desktop/photo.png a sunset
```

Images stay where Codex saves them. Ask Claude to copy them somewhere if you want
them in a project.

You don't need to type the command: asking Claude to "generate an image of…" also
triggers the skill.

## Layout

```
.claude-plugin/
  marketplace.json   # makes this repo a plugin marketplace
  plugin.json        # plugin metadata and version
skills/
  image-gen/
    SKILL.md         # the skill itself
```

## License

MIT
