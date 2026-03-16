# Obsidian Kanban Plugin - Fork with Escape Key Save Behavior

**This is a fork of the original Obsidian Kanban plugin with modified Escape key behavior.**

---

## Changes in This Fork

This fork modifies the Escape key behavior to **save edits instead of canceling them**:

### Modified Behavior:
- **Escape key**: Now saves changes instead of canceling them
- **Click outside**: Now saves changes (for item form) instead of discarding them
- **Enter key**: Continues to save changes (when not allowing new lines)

### Files Modified:
- `src/components/Item/ItemContent.tsx` - Escape key saves card edits
- `src/components/Item/ItemForm.tsx` - Escape key and click-outside save new cards
- `src/components/Lane/LaneTitle.tsx` - Escape key saves lane title edits
- `src/components/Lane/LaneForm.tsx` - Escape key creates new lane

### Documentation:
- `ESCAPE_KEY_CHANGES.md` - Detailed documentation of all changes
- `AGENTS.md` - Project documentation with build commands

---

## Original Plugin Documentation

Create markdown-backed Kanban boards in [Obsidian](https://obsidian.md/)

- [Bugs, Issues, & Feature Requests](https://github.com/mgmeyers/obsidian-kanban/issues)
- [Development Roadmap](https://github.com/mgmeyers/obsidian-kanban/projects/1)

![Screen Shot 2021-09-16 at 12.58.22 PM.png](https://github.com/mgmeyers/obsidian-kanban/blob/main/docs/Assets/Screen%20Shot%202021-09-16%20at%2012.58.22%20PM.png)

![Screen Shot 2021-09-16 at 1.10.38 PM.png](https://github.com/mgmeyers/obsidian-kanban/blob/main/docs/Assets/Screen%20Shot%202021-09-16%20at%201.10.38%20PM.png)

## Documentation

Find the plugin documentation here: [Obsidian Kanban Plugin Documentation](https://publish.obsidian.md/kanban/)

## Building from Source

1. Clone this repository
2. Install dependencies: `npm install` or `yarn install`
3. Build the plugin: `npm run build`
4. Copy `main.js` to your Obsidian plugins folder

## License

MIT License - See LICENSE.md for details
