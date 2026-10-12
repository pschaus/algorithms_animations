# Agent Guidelines & Synchronization Protocol (`agents.md`)

This repository contains interactive step-by-step educational animations for the course **LINFO1121: Data Structures and Algorithms** at UCLouvain (taught by Prof. Pierre Schaus, based on *Algorithms 4th Edition* by Robert Sedgewick and Kevin Wayne).

---

## 🚨 MANDATORY INSTRUCTION FOR ALL AI AGENTS

> **Whenever you add, modify, or rename an algorithm visualizer in this repository, you MUST update `index.html` so that the index page, search index, category filters, and quick navigation menu reflect the change.**
>
> **Never consider a task complete without verifying that `index.html` is up to date and that two-way links work seamlessly.**

---

## 1. Repository Architecture

```text
algorithms_animations/
├── index.html            # Central portal: searchable catalog, filter pills, quick navigation menu
├── counting_sort.html    # Standalone visualizer: Counting Sort
├── <new_algorithm>.html  # Any future standalone algorithm visualizer
└── agents.md             # This instruction file for AI agents & contributors
```

### Core Architecture Principles
1. **Self-Contained Visualizers:** Each algorithm visualizer is a standalone HTML file (`*.html`) containing its own CSS and JavaScript (vanilla, no npm build required). It must run cleanly when opened directly in a browser via `file://` or hosted statically on GitHub Pages.
2. **Central Portal (`index.html`):** The single entry point for students and instructors. It catalogs all algorithms, displays time/space complexities, educational properties, search capabilities, and a quick dropdown navigation menu.

---

## 2. Step-by-Step Protocol: Adding a New Algorithm

Follow these steps in order when tasked with adding a new algorithm animation:

### Step 1: Create the New Visualizer File
- Name the file using lowercase snake_case: `<algorithm_name>.html` (e.g. `quick_sort.html`, `red_black_bst.html`, `dijkstra.html`).
- **Include the Back Button in the Header:** The visualizer header **must** include a link back to `index.html`:
  ```html
  <header>
    <div class="header-branding">
      <a href="index.html" class="btn-nav-index" title="Back to Algorithms Index">
        <span>←</span>
        <span>Index</span>
      </a>
      <span class="badge-course">LINFO1121</span>
      <div>
        <h1>Algorithm Name Visualizer</h1>
        <div class="header-subtitle">Educational subtitle / invariant summary</div>
      </div>
    </div>
    ...
  </header>
  ```
  And include the matching CSS style:
  ```css
  .btn-nav-index {
    display: inline-flex;
    align-items: center;
    gap: 0.35rem;
    background: #1e293b;
    color: #94a3b8;
    border: 1px solid var(--border-color, #24344d);
    border-radius: 6px;
    padding: 0.3rem 0.65rem;
    font-size: 0.78rem;
    font-weight: 600;
    text-decoration: none;
    transition: all 0.15s ease;
  }
  .btn-nav-index:hover {
    background: #334155;
    color: var(--accent-blue, #38bdf8);
    border-color: var(--accent-blue, #38bdf8);
  }
  ```

### Step 2: Register the Algorithm in `index.html`
Open `index.html` and locate the `ALGORITHMS` registry array in the `<script>` tag.

1. **If the algorithm was already listed as `"status": "planned"`:**
   - Update its `status` to `"available"`.
   - Ensure `file` matches your exact filename (e.g. `"quick_sort.html"`).
   - Review and refine `description`, `complexities`, `properties`, and `features`.

2. **If adding an algorithm that was not in the initial array:**
   - Add a new object to `ALGORITHMS` following the schema below.

```javascript
{
  id: "quick-sort",                          // Unique slug
  title: "Quick Sort & 3-Way Partitioning",  // Standard English title
  frenchTitle: "Tri rapide (Dijkstra)",      // French title used in UCLouvain lectures
  category: "part2",                         // Course category ID (see Category Mapping below)
  categoryName: "Part 2: Sorting",           // Full category display name
  file: "quick_sort.html",                   // Relative filename
  status: "available",                       // "available" for working visualizers, "planned" otherwise
  description: "Partitions around a pivot element. 3-way Dutch National Flag partitioning handles duplicate keys in linear time.",
  complexities: {
    best: "O(n log n)",
    avg: "O(n log n)",
    worst: "O(n²)",
    space: "O(log n)"
  },
  properties: ["Not Stable", "Comparative", "In-place", "Dutch National Flag"],
  features: ["Step-by-step", "Pivot selection", "Duplicate keys demo", "Call stack view"]
}
```

> **Automated Dynamic UI:** Once `ALGORITHMS` is updated, `index.html` automatically:
> - Renders the algorithm card with the glowing emerald "● Live Visualizer" badge and active "Launch Visualizer ➔" CTA button.
> - Adds the entry to the top header "⚡ Algorithms Menu" dropdown.
> - Updates the category filter pill counts.
> - Updates the hero banner statistics counters (`statAvailableCount`, `statTotalCount`).
> - Indexes the algorithm for real-time search queries.

