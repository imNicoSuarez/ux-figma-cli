# UX Claude

<p align="center">
  <a href="https://intodesignsystems.com"><img src="https://img.shields.io/badge/Into_Design_Systems-intodesignsystems.com-ff6b35" alt="Into Design Systems"></a>
  <img src="https://img.shields.io/badge/Figma-Desktop-purple" alt="Figma Desktop">
  <img src="https://img.shields.io/badge/No_API_Key-Required-green" alt="No API Key">
  <img src="https://img.shields.io/badge/Claude_Code-Ready-blue" alt="Claude Code">
</p>

<p align="center">
  <b>Control Figma Desktop with Claude Code.</b><br>
  Full read/write access. No API key required.<br>
  Just talk to Claude about your designs.
</p>

```
  ██╗   ██╗██╗  ██╗     ██████╗██╗      █████╗ ██╗   ██╗██████╗ ███████╗
  ██║   ██║╚██╗██╔╝    ██╔════╝██║     ██╔══██╗██║   ██║██╔══██╗██╔════╝
  ██║   ██║ ╚███╔╝     ██║     ██║     ███████║██║   ██║██║  ██║█████╗
  ██║   ██║ ██╔██╗     ██║     ██║     ██╔══██║██║   ██║██║  ██║██╔══╝
  ╚██████╔╝██╔╝ ██╗    ╚██████╗███████╗██║  ██║╚██████╔╝██████╔╝███████╗
   ╚═════╝ ╚═╝  ╚═╝     ╚═════╝╚══════╝╚═╝  ╚═╝ ╚═════╝ ╚═════╝╚══════╝
```

## What is This?

A CLI that connects directly to Figma Desktop and gives you complete control:

- **shadcn/ui Components** — Generate all 30 official shadcn components with real Lucide icons and variable binding
- **Blocks** — Pre-built UI layouts (dashboards, pages) with one command
- **Design Tokens** — Create variables, collections, modes (Light/Dark), bind to nodes
- **Create Anything** — Frames, text, shapes, icons (150k+ from Iconify), components
- **Slots** — Create and manage Figma's new Slots feature for flexible component content
- **Team Libraries** — Import and use components, styles, variables from any library
- **Analyze Designs** — Colors, typography, spacing, find repeated patterns
- **Lint & Accessibility** — Contrast checker, touch targets, design rules
- **Export** — PNG, SVG, JSX, Storybook stories, CSS variables, Tailwind config
- **Batch Operations** — Rename layers, find/replace text, create 100 variables at once
- **Works with Claude Code** — Just ask in natural language, Claude knows all commands

---

## shadcn/ui Component Package

Generate production-ready shadcn/ui components directly in Figma. All 30 components with 58 variants, matching the official shadcn/ui specs.

### Quick Start

```bash
# 1. Add shadcn design tokens (Light/Dark mode)
node src/index.js tokens preset shadcn

# 2. Generate all components
node src/index.js shadcn add --all

# Or pick specific ones
node src/index.js shadcn add button card input tabs

# List available components
node src/index.js shadcn list
```

### What You Get

**30 components, 58 variants:**

| Component | Variants |
|-----------|----------|
| Button | Default, Secondary, Destructive, Outline, Ghost, Link, Small, Large, Icon |
| Badge | Default, Secondary, Destructive, Outline |
| Card | Full card with Header, Content, Footer |
| Input | Default, Filled, With Label |
| Textarea | Default |
| Label | Default |
| Alert | Default (info icon), Destructive (alert icon) |
| Avatar | Default, Small |
| Switch | On, Off |
| Separator | Horizontal, Vertical |
| Skeleton | Text, Circle, Card |
| Progress | 60%, 30% |
| Toggle | Default, Active |
| Checkbox | Unchecked, Checked (with check icon) |
| Tabs | Full tabs with content panel |
| Table | Header + 3 rows |
| Radio Group | Unchecked, Checked, Full group |
| Select | Closed, Filled, Open (with dropdown + check icon) |
| Slider | With thumb |
| Breadcrumb | With chevron separators |
| Pagination | With chevron + ellipsis icons |
| Kbd | Single key, Key combo |
| Spinner | Small, Medium |
| Tooltip | Tooltip + trigger |
| Dialog | With close button, form fields |
| Dropdown Menu | With items + separator |
| Accordion | Open + collapsed items |
| Navigation Menu | Active + inactive items |
| Sheet | Side panel with form |
| Hover Card | Profile card |

