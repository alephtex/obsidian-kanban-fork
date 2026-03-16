AGENTS.md

Project: Obsidian Kanban Plugin - Fork with Escape Key Save Behavior
Framework: TypeScript, React (Preact), Obsidian API
Build Tool: esbuild

## Fork Modifications

### Escape Key Behavior Changes
This fork modifies the Escape key behavior to **save edits instead of canceling them**:

**Modified Files:**
- `src/components/Item/ItemContent.tsx` - Escape key saves card edits
- `src/components/Item/ItemForm.tsx` - Escape key and click-outside save new cards
- `src/components/Lane/LaneTitle.tsx` - Escape key saves lane title edits
- `src/components/Lane/LaneForm.tsx` - Escape key creates new lane

**Behavior Changes:**
- **Escape key**: Now saves changes instead of canceling them
- **Click outside**: Now saves changes (for item form) instead of discarding them
- **Enter key**: Continues to save changes (when not allowing new lines)

**Documentation:**
- `ESCAPE_KEY_CHANGES.md` - Detailed documentation of all changes

## 1. Build, Lint, and Test Commands

All commands are run via `yarn` or `npm` (preferring `yarn` as per lockfile).

**Build & Development**
- `yarn dev`: Start development build (watch mode).
- `yarn build`: Production build (outputs to `main.js`).
- `yarn typecheck`: Run TypeScript compiler to check types without emitting files.

**Code Quality & Formatting**
- `yarn lint`: Check for linting errors using ESLint.
- `yarn lint:fix`: Automatically fix linting errors.
- `yarn prettier`: Format code using Prettier.
- `yarn clean`: Run Prettier then ESLint fix (pre-commit hook equivalent).

**Testing**
- **Note:** The repository does not appear to have a test runner configured in `package.json`.
- To run specific tests (if added), use the relevant test runner command (e.g., `jest` or `vitest`).
- If a test file is found (e.g., `*.test.ts`), run it using the installed test runner.

**Release**
- `yarn bump`: Bump version and update manifest.
- `yarn release`: Commit, tag, and push the release.

## 2. Code Style Guidelines

### Imports & Sorting
- **Prettier Plugin**: Uses `@trivago/prettier-plugin-sort-imports`.
- **Order**: Imports are sorted with `importOrder: ['^[./]']` (internal imports first, then external).
- **Separation**: Blank lines separate import groups.
- **Aliases**: Imports from `src/*` are preferred over relative paths like `../../`.

### Formatting
- **Standard**: Prettier config in `prettier.config.cjs`.
- **Quotes**: Single quotes for TS/JS, double for JSX.
- **Semicolons**: Always included.
- **Indentation**: 2 spaces.
- **Line Length**: 100 characters.
- **Trailing Commas**: ES5 style.

### Types & TypeScript
- **Strictness**: `noImplicitAny: true`.
- **JSX**: Enabled with `react-jsx` mode.
- **Target**: ES2018.
- **Paths**: Aliases configured for `react` and `react-dom` to use Preact compatibility layer.
- **Avoid**: `any` types where possible (though lint rule `@typescript-eslint/no-explicit-any` is currently `off`).

### React / Preact Components
- **Naming**: PascalCase for components.
- **Hooks**: Follow standard React hooks rules.
- **State**: Immutability preferred (uses `immutability-helper`).
- **Styling**: CSS/LESS modules or standard CSS (check component implementation).

### Error Handling
- **Async/Await**: Enforce `await-thenable` lint rule.
- **General**: Use try/catch for Obsidian API calls or file operations.

### Negative Space Programming (Defensive Programming)
**CRITICAL**: Always use Negative Space Programming patterns. Do not write "Happy Path" code without first asserting the state of reality.

**The Pattern:**
1. **Define Negative Space** (Invalid States) at the start of every function
2. **Assert Early, Crash Loudly** - Check all inputs and invariants
3. **Eliminate Ambiguity** - Never assume variables "should" be there

**Examples:**
```typescript
// Bad (Vibe Coding - NOT ACCEPTABLE):
function processPayment(amount) {
  return api.charge(amount);
}

// Good (Negative Space - REQUIRED):
function processPayment(amount) {
  // 1. Define Negative Space (Invalid States)
  if (typeof amount !== 'number') throw new Error("Payment amount must be a number");
  if (amount <= 0) throw new Error("Payment amount must be positive");

  // 2. Run Logic (Guaranteed Valid State)
  return api.charge(amount);
}
```

**Goal:** Your code should fail INSTANTLY at the source of the error, rather than propagating `undefined`, `null`, or `NaN` downstream.

### File Structure
- Source code resides in `src/`.
- Avoid modifying files in `docs/` (documentation) or `.obsidian/` (workspace configs).

### Git Workflow
- Commit messages are version-tagged during release (`yarn release`).
- No specific commit hook mentioned, but `yarn clean` is recommended pre-commit.

## 3. Environment & Configuration
- **Node.js**: Required (version defined in `.nvmrc` or package engines if present).
- **Obsidian**: Requires Obsidian v1.0.0+.
- **VSCode**: Recommended extensions configured in `.vscode/extensions.json`.

## 4. Obsidian API & Development Best Practices (2025/2026)

### Official Resources
- **Obsidian Developer Documentation**: https://docs.obsidian.md
- **API Reference**: https://docs.obsidian.md/Reference/TypeScript+API
- **Sample Plugin**: https://github.com/obsidianmd/obsidian-sample-plugin (official template)

### Latest API Changes & Features
- **React/Preact Support**: Officially supported. Use `jsxImportSource: "preact"` in tsconfig.json.
- **Mobile Compatibility**: Ensure plugins work on mobile by testing touch events and mobile-specific APIs.
- **Settings Storage**: Use `this.settings` object saved via `saveSettings()` method.
- **Vault API**: Use `app.vault` for file operations. New methods include `appendBinary()` for binary file handling.
- **Plugin Lifecycle**: Implement `onload()` for initialization and `onunload()` for cleanup.

### Development Recommendations
1. **Use Official Template**: Start with `obsidianmd/obsidian-sample-plugin` for latest configurations
2. **TypeScript First**: All modern plugins use TypeScript for type safety
3. **Preact for UI**: Lightweight React alternative recommended for plugin UIs
4. **Mobile Testing**: Test on mobile devices early in development
5. **Community Guidelines**: Follow plugin guidelines at https://docs.obsidian.md/Plugins/Releasing/Plugin+guidelines

### Breaking Changes (Recent)
- **BaseOption#shouldHide**: Function signature changed (no longer receives config argument)
- **API Stability**: Obsidian API is stable but check changelog for updates

### Recommended Dependencies
- `obsidian`: Latest plugin API types
- `preact`: For React-compatible UI components
- `@types/node`: For Node.js type definitions
- TypeScript 5.x for latest features

### Debugging Tips
- Use `console.log()` for debugging (visible in developer console)
- Enable developer mode in Obsidian (Ctrl+Shift+I or Cmd+Option+I)
- Check plugin logs in `.obsidian/plugins/[plugin-id]/` directory