### Step 3: Verify Two-Way Navigation
1. Open `index.html` in a browser or test tool:
   - Check that the new algorithm appears under its category.
   - Click "Launch Visualizer ➔" and verify that it loads the new page.
   - Test the "⚡ Algorithms Menu" dropdown and ensure clicking the algorithm works.
2. In the new algorithm page:
   - Click the "← Index" button and verify that it navigates cleanly back to `index.html`.

---

## 3. Course Category Mapping (LINFO1121)

When assigning `category` and `categoryName`, use the following standard course parts:

| Category ID | Display Name (`categoryName`) | Typical Algorithms & Data Structures |
| :--- | :--- | :--- |
| `part1` | `Part 1: Data Structures` | Dynamic Arrays, Stacks, Queues, Linked Lists, Union-Find (WQUPC) |
| `part2` | `Part 2: Sorting` | Counting Sort, Selection, Insertion, Shellsort, Merge Sort, Quick Sort (3-Way), Heap Sort, Radix Sort (LSD/MSD) |
| `part3` | `Part 3: Search Trees` | Binary Search Trees (BST), 2-3 Trees, Left-Leaning Red-Black BST (LLRB), B-Trees |
| `part4` | `Part 4: Hash & Strings` | Hash Tables (Separate Chaining, Linear Probing), Tries, TST, Substring Search (KMP, Boyer-Moore, Rabin-Karp) |
| `part5` | `Part 5: Priority Queues` | Binary Heaps (Min/Max), Huffman Compression, LZW Compression |
| `part6` | `Part 6: Graphs` | DFS, BFS, Topological Sort, Strongly Connected Components, MST (Prim, Kruskal), Shortest Paths (Dijkstra, Bellman-Ford) |

---

## 4. UI & Visual Design Standards for Visualizers

To maintain visual unity across the entire course suite, all visualizers should follow the design language established in `counting_sort.html` and `index.html`:

### Theme Palette (Dark Mode)
```css
:root {
  --bg-main: #0b1120;        /* Deep navy background */
  --bg-card: #151f32;        /* Card surface */
  --bg-card-inner: #0f172a;  /* Inset panels, inputs, arrays */
  --border-color: #24344d;   /* Subtle divider border */
  --border-light: #334869;   /* Hover / focused borders */
  --text-main: #f8fafc;      /* Crisp white body text */
  --text-muted: #94a3b8;     /* Secondary descriptions */
  --text-dim: #64748b;       /* Muted labels & hints */

  /* Accents */
  --accent-blue: #38bdf8;    /* Primary highlight & active states */
  --accent-indigo: #6366f1;  /* Secondary accent */
  --accent-emerald: #10b981; /* Success, sorted elements, live status */
  --accent-amber: #f59e0b;   /* Warnings, active pivots, current pointers */
  --accent-rose: #f43f5e;    /* Mismatches, deletions */
}
```

### Essential Visualizer Controls
Each visualizer should ideally provide:
- **Phase Bar / Stepper:** Visual pill indicator showing which phase of the algorithm is currently executing.
- **Playback Controls:** Previous Step (`⏮`), Play / Pause (`▶` / `⏸`), Next Step (`⏭`), Reset (`↺`).
- **Speed Slider:** Adjust animation delay (e.g. 100ms to 2000ms).
- **Data Generator:** Random instance button + preset configurations (including edge cases such as sorted, reverse-sorted, duplicate keys).
- **Custom Input:** Modal or input field allowing students to test custom arrays/values.
- **Pseudo-Code / Invariant Panel:** Visual box highlighting the active line of code or mathematical invariant being maintained.

---

## 5. Agent Verification Checklist

Before reporting completion on any task that creates or modifies an algorithm visualizer, verify each item:

- [ ] New HTML file is saved in the repository root directory.
- [ ] New HTML file contains the "← Index" back button in its header.
- [ ] `index.html` has been updated:
  - [ ] `ALGORITHMS` entry has `status: "available"`
  - [ ] `file` path is correct and relative (e.g. `"my_algo.html"`)
  - [ ] Time and space complexities are accurately documented
  - [ ] French title and English title are present
  - [ ] Category ID corresponds to the correct LINFO1121 course part
- [ ] Opened and tested in browser:
  - [ ] Clicking "Launch Visualizer" from `index.html` opens the visualizer.
  - [ ] Clicking "← Index" returns to `index.html`.
  - [ ] Category filter pills count and display the new visualizer correctly.
  - [ ] Searching for the algorithm title in the search input matches the card.
  - [ ] Top header "⚡ Algorithms Menu" dropdown lists the visualizer with a green "Live" badge.