### Real Lucide Icons

Components use actual Lucide SVG icons (not placeholder shapes), fetched from the Iconify API and rendered as vector nodes in Figma:

- **Pagination**: chevron-left, chevron-right, ellipsis
- **Select**: chevron-down, chevron-up, check
- **Accordion**: chevron-down, chevron-right
- **Checkbox**: check
- **Dialog/Sheet**: x (close button)
- **Alert**: info, alert-circle
- **Button/Icon**: plus
- **Toggle**: bold
- **Breadcrumb**: chevron-right
- **Navigation Menu**: chevron-down

### Design Token Integration

All components use `var:` syntax to bind directly to shadcn variables. When you add tokens with `tokens preset shadcn`, components automatically use your Light/Dark mode colors:

- `background`, `foreground` — page background/text
- `card`, `card-foreground` — card backgrounds
- `primary`, `primary-foreground` — buttons, accents
- `secondary`, `secondary-foreground` — secondary actions
- `muted`, `muted-foreground` — subtle text, disabled states
- `accent`, `accent-foreground` — hover states
- `destructive`, `destructive-foreground` — error states
- `border`, `input`, `ring` — borders, inputs, focus rings

---

## Blocks (Pre-built UI Layouts)

Use `blocks create` for dashboards and full page layouts — much faster than building manually with render/eval.

```bash
# List available blocks
node src/index.js blocks list

# Create a full analytics dashboard
node src/index.js blocks create dashboard-01
```

### dashboard-01

A complete analytics dashboard including:

- Sidebar with real Lucide icons
- Stats cards (Revenue, Customers, Accounts, Growth)
- Area chart with two datasets
- Data table with pagination
- All colors bound to shadcn variables (Light/Dark mode ready)

**Dark mode copy:** After creating, clone and switch mode via eval:

```javascript
var clone = dashboard.clone();
clone.name = 'Dashboard (Dark)';
clone.setExplicitVariableModeForCollection(semanticCollection, darkModeId);
```

---

## AI Verification

After creating any component, run `verify` to capture a screenshot for visual validation:

```bash
node src/index.js verify              # Screenshot of current selection
node src/index.js verify "123:456"    # Screenshot of specific node
```

Returns JSON with a base64 image (max 2000px, auto-scaled). Always verify after `render`, `render-batch`, or `node to-component`.

---

## Slots

Figma's native Slots feature lets designers add, remove, and reorder content in component instances without detaching.

### Commands

```bash
# Create slot on selected component
node src/index.js slot create "Content" --flex col --gap 8 --padding 16

# List slots in a component
node src/index.js slot list
node src/index.js slot list "component-id"

# Convert an existing frame to a slot (must be inside a component)
node src/index.js slot convert --name "Actions"

# Set preferred components for a slot
node src/index.js slot preferred "Slot#1:2" "component-id-1" "component-id-2"

# Add content to a slot in an instance
node src/index.js slot add "slot-id" --component "component-id"
node src/index.js slot add "slot-id" --frame
node src/index.js slot add "slot-id" --text "Hello"

# Reset slot in instance to defaults
node src/index.js slot reset
node src/index.js slot reset "slot-node-id"
```

### JSX Slot Syntax

```jsx
<Frame name="Card" w={300} bg="#18181b" rounded={12} flex="col" p={16} gap={12}>
  <Text size={18} weight="bold" color="#fff">Card Title</Text>
  <Slot name="Content" flex="col" gap={8} w="fill">
    <Text size={14} color="#a1a1aa">Default slot content</Text>
  </Slot>
  <Slot name="Actions" flex="row" gap={8} />
</Frame>
```

> **Critical:** Setting `frame.isSlot = true` directly in eval does **not** create a slot. Always use `slot convert` or the JSX `<Slot>` element.

