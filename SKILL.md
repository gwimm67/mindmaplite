# Mindmap JSON Generator

## When to use
Activate when the user runs `/mindmap <topic>` or asks to create a mindmap.

## What you do
Generate a structured mindmap as a JSON file matching the exact schema below. Never output plain bullet notes, markdown lists, or prose outlines — always output the JSON.

---

## JSON Schema

```json
{
  "name": "<mindmap title>",
  "nodes": [
    {
      "id": "<8-char hex string>",
      "text": "<node label>",
      "x": <float>,
      "y": <float>,
      "color": "#3b6ea5",
      "notes": "<optional detail string, empty string if none>",
      "image_path": null,
      "important": false
    }
  ],
  "edges": [
    {
      "id": "<8-char hex string>",
      "src": "<source node id>",
      "dst": "<destination node id>",
      "label": ""
    }
  ],
  "background": null
}
```

---

## Layout Rules

### Node positioning (x, y)
Use a radial/tree layout. The root node always sits near center.

**Root node:** x: 400, y: 100

**First-level children:** spread horizontally below the root.
- Spacing between siblings: 220px horizontally
- Drop 160px below parent (y + 160)
- Center the row: start_x = 400 - ((count - 1) * 220 / 2)

**Second-level children:** same logic, drop another 160px below their parent.

**Example for 3 first-level children:**
- child 1: x: 180, y: 260
- child 2: x: 400, y: 260
- child 3: x: 620, y: 260

### Node color
Always `"#3b6ea5"` unless the user specifies a different color.

### IDs
Generate random 8-character lowercase hex strings for every node and edge. They must be unique within the file.

### Edges
Connect parent → child with a directed edge. Root connects to all first-level children. First-level nodes connect to their own children.

### Notes field
If a node has meaningful detail worth adding, put it in `"notes"`. Otherwise leave it as `""`.

---

## Output format

Output the JSON inside a code block tagged `json`. Then below it, write a single short line describing the map (e.g. "7-node mindmap on [topic], root → 3 branches").

Do NOT output:
- Bullet point outlines
- Markdown headers as a substitute
- Prose explanations before the JSON
- Any disclaimer or preamble

---

## Example

User: `/mindmap Machine Learning`

Output:

```json
{
  "name": "Machine Learning",
  "nodes": [
    {
      "id": "a1b2c3d4",
      "text": "Machine Learning",
      "x": 400.0,
      "y": 100.0,
      "color": "#3b6ea5",
      "notes": "",
      "image_path": null,
      "important": false
    },
    {
      "id": "e5f6a7b8",
      "text": "Supervised",
      "x": 180.0,
      "y": 260.0,
      "color": "#3b6ea5",
      "notes": "Labeled training data",
      "image_path": null,
      "important": false
    },
    {
      "id": "c9d0e1f2",
      "text": "Unsupervised",
      "x": 400.0,
      "y": 260.0,
      "color": "#3b6ea5",
      "notes": "No labels, finds patterns",
      "image_path": null,
      "important": false
    },
    {
      "id": "a3b4c5d6",
      "text": "Reinforcement",
      "x": 620.0,
      "y": 260.0,
      "color": "#3b6ea5",
      "notes": "Reward-based learning",
      "image_path": null,
      "important": false
    },
    {
      "id": "e7f8a9b0",
      "text": "Regression",
      "x": 70.0,
      "y": 420.0,
      "color": "#3b6ea5",
      "notes": "",
      "image_path": null,
      "important": false
    },
    {
      "id": "c1d2e3f4",
      "text": "Classification",
      "x": 290.0,
      "y": 420.0,
      "color": "#3b6ea5",
      "notes": "",
      "image_path": null,
      "important": false
    }
  ],
  "edges": [
    { "id": "aa11bb22", "src": "a1b2c3d4", "dst": "e5f6a7b8", "label": "" },
    { "id": "cc33dd44", "src": "a1b2c3d4", "dst": "c9d0e1f2", "label": "" },
    { "id": "ee55ff66", "src": "a1b2c3d4", "dst": "a3b4c5d6", "label": "" },
    { "id": "gg77hh88", "src": "e5f6a7b8", "dst": "e7f8a9b0", "label": "" },
    { "id": "ii99jj00", "src": "e5f6a7b8", "dst": "c1d2e3f4", "label": "" }
  ],
  "background": null
}
```

6-node mindmap on Machine Learning, root → 3 branches → 2 sub-nodes under Supervised.
