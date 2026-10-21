# AI Prompt & Code Studio Workbench

A lightweight, local-first developer productivity workbench built for prompt engineers, software architects, and AI developers. Create and curate reusable system prompts, extract and inject dynamic template variables in real-time, inspect AI-generated code patches with an aligned side-by-side diff visualizer, estimate token consumption, and manage full JSON workspace backups.

Zero build step, zero dependencies, zero telemetry. Runs directly in any modern browser.

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Architecture & Technology Stack](#architecture--technology-stack)
- [Project File Structure](#project-file-structure)
- [Quick Start](#quick-start)
- [Browser Compatibility](#browser-compatibility)
- [Data Persistence & Storage Model](#data-persistence--storage-model)
- [Prompt Library & Templates](#prompt-library--templates)
- [Variable Placeholder Syntax & Presets](#variable-placeholder-syntax--presets)
- [Diff & Patch Inspector](#diff--patch-inspector)
- [Workspace Backup & Restore](#workspace-backup--restore)
- [Global Keyboard Shortcuts](#global-keyboard-shortcuts)
- [Offline Resilience & Fallback Behavior](#offline-resilience--fallback-behavior)
- [Troubleshooting & Known Limitations](#troubleshooting--known-limitations)
- [Git Workflow & Milestones](#git-workflow--milestones)

---

## Overview

Modern AI development workflows often suffer from scattered system prompts, tedious copy-pasting of variable placeholders, and the challenge of inspecting subtle code modifications suggested by Large Language Models.

**AI Prompt & Code Studio Workbench** provides a unified, local-first cockpit that runs entirely on client-side web technologies without requiring Node.js, databases, or local servers. All workspace data is persisted in browser `localStorage`, ensuring complete privacy and immediate launch times.

---

## Key Features

### 1. Reusable Prompt Library
- **Full CRUD Support:** Create, view, edit, duplicate, and delete prompt templates with instant modal interfaces.
- **Categorization & Tags:** Group prompts under `coding`, `architecture`, `ui`, `debugging`, and `security` categories with multi-tag support.
- **Real-Time Search & Filtering:** Debounced search across prompt titles, descriptions, bodies, and tags combined with category filter chips.
- **Pre-Seeded Factory Templates:** Ships with 4 production-grade system prompts for security audits, enterprise architecture specs, accessible Tailwind UI design, and root-cause bug refactoring.

### 2. Dynamic Variable Injector
- **Automatic Variable Extraction:** Parses `{{VARIABLE_NAME}}` placeholders dynamically from prompt templates using regular expressions.
- **Smart Adaptive Input Forms:** Automatically detects multiline fields (such as code snippets, specs, error logs) versus single-line fields (such as languages, frameworks).
- **One-Click Suggestion Chips:** Pre-configured quick-fill suggestions for common programming languages, frameworks, and output formats.
- **Live Output Synthesizer:** Real-time prompt compilation as you type, preserving whitespace and formatting.
- **Unresolved Placeholder Detection:** Visual alert badges highlight any missing variables before copying.
- **Variable Presets:** Save and load customized sets of variable values for specific templates.
- **Seamless Diff Transfer:** Send the synthesized prompt directly into the Diff Inspector with one click.

### 3. Side-by-Side Diff & Patch Inspector
- **Custom LCS Line-Diff Engine:** High-performance Longest Common Subsequence line diff with prefix and suffix trimming optimization.
- **Side-by-Side Aligned View:** Color-coded additions (emerald `+`), deletions (rose `-`), and unchanged lines with synchronized dual line numbers.
- **Utility Actions:** Swap original and modified code panes, normalize indentation (convert tabs to 2 spaces and trim trailing whitespace), clear inputs, or copy modified code.
- **Live Diff Statistics:** Real-time counters for added, removed, and unchanged lines.
- **Identical State Detection:** Clear visual feedback when original and modified sources match identically.

### 4. Text Metrics & Token Estimation
- Real-time character, word, line, and approximate token counting.
- Uses standard heuristic token estimation (`Estimated tokens ≈ character count / 4`) labeled clearly as an estimate.

### 5. Workspace JSON Backup & Restore
- **Export Backup:** Downloads a complete, versioned, timestamped JSON snapshot (`prompt-workbench-backup-YYYY-MM-DD.json`).
- **Safe Import Engine:** Validates schema structure, sanitizes input types, and displays a restore summary.
- **Flexible Restore Modes:** Choose between **Merge with existing** (preserves current prompts and updates matching IDs) or **Replace entire workspace** (clean wipe and restore).
- **Drag-and-Drop Zone:** Drop JSON backup files directly into the Settings panel.

### 6. Quick Launcher & Workflow Shortcuts
- Global search palette (`Ctrl + K` or `Cmd + K`) for instant navigation between views, quick actions, and individual prompts.
- Keyboard navigation (Arrow keys, Enter, Escape).
- Quick copy shortcut (`Ctrl + Enter` or `Cmd + Enter`) to immediately copy active output.

---

## Architecture & Technology Stack

The workbench follows a zero-dependency, single-file architectural model:

| Component | Technology | Delivery |
| :--- | :--- | :--- |
| **Markup & Structure** | Semantic HTML5 | Embedded in `index.html` |
| **CSS Utilities** | Tailwind CSS v3 | CDN (`cdn.tailwindcss.com`) |
| **Custom Styling & Fallbacks** | Vanilla CSS3 (Custom Properties) | Embedded `<style>` block |
| **Icons** | Font Awesome 6.5.1 | CDN (`cdnjs.cloudflare.com`) |
| **Typography** | Inter & JetBrains Mono | Google Fonts CDN |
| **Client Engine** | Vanilla ES6+ JavaScript | Embedded `<script>` block |
| **Persistence Engine** | Web Storage API (`localStorage`) | Native Browser API |
| **Clipboard Engine** | Async Clipboard API + ExecCommand Fallback | Native Browser API |

### Architecture Principles

1. **Local-First & Client-Only:** No server, database, or network connection is required for core prompt editing, variable injection, diffing, or data persistence.
2. **Defensive Storage Operations:** All localStorage reads and writes are wrapped in safe JSON serialization and quota-handling blocks.
3. **Safe DOM Rendering:** User-entered prompt text and diff lines are escaped or rendered safely via `textContent` to prevent DOM XSS vulnerabilities.
4. **Degradation Resilience:** Embedded CSS variables ensure the dark theme, layout grids, borders, and typography remain functional even when external CDNs are unavailable.

---

## Project File Structure

```
AI-Powered Code & Prompt Refinement Workbench/
├── index.html        # Self-contained single-page application (HTML, CSS, JS)
└── README.md         # Full project documentation and operational manual
```

---

## Quick Start

No package manager, npm install, or build command is required.

1. **Clone or Download:**
   ```bash
   git clone https://github.com/Red-swipe/Code-Prompt-Refinement-.git
   cd "Code-Prompt-Refinement-"
   ```

2. **Open in Browser:**
   - Double-click `index.html` to open it in your default web browser (Edge, Chrome, Brave, Firefox, Safari).
   - Alternatively, open from the command line:
     ```bash
     # Windows PowerShell
     Start-Process "index.html"

     # macOS
     open index.html

     # Linux
     xdg-open index.html
     ```

---

## Browser Compatibility

The application is thoroughly tested and compatible with modern evergreen browsers:

- **Microsoft Edge:** 90+ (Chromium)
- **Google Chrome:** 90+
- **Brave Browser:** 1.20+
- **Mozilla Firefox:** 88+
- **Apple Safari:** 14+

*Requirements: JavaScript must be enabled. Local storage must be accessible (standard private browsing modes allow ephemeral local storage).*

---

## Data Persistence & Storage Model

All persistent workbench data is isolated in your browser's origin `localStorage`:

| Storage Key | Type | Description |
| :--- | :--- | :--- |
| `workbench_prompts` | `Array<PromptRecord>` | User-curated and factory-seeded prompt templates |
| `workbench_presets` | `Array<PresetRecord>` | Saved variable configurations per template |
| `workbench_settings` | `Object` | Optional application preferences |

### Prompt Record Schema
```typescript
interface PromptRecord {
  id: string;              // Unique identifier (e.g., "prompt_1712345678_ab12cd")
  title: string;           // Template display title
  description: string;     // Short summary of prompt utility
  category: string;        // Primary category: coding | architecture | ui | debugging | security | general
  tags: string[];          // Array of search/filter tags
  body: string;            // Raw template string with {{PLACEHOLDERS}}
  createdAt: string;       // ISO 8601 timestamp
  updatedAt: string;       // ISO 8601 timestamp
}
```

### Preset Record Schema
```typescript
interface PresetRecord {
  id: string;              // Unique preset identifier
  promptId: string;        // Associated prompt template ID
  name: string;            // Name of the preset (e.g., "TypeScript & Fastify")
  values: Record<string, string>; // Map of variable names to values
  createdAt: string;       // ISO 8601 timestamp
}
```

---

## Prompt Library & Templates

The application initializes with four pre-configured production system prompts:

1. **Code Reviewer & Security Auditor:** Inspects code for OWASP Top 10 vulnerabilities, race conditions, memory safety, Big-O algorithmic complexity, and generates refactored code patches.
2. **System Architecture Spec Generator:** Transforms high-level requirements into enterprise architecture documentation, Mermaid topology diagrams, data models, API contracts, and scalability roadmaps.
3. **Tailwind CSS & UI Component Designer:** Generates fully accessible (WCAG AA), responsive, interactive UI components with coherent state handling and dark mode support.
4. **Bug Hunter & Refactoring Agent:** Isolates root causes from error traces, produces surgical non-breaking fixes, idiomatic clean-code refactorings, and regression test suites.

---

## Variable Placeholder Syntax & Presets

### Placeholder Syntax
Placeholders must follow standard mustache syntax:
```
{{VARIABLE_NAME}}
```
- Variable names may contain letters, digits, and underscores (e.g., `{{LANGUAGE}}`, `{{FOCUS_AREAS}}`, `{{SCHEMA_1}}`).
- Leading and trailing spaces inside braces are automatically trimmed (e.g., `{{  FRAMEWORK  }}` parses as `FRAMEWORK`).
- Duplicate placeholders in the same prompt share a single input field; updating one replaces all occurrences.

### Suggestion Chips
Variables matching common names display clickable shortcut pills:
- `LANGUAGE`: TypeScript, JavaScript, Python, Rust, Go, Java, Dart, C++
- `FRAMEWORK`: React, Next.js, Tailwind CSS, FastAPI, Flutter, Node.js, Vue.js
- `OUTPUT_FORMAT`: Markdown, JSON, Code-only, Structured Report
- `SCALE_GOAL`: 10k DAU, 100k DAU, 1M DAU, 10,000 req/sec

---

## Diff & Patch Inspector

The Diff Inspector lets you verify changes made by AI assistants:

- **Original Code (Left Pane):** Paste existing source code or previous prompt iteration.
- **Modified Code (Right Pane):** Paste revised code or AI response.
- **LCS Line Engine:** Computes minimal edit scripts using Longest Common Subsequence logic with prefix and suffix trimming.
- **Aligned Table Output:** Displays exact matching row pairs with individual line numbers:
  - <span style="color: #f43f5e; font-weight: bold;">Red (-)</span>: Removed lines.
  - <span style="color: #10b981; font-weight: bold;">Green (+)</span>: Added lines.
  - Neutral: Unmodified context lines.
- **Toolbar Utilities:** Swap Original/Modified, Normalize whitespace/indentation, Clear, and Copy Modified.

---

## Workspace Backup & Restore

### Export
Click **Export** in the top navigation or Settings panel to download a JSON snapshot:
```json
{
  "app": "AI Prompt & Code Studio Workbench",
  "schemaVersion": "1.0",
  "exportedAt": "2026-10-21T15:30:00.000Z",
  "data": {
    "prompts": [ ... ],
    "presets": [ ... ]
  }
}
```

### Restore
1. Click **Import** or drag-and-drop a `.json` backup file onto the drop zone in Settings.
2. The Import Modal validates the file and displays total prompts and presets found.
3. Select your restore strategy:
   - **Merge with existing:** Retains existing templates and overwrites records sharing identical IDs.
   - **Replace entire workspace:** Overwrites the entire local database with the imported backup.
4. Click **Apply Restore** to commit changes.

---

## Global Keyboard Shortcuts

| Shortcut | Action | Scope |
| :--- | :--- | :--- |
| <kbd>Ctrl</kbd> + <kbd>K</kbd> / <kbd>Cmd</kbd> + <kbd>K</kbd> | Open Quick Jump / Search Palette | Global |
| <kbd>Ctrl</kbd> + <kbd>Enter</kbd> / <kbd>Cmd</kbd> + <kbd>Enter</kbd> | Copy active prompt output or modified code | Global |
| <kbd>Escape</kbd> | Close active modal, dropdown, or drawer | Global |
| <kbd>↑</kbd> / <kbd>↓</kbd> | Navigate launcher search results | Quick Launcher |
| <kbd>Enter</kbd> | Execute selected item | Quick Launcher |

---

## Offline Resilience & Fallback Behavior

- **Core Functionality Offline:** All data management, prompt compilation, variable injection, diff algorithms, token calculations, and JSON export/import operate 100% offline without network requests.
- **External Dependencies:**
  - Tailwind CSS CDN, Font Awesome icons, and Google Fonts are fetched when connected to the internet.
  - If loaded offline or behind restrictive firewalls, native system fonts (`system-ui`, monospace) and embedded CSS fallback variables maintain layout integrity, contrast ratios, and button functionality.

---

## Troubleshooting & Known Limitations

1. **Storage Unavailable:** If third-party cookies or storage are completely blocked by browser privacy extensions, changes will only persist in memory for the current session.
2. **Clipboard Restrictions:** If clipboard permissions are denied by the browser, use standard manual selection (`Ctrl + A`, `Ctrl + C`) within the output pane.
3. **Very Large Files in Diff (>10,000 lines):** To maintain interface responsiveness, files exceeding 2.5 million line-product comparisons gracefully fall back to chunked line diffing.

---

## Git Workflow & Milestones

The project was built and versioned through six sequential execution stages:

1. `feat(ui): initialize dark theme UI shell and navigation layout`
2. `feat(prompts): add system prompt library CRUD and localstorage persistence`
3. `feat(injector): implement dynamic template variable extraction and live prompt preview`
4. `feat(diff): build side-by-side line diff visualizer and patch comparison engine`
5. `feat(utils): add token estimation, workspace JSON import/export, and keyboard shortcuts`
6. `docs(readme): finalize project documentation and production builds`

---

## License

MIT License. Free for personal, commercial, and enterprise developer productivity.
