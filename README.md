# TGG Grid

**The Greco Grid**

A dependency-free, local-first data workspace for exploring, editing, analyzing, and visualizing CSV data entirely in the browser.

TGG Grid is built as a **Single-File Local Application (SFLA)**. The complete application runs from a single HTML file with no application server, package manager, framework, installation process, or third-party runtime dependencies.

Load a CSV, work with the data locally in your browser, and optionally save a TGG configuration file to preserve the workspace you've built around it.

> **Your CSV is the data. Your TGG configuration is the workspace.**

## Run TGG Grid

**[▶ Run TGG Grid in your browser](https://mikejamesgreco.github.io/tgg-grid/)**

No installation is required. The GitHub Pages version runs TGG directly in your browser, just like opening the standalone `tgg-grid.html` file locally. Your normal CSV workflow remains local-first; files you load are processed in the browser unless you explicitly use a feature that communicates with an external service, such as API Explorer.

---

## Why TGG Grid?

Many data tools require uploading data to a service, installing desktop software, running a server, or building a development environment.

TGG Grid takes a different approach.

```text
CSV File
   │
   ▼
┌─────────────────────────────┐
│          TGG Grid           │
│                             │
│  Edit       Analyze         │
│  Filter     Validate        │
│  Search     Visualize       │
│  Transform  Explore         │
│                             │
└──────────────┬──────────────┘
               │
        ┌──────┴──────┐
        ▼             ▼
   Modified CSV    TGG Config
```

The application runs locally in the browser and works directly with user-owned files.

---

## Core Principles

TGG Grid is designed around a few simple principles:

- **Local-first** — data is processed in the browser.
- **Single-file application** — the application is distributed as one HTML file.
- **Zero third-party runtime dependencies** — no frameworks, CDNs, or runtime packages are required.
- **CSV-first** — ordinary CSV files remain the physical data source.
- **Non-proprietary data** — using TGG does not require converting your data into a proprietary file format.
- **Configuration is separate from data** — workspace behavior can be saved independently from the CSV.
- **Progressive capability** — TGG can be used as a simple CSV viewer/editor or as a much richer data workspace.
- **Browser-native APIs first** — native browser capabilities are preferred wherever practical.

---

## Getting Started

No installation is required.

1. Open the **[hosted TGG Grid](https://mikejamesgreco.github.io/tgg-grid/)** or open `tgg-grid.html` locally in a modern browser.
2. Choose **Load Data**.
3. Select a CSV file.
4. Start working with the data.

A TGG configuration file is optional.

You can begin with nothing more than:

```text
customers.csv
```

and later build a workspace around it:

```text
customers.csv
customers.json
```

The CSV contains the physical data.

The configuration can preserve things such as views, layouts, formatting, validation rules, calculated columns, visualizations, and other workspace behavior.

---

## CSV Editing and Data Operations

TGG Grid is not just a CSV viewer.

Physical CSV data can be edited directly using features including:

- Inline cell editing
- Multi-cell selection
- Row selection
- Copy and paste
- Fill operations
- Find and replace
- Bulk transformations
- Insert rows
- Duplicate rows
- Delete rows
- Undo and redo
- Data validation
- Data-quality analysis
- Column profiling

Modified physical data can be written back to CSV using **Save Data**.

---

## Virtualized Grid

TGG Grid uses a virtualized rendering architecture.

Only the rows needed for the visible portion of the grid are rendered into the DOM, allowing the application to work with datasets substantially larger than would be practical using a traditional HTML table.

Internally, physical records are stored compactly as row-oriented delimited strings rather than expanding every cell into a permanent JavaScript object.

This architecture was designed specifically with large browser-resident datasets in mind.

---

## Columns

TGG supports several kinds of columns.

### Physical Columns

Columns originating from the CSV.

These are editable and are included when physical data is saved or exported.

### Calculated Columns

Read-only virtual columns created using TGG's safe formula language.

Examples include:

```text
[Quantity] * [Unit Price]
```

and:

```text
IF([Status] = "OPEN", "Active", "Complete")
```

Calculated columns do not modify the physical CSV structure.

### JavaScript Derived Columns

Advanced virtual columns can execute trusted JavaScript expressions.

These provide substantially more flexibility than calculated columns but should only be used with configuration files you trust.

### Action Columns

Virtual columns can also expose row-level actions such as:

- Opening URLs
- Copying values
- Opening row details
- Running custom JavaScript actions

---

## Cell Rendering

Columns can use alternate presentation styles without changing the underlying CSV value.

Current capabilities include:

- Text
- Numeric formatting
- Currency
- Percentage
- Date
- Date/time
- Conditional formatting
- Badges
- Links
- QR codes

Presentation remains separate from physical data.

---

## Saved Views

A single CSV can support multiple ways of working with the same dataset.

TGG Saved Views preserve presentation and workspace state without duplicating the underlying data.

Current view types include:

### Grid

The standard editable data-grid workspace.

### Kanban

Groups records into lanes and displays them as cards.

Useful for:

- Project tracking
- Issue tracking
- Sales pipelines
- Workflow queues
- Status boards

### Gantt

Displays date-oriented records on a timeline.

Useful for:

- Projects
- Tasks
- Schedules
- Release plans
- Implementation timelines

### Sequence

Generates interactive sequence diagrams directly from CSV records.

Supported constructs include:

- Requests
- Responses
- Asynchronous messages
- Notes
- Self-calls
- Activation bars
- Participant destruction
- Groups and phases
- `alt` / `else`
- `opt`
- `loop`
- Nested fragments

Sequence diagrams can also be exported as PNG images.

### API Explorer

Turns CSV records describing REST operations into an interactive API-testing workspace.

Current capabilities include:

- GET, POST, PUT, PATCH, DELETE, and other HTTP methods
- Path parameters
- Query parameters
- Custom request headers
- JSON request bodies
- JSON Schema-driven request generation
- Local JSON Schema `$ref` resolution
- Basic authentication
- Bearer authentication
- API-key authentication
- Multiple API environments
- Direct browser `fetch()` invocation
- Response inspection

Runtime credentials are intentionally kept separate from persisted configuration.

---

## Source View

Every loaded dataset has a protected **Source View**.

Source View provides a predictable representation of the physical CSV:

- Physical columns only
- Original source-column order
- Raw values
- No derived columns
- No action columns
- No presentation renderers
- No saved formatting
- No persisted column hiding or pinning

It provides a convenient way to return to the underlying data regardless of how sophisticated the workspace becomes.

---

## Analysis

TGG includes several built-in analysis capabilities.

### Aggregation

Build grouped summaries using operations such as:

- Count
- Distinct count
- Sum
- Average
- Minimum
- Maximum

### Pivot

Create multi-dimensional summaries with:

- Multiple row dimensions
- Column dimensions
- Multiple measures
- Expand/collapse
- Parent totals
- Grand totals
- Top/Bottom N
- Percentage displays
- Drill-down

### Data Profiling

Inspect the characteristics of columns and values.

### Data Quality

Analyze datasets for potential quality issues and duplicate records.

### Validation Audit

Run configured validation rules across the current view or full dataset and inspect violations.

Several heavyweight analysis operations execute using browser Web Workers to reduce blocking of the main user interface.

---

## File Handling

TGG keeps physical data and workspace configuration intentionally separate.

### Save Data

Writes the modified physical dataset back to CSV.

### Export Data

Exports a chosen subset or representation of the data.

### Save Config

Stores TGG workspace configuration independently from the CSV.

Where supported, TGG uses the browser File System Access API and streaming writes to reduce the memory overhead associated with exporting large files.

Fallback browser download behavior is used where those APIs are unavailable.

---

## Local-First Architecture

TGG itself does not require a backend server.

```text
┌──────────────────── Browser ────────────────────┐
│                                                │
│ CSV ──► TGG Grid ──► Edit / Analyze / Display  │
│             │                                  │
│             ├────► CSV                         │
│             └────► Config                      │
│                                                │
└────────────────────────────────────────────────┘
```

Ordinary CSV processing, editing, analysis, and visualization occur locally.

Some optional features, such as API Explorer, intentionally communicate with remote systems when the user invokes an API operation.

---

## API Explorer and CORS

API Explorer uses the browser's native `fetch()` implementation.

Normal browser security rules therefore apply, including **Cross-Origin Resource Sharing (CORS)**.

An API must permit browser requests from the current origin for direct invocation to succeed.

TGG does not attempt to bypass browser CORS restrictions.

For controlled development or internal testing environments, browser-development tools or extensions may be used to alter CORS behavior. Production systems should instead configure appropriate server-side CORS policies or use an approved API gateway/proxy.

---

## Trusted Configuration

TGG configuration files can contain executable JavaScript for advanced functionality such as Derived Columns and Action Columns.

For that reason:

> **Only load TGG configuration files from sources you trust.**

TGG's calculated-column formula language is separately parsed and does not use arbitrary JavaScript execution, but advanced JavaScript features intentionally provide access to normal browser capabilities.

---

## Single-File Local Application (SFLA)

TGG Grid follows an architecture we refer to as a **Single-File Local Application**, or **SFLA**.

An SFLA is a complete browser application designed to operate primarily from a single self-contained file.

For TGG this means:

```text
tgg-grid.html
```

contains the application.

No runtime installation is necessary.

The surrounding repository contains documentation, samples, regression tests, and development resources, but they are not required to run the application itself.

---

## Repository Structure

The repository is intentionally simple.

```text
tgg-grid/
│
├── index.html              # GitHub Pages launcher
├── tgg-grid.html           # Standalone TGG application
│
├── samples/
│   ├── grid/
│   ├── kanban/
│   ├── gantt/
│   ├── sequence/
│   └── api-explorer/
│
├── test/
│   ├── fixtures/
│   ├── expected/
│   └── run-regression.js
│
├── docs/
│
├── README.md
├── CHANGELOG.md
└── LICENSE
```

The exact structure may evolve as the project grows.

---

## Regression Testing

TGG has grown beyond a simple grid, so preserving existing functionality as new features are introduced is important.

The project is moving toward a permanent regression suite consisting of:

- Canonical CSV fixtures
- Canonical workspace configurations
- JavaScript syntax validation
- Feature-inventory validation
- Unit tests for pure JavaScript functions
- Browser smoke tests
- Manual visual/UX validation

The goal is for every release to be tested against the same known feature baseline.

---

## Browser Support

TGG is designed for modern desktop browsers.

Chromium-based browsers such as Microsoft Edge and Google Chrome currently provide the broadest support for browser-native capabilities used by TGG, particularly the File System Access API.

Other modern browsers may use fallback behavior where a particular browser API is unavailable.

---

## Privacy

TGG's normal CSV workflow is local-first.

Loading a CSV does not inherently require uploading that CSV to a TGG server or cloud service.

Users should still consider the behavior of:

- APIs they explicitly invoke
- URLs opened by actions
- JavaScript contained in trusted configurations
- Browser extensions
- Browser policies
- Other external services they intentionally use

when working with sensitive information.

---

## Project Status

TGG Grid is under active development.

The application has evolved from an experimental high-performance CSV grid into a broader local data workspace. Features and configuration formats may continue to evolve while the project approaches stable public releases.

---

## Philosophy

TGG is intentionally built differently from many modern web applications.

The objective is not to eliminate JavaScript or browser capabilities. It is to eliminate unnecessary infrastructure between the user and their data.

```text
No framework.
No package manager.
No application server.
No proprietary data store.
No third-party runtime dependencies.

Just a browser, a file, and your data.
```

---

## License

License information will be added to the repository's `LICENSE` file.

---

## Author

**Michael J. Greco**

TGG Grid — **The Greco Grid**

© mikejamesgreco.me LLC. All rights reserved.
