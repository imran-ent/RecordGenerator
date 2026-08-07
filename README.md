# Record Press - Lab Record Generator

**Record Press** is a lightweight, zero-dependency web utility that lets students and educators quickly generate clean, standardized, print-ready lab records and assignment write-ups.

Fill in your experiment details, code, and sample outputs on the left workbench and instantly preview a live, perfectly framed lab sheet on the right. Each page is laid out in JavaScript to exactly fit A4, so the on-screen preview matches the printed PDF pixel-for-pixel, including a full border on every page.

---

## Features

- **Live split-screen workbench:** Real-time side-by-side editing and preview.
- **Full border on every page:** JS pagination splits content across exact-size A4 sheets, so every printed page (including blank ruled ones) carries a complete frame.
- **Custom security watermark:** Tiles your roll number, registration ID, or institutional identifier diagonally across every page.
- **Flexible section modes:** Toggle sections such as Aim or Algorithm between typed text and blank rule-lined areas for manual handwriting.
- **Code & output formatting:** Styled code blocks and terminal output blocks with an optional "=== Code Execution Successful ===" success line.
- **Extra blank ruled pages:** Append fully ruled A4 pages (plain sheets with only the watermark and page number) for workings, diagrams, or a viva page.
- **Per-section typography:** Set a base font and size, then override per section (Title, Aim, Algorithm, Source Code, Output, Result).
- **Autosave & backup:**
  - Work auto-saves to this browser's `localStorage` and is restored on reload.
  - Export/Import full records as `.json` backup files.
  - **Cloud backup via Supabase:** Save, update, load, and delete records in your own Supabase project.
  - **Save as PDF:** Styled via print CSS targeting standard A4.
  - **Download as Word (.doc):** Word-readable HTML document with the full record (headers, Aim, Algorithm, Source Code, Outputs, Result, and blank-page boxes) laid out for A4.

---

## Quick Start

1. Download or copy the `index.html` file.
2. Open `index.html` in any modern web browser (Chrome, Edge, Firefox).
3. Fill out the workbench fields:
   - **Header info:** Title, Experiment No., Date, Watermark.
   - **Content sections:** Aim, Algorithm, Source Code, Outputs, Result.
   - **Pages:** Optional extra blank ruled pages.
   - **Typography:** Base font/size plus per-section overrides.
4. Click **Print / Save as PDF** or **Download as Word (.doc)**.
   - For PDF: set **Destination** to **Save as PDF**, keep **Paper size** on **A4** and **Margins** on **None**, and enable **Background graphics** so watermarks and output boxes render.
5. Optionally press **Connect** under *Cloud Backup* to store records in Supabase.

---

## Supabase Cloud Setup

1. Create a free project at [supabase.com](https://supabase.com).
2. Open **SQL Editor** and run:

   ```sql
   create table records (
     id uuid primary key default gen_random_uuid(),
     name text not null,
     payload jsonb not null,
     created_at timestamptz default now(),
     updated_at timestamptz default now()
   );
   ```

3. In the project settings, copy your **Project URL** and **anon public key**.
4. In Record Press, paste both into the *Cloud Backup* panel and press **Connect & Save Settings**.
5. Use **Save to cloud** to push the current workbench, **Load** / **Delete** per saved record, and **Backup .json** / **Restore .json** for offline backups.

Your Supabase URL and anon key are stored only in this browser's `localStorage`. The anon key is safe to ship in front-end code as long as Row Level Security is enabled on your table.

---

## Printing & PDF Export Tips

- **Destination:** Save as PDF.
- **Paper Size:** A4.
- **Margins:** None (the template provides its own 12 mm internal border).
- **Background Graphics:** On, so the watermark and shaded output boxes print.

---

## Technology Stack

- **HTML5 & CSS3:** Responsive workbench layout and custom `@media print` stylesheets.
- **Vanilla JavaScript (ES6+):** No build step or npm dependencies for the app itself.
- **Supabase JS (CDN):** Optional cloud backup via the browser `window.supabase` client.

---

## License

Distributed under the MIT License. Feel free to modify and adapt for personal or institutional use.