---

## Why This CLI?

This project includes a `CLAUDE.md` file that Claude reads automatically. It contains:

- All available commands and their syntax
- Best practices (e.g., "use `render` for text-heavy designs")
- Common requests mapped to solutions

**Want to teach Claude new tricks?** Just update `CLAUDE.md`. No code changes needed.

**Example:** You type "Create Tailwind colors" -> Claude already knows to run `node src/index.js tokens tailwind` because it's documented in `CLAUDE.md`.

---

## What You Need

- **Node.js 18+** — `brew install node` (or [download](https://nodejs.org/))
- **Figma Desktop** (free account works)
- **Claude Code** ([get it here](https://www.anthropic.com/claude-code))
- **macOS or Windows** (macOS recommended, Windows supported)

---

## Setup

```bash
git clone https://github.com/silships/ux-figma-cli.git
cd ux-figma-cli
npm install
npm run setup-alias
source ~/.zshrc
```

That's it. Now open a **new terminal** and type:

```bash
uxclaude
```

This will:
1. Start Figma (if not running)
2. Connect to Figma via the UX Claude plugin
3. Show your open Figma files: pick one with arrow keys
4. Launch Claude Code with all commands pre-loaded

**Done.** Talk to Claude about your Figma file.

> **Note:** `uxclaude` works from any directory. The setup script saves the repo location to `~/.uxclaude/config.json`.

### uxclaude Options

| Command | Description |
|---------|-------------|
| `uxclaude` | Interactive file picker, connects via plugin |
| `uxclaude --setup` | Update the path to the ux-figma-cli repo |

### Manual Setup (without uxclaude)

```bash
cd figma-cli
claude
```

Then tell Claude: `Connect to Figma`

---

## Using It

Once connected, just talk to Claude:

> "Add shadcn colors to my project"

> "Add all shadcn components"

> "Add a card component with button and input"

> "Check accessibility"

> "Export variables as CSS"

The included `CLAUDE.md` teaches Claude all commands automatically. No manual required.

**Each session:** Start the UX Claude plugin in Figma before running `uxclaude`.

---

## JSX Rendering with Icons

The CLI includes a JSX-like syntax for creating complex layouts. Icons are rendered as real SVG vectors:

```jsx
// Real Lucide icons in JSX
<Frame name="Nav" flex="row" items="center" gap={8} bg="var:card" p={12} rounded={8}>
  <Icon name="lucide:home" size={20} color="var:foreground" />
  <Text size={14} weight="medium" color="var:foreground">Home</Text>
  <Frame grow={1} />
  <Icon name="lucide:settings" size={20} color="var:muted-foreground" />
</Frame>
```

Icons support:
- Any icon from [Lucide](https://lucide.dev/icons) (2000+ icons)
- Any icon set on [Iconify](https://iconify.design/) (150,000+ icons): `mdi:home`, `heroicons:star`, etc.
- Variable color binding with `var:` syntax
- Custom sizes

---

## How to Connect

UX Claude uses a Figma plugin to communicate. No Figma patching or Full Disk Access required.

```
┌─────────────┐     WebSocket     ┌─────────────┐     Plugin API     ┌─────────────┐
│     CLI     │ <---------------> │   Daemon    │ <----------------> │   Plugin    │
└─────────────┘   localhost:3456  └─────────────┘                    └─────────────┘
```

**Step 1:** Import plugin (one-time only)
1. In Figma: **Plugins -> Development -> Import plugin from manifest**
2. Select `plugin/manifest.json` from this project
3. Click **Open**

**Step 2:** Start the plugin (each session)
1. In Figma: **Plugins -> Development -> UX Claude**
2. Terminal shows: `Plugin connected!`

**Tip:** Right-click the plugin -> **Add to toolbar** for quick access.

**Step 3:** Run
```bash
uxclaude
```

---

## Troubleshooting

### Plugin Not Connecting

1. Make sure the **UX Claude plugin is running** in Figma (Plugins -> Development -> UX Claude)
2. Make sure you have a **design file open** in Figma (not just the home screen)
3. Restart the daemon: `node src/index.js daemon restart`
4. Run connect again: `node src/index.js connect`

### Windows

Windows is supported but less tested than macOS.

**Figma Location:** The CLI expects Figma at `%LOCALAPPDATA%\Figma\Figma.exe` (default install location).

---

## Updating

```bash
cd ~/path/to/ux-figma-cli
git pull
npm install
```

## How It Works

Connects to Figma Desktop via the UX Claude plugin. No API key needed — it uses your existing Figma session.

```
┌─────────────┐     WebSocket     ┌─────────────┐     Plugin API     ┌─────────────┐
│   uxclaude  │ <---------------> │   Daemon    │ <----------------> │   Plugin    │
│    (CLI)    │   localhost:3456  └─────────────┘                    │  (Figma)    │
└─────────────┘                                                       └─────────────┘
```

### Security

The CLI runs a local daemon for faster command execution. Security features:

- **Session token authentication**: Random 32-byte token required for all requests
- **No CORS headers**: Blocks cross-origin browser requests
- **Host header validation**: Only accepts localhost/127.0.0.1
- **Idle timeout**: Auto-shutdown after 10 minutes of inactivity (configurable)

Token is stored at `~/.uxclaude/.daemon-token` with owner-only permissions (0600).

---

## Full Feature List

### shadcn/ui Components

- **30 components, 58 variants** matching official shadcn/ui specs
- Real **Lucide SVG icons** (chevrons, check, x, plus, info, alert-circle, bold, ellipsis)
- **Design token binding** via `var:` syntax (auto-binds to shadcn Light/Dark mode variables)
- Components: Button (9), Badge (4), Card, Input (3), Textarea, Label, Alert (2), Avatar (2), Switch (2), Separator (2), Skeleton (3), Progress (2), Toggle (2), Checkbox (2), Tabs, Table, Radio Group (3), Select (3), Slider, Breadcrumb, Pagination, Kbd (2), Spinner (2), Tooltip, Dialog, Dropdown Menu, Accordion, Navigation Menu, Sheet, Hover Card

### Design Tokens & Variables

- **Color presets** -- shadcn (276 vars with Light/Dark mode), Radix UI (156 vars)
- Create Tailwind CSS color palettes (all 22 color families, 50-950 shades)
- Create and manage variable collections
- **Variable modes** (Light/Dark/Mobile) with per-mode values
- **Batch create** up to 100 variables at once
- **Batch update** variable values across modes
- Bind variables to node properties (fill, stroke, gap, padding, radius)
- Export variables as CSS custom properties
- Export variables as Tailwind config

### Create Elements

- Frames with auto-layout
- Rectangles, circles, ellipses
- Text with custom fonts, sizes, weights
- Lines
- Icons (150,000+ from Iconify: Lucide, Material Design, Heroicons, etc.)
- Groups
- Components from frames
- Component instances
- **Component sets with variants**

### JSX Rendering

- **JSX-like syntax** for complex layouts (`<Frame>`, `<Text>`, `<Icon>`, `<Slot>`)
- **Real Lucide/Iconify icons** rendered as SVG vectors (not placeholders)
- **Variable binding** with `var:name` syntax for fills, strokes, text colors, icon colors
- Auto-layout props: `flex`, `gap`, `p`/`px`/`py`, `justify`, `items`, `grow`, `wrap`
- Sizing: `w`/`h` (fixed), `w="fill"` (stretch), auto-hug
- Appearance: `bg`, `stroke`, `strokeWidth`, `strokeAlign`, `rounded`, `shadow`, `opacity`, `overflow`
- **Slots** for component content areas (`slot create`, `slot convert`, `slot add`, `slot preferred`, `slot reset`)

### Modify Elements

- Change fill and stroke colors
- Set corner radius
- Resize and move
- Apply auto-layout (row/column, gap, padding)
- Set sizing mode (hug/fill/fixed)
- Rename nodes
- Duplicate nodes
- Delete nodes
- **Flip nodes** (horizontal/vertical)
- **Scale vectors**

### Find & Select

- Find nodes by name
- Find nodes by type (FRAME, COMPONENT, TEXT, etc.)
- **XPath-like queries** (`//FRAME[@width > 300]`)
- Select nodes by ID
- Get node properties
- Get node tree structure

### Canvas Operations

- List all nodes on canvas
- Arrange frames in grid or column
- Delete all nodes
- Zoom to fit content
- Smart positioning (auto-place without overlaps)

### Export

- **Export node by ID** (`export node "1:234" -s 2 -f png`)
- Export nodes as PNG (with scale factor)
- Export nodes as SVG
- **Export multiple sizes** (@1x, @2x, @3x)
- Take screenshots
- **Export to JSX** (React code)
- **Export to Storybook** stories
- Export variables as CSS
- Export variables as Tailwind config

### FigJam Support

- Create sticky notes
- Create shapes with text
- Connect elements with arrows
- List FigJam elements
- Run JavaScript in FigJam context

### Team Libraries

- List available library variable collections
- Import variables from libraries
- Import components from libraries
- Create instances of library components
- Import and apply library styles (color, text, effect)
- Bind library variables to node properties
- Swap component instances to different library components
- List all enabled libraries

### Designer Utilities

- **Batch rename layers** (with patterns: {n}, {name}, {type})
- **Case conversion** (camelCase, PascalCase, snake_case, kebab-case)
- **Lorem ipsum generator** (words, sentences, paragraphs)
- **Fill text with placeholder content**
- **Insert images from URL**
- **Unsplash integration** (random stock photos by keyword)
- **Contrast checker** (WCAG AA/AAA compliance)
- **Check text contrast** against background
- **Find and replace text** across all layers
- **Select same** (fill, stroke, font, size)
- **Color blindness simulation** (deuteranopia, protanopia, tritanopia)

### Query & Analysis

- **Analyze colors** -- usage frequency, variable bindings
- **Analyze typography** -- all font combinations used
- **Analyze spacing** -- gap/padding values, grid compliance
- **Find clusters** -- detect repeated patterns (potential components)
- **Visual diff** -- compare two nodes
- **Create diff patch** -- structural patches between versions

### Lint & Accessibility

- **Design linting** with 8+ rules:
  - `no-default-names` -- detect unnamed layers
  - `no-deeply-nested` -- flag excessive nesting
  - `no-empty-frames` -- find empty frames
  - `prefer-auto-layout` -- suggest auto-layout
  - `no-hardcoded-colors` -- check variable usage
  - `color-contrast` -- WCAG AA/AAA compliance
  - `touch-target-size` -- minimum 44x44 check
  - `min-text-size` -- minimum 12px text
- **Accessibility snapshot** -- extract interactive elements tree

### Component Variants

- Create component sets with variants
- Add variant properties
- Combine frames into component sets
- **Organize variants** into grid with labels
- **Auto-generate component sets** from similar frames

### Component Documentation

- **Add descriptions** to components (supports markdown)
- **Document with template** (usage, props, notes)
- Read component descriptions

### CSS Grid Layout

- Set up grid layout with columns and rows
- Configure column/row gaps
- Auto-reorganize children into grid

### Console & Debugging

- **List open Figma files** (`files` command, used by uxclaude)
- **Capture console logs** from Figma
- **Execute code with log capture**
- **Reload page**
- **Navigate to files**

### Website Recreation

- **Recreate a URL as Figma frames** (`recreate-url "https://example.com" --name "Page"`)
- **Screenshot any URL** (`screenshot-url "https://example.com"`)

### Advanced

- Execute any Figma Plugin API code directly
- Render complex UI from JSX-like syntax
- Full programmatic control over Figma
- Match vectors to Iconify icons

### Not Supported (requires REST API)

- Comments (read/write/delete) -- requires Figma API key
- Version history
- Team/project management

---

## Author

**[Sil Bormueller](https://www.linkedin.com/in/silbormueller/)** -- [intodesignsystems.com](https://intodesignsystems.com)

## Powered By

All commands use native **Figma Plugin API** implementations via the UX Claude plugin — no external dependencies required beyond the plugin itself.

## License

MIT
