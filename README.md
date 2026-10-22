# Mindmap Plugin for Claude

Generates structured mindmap JSON files with a node-graph layout on `/mindmap` command.

## Install

```bash
/plugin marketplace add gwimm67/mindmaplite
/plugin install mindmap@mindmaplite
```

## Usage

```
/mindmap Machine Learning
/mindmap World War 2
/mindmap My Startup Idea
```

Claude outputs JSON with:
- Nodes: `id`, `text`, `x/y` coords, `color`, `notes`, `image_path`, `important`
- Edges: `id`, `src`, `dst`, `label`
- Radial tree layout, no overlapping nodes

## Submit to Official Directory

1. `claude plugin validate ./`
2. Submit at: https://claude.com/resources/articles/build-plugins-for-claude

## License

MIT
