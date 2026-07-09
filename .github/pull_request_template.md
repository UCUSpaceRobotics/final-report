## What this PR adds

<!-- One or two sentences. Which section / team file, what content. -->

## Cross-references added or updated

<!-- \autoref / \ref links to or from other sections, if any. Write "none" otherwise. -->

## What remains

<!-- Anything intentionally left for a follow-up PR. Write "nothing" if complete. -->

## Screenshot

<!-- REQUIRED: a screenshot of the compiled section/page(s) this PR changes,
     pasted directly below (drag-and-drop the image into this box).
     Reviewers should be able to see your change without downloading the PDF. -->

## Checklist

- [ ] One content file changed (plus its own figures)
- [ ] Tiny contract (`% Teams: … / Status: …`) updated
- [ ] No placeholders (`[X]`, `[Add content …]`, `\lipsum`)
- [ ] All quantities via `siunitx` (`\qty`, `\qtyrange`, `\ang`, `\num`, …)
- [ ] Diagrams are exported PDFs (drawn outside LaTeX), figures in the right folder
- [ ] Compiles locally: `latexmk -pdf main.tex`
- [ ] Screenshot of the changed section pasted above
