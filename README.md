# Mindmap Plugin for Claude

Generates structured mindmap JSON files with a node-graph layout on `/mindmap` command.

## Install (Claude Code)

```bash
cp -r .claude-plugin/ ~/.claude/plugins/mindmap/
```

## Usage

```
/mindmap Machine Learning
/mindmap World War 2
/mindmap My Startup Idea
```

Claude outputs JSON matching the node-graph schema with:
- Nodes: id, text, x/y coordinates, color, notes, image_path, important
- Edges: id, src, dst, label
- Radial tree layout (no overlapping nodes)

## Community Marketplace

```bash
/plugin marketplace add anthropics/claude-plugins-community
/plugin install mindmap@claude-community
```

## Submit to Official Directory

1. Push this repo to GitHub (public)
2. Run: claude plugin validate ./
3. Submit at: claude.com/resources/articles/build-plugins-for-claude
