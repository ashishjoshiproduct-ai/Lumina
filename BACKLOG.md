# Lumina — Backlog (post-MVP)

Things we've consciously decided *not* to build for the MVP, with the reasoning so future-us remembers why. Parked, not forgotten.

## Navigation
- **Scroll-depth reading instead of Next button.** MVP uses a Next button because it gives a dead-simple "what have you read" signal. The natural UX is free scroll with invisible checkpoints (mark a section read once it scrolls past the top), but that's more code and not needed to prove the core idea. Upgrade once the AI features are validated.

## Memory / persistence
- **Anything beyond Level 2 (device memory).** MVP saves progress per-PDF on the user's device via browser storage. Level 3 — cloud accounts with sign-in, a server, and a database so progress follows the user across devices — is real infrastructure and premature until people demonstrably want to come back. Defer.

## Chunking / document parsing
- **Smart section detection.** MVP splits text crudely (every ~150 words). Real section boundaries (Abstract, Methods, etc.) are messy to extract from PDFs and can wait. The whole splitter lives in one function, so this is a contained upgrade.
- **PDF identity beyond filename.** MVP tells PDFs apart by filename, so two different files both named `paper.pdf` would clobber each other's progress. Rare; fix later with a content-based fingerprint.

## Test material / scope
- **Research-paper-specific features.** MVP stays general (any text-based PDF). Paper-specific niceties (parsing arXiv structure, citations, figures) are a possible future wedge but not MVP.
- **Scanned / image-only PDFs.** MVP only handles text-based PDFs. Scanned documents need OCR (image-to-text), which is a separate, heavier capability.

## Showing figures and images
- **MVP is text-only and drops all figures.** Two ways to display a PDF, in tension: (a) extract text — what we do; enables AI scoping but loses images and layout; (b) render each page as an image — shows figures and layout, but the app can't read the words without OCR. The real answer is to do BOTH: render the page for the human, extract text in the background for the AI. More work; deferred until the core AI value is proven.

## Watermark / header / footer noise
- **Fixed the arXiv vertical watermark** (filter rotated text fragments). Still TODO: page numbers, running headers/footers, and line numbers can still leak into the text. Improve the cleanup pass later.

## Heading detection (added, heuristic)
- **Headings detected by font size** (lines clearly bigger than body = heading). Good enough but imperfect: unusual typography can miss or mislabel a heading. Could upgrade with font-weight/position signals or a proper PDF structure parser later. This also serves as the first step toward the "smart section detection" item above.

## Footnote / reference marker stripping (added, crude)
- **Small stray digit-fragments are dropped** (raised reference numbers print smaller than body). Risk: occasionally drops a legitimately small number. Also can't yet split a reference number fused into the same fragment as a word. "Strip for now, revisit later" per decision.

## Page-number jump
- **Jump is by section number, not the paper's printed page number.** Tracking printed page numbers was deferred when we moved off pages; revisit if real page-number jumping is wanted.

## Not yet specified (placeholders for features still ahead)
- The AI "Clarify" and "Recall" layers — these are core to the product but not yet built; this backlog tracks what we're *skipping*, not what's still to come.
