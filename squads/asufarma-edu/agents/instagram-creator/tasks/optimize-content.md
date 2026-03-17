---
task: optimize-content
agent: squads/asufarma-edu/agents/instagram-creator
order: 8
input:
  - feed_carousel (output of create-instagram-feed.md)
  - reels_script (output of create-instagram-reels.md)
  - stories_sequence (output of create-instagram-stories.md)
  - reviewer_feedback (optional: P2/P3 feedback from Vera, if revision cycle)
output:
  - optimized_content_package (YAML, final versions of all formats + cross-format consistency report)
---

## Process

1. **Cross-format consistency check.** Ensure the keyword CTA is the same word across feed caption, reels caption, and stories CTA frame (e.g., all use "SONO", not "SONO" in feed and "DORMIR" in stories). Verify the product name is identical in all three formats. Confirm the disclaimer is present in all non-dermocosmetico formats. Flag any inconsistency and fix it.

2. **Caption and copy polish.** Re-read every caption with fresh eyes. Apply final polish: (a) does the hook still feel fresh or did it become generic during drafting? (b) are there any filler words that can be cut? (c) is the hashtag block optimized — no duplicate hashtags across formats, mix of reach and niche tags? (d) is the blue heart 💙 signature present and in the right position (end of copy, before hashtags)? (e) character count verified and under 2200?

3. **Apply reviewer feedback if present.** If `reviewer_feedback` is provided (from a previous Vera review), process each P2 and P3 item systematically. Note each change made and confirm the P1 items were resolved (P1 fixes are mandatory and block delivery). Deliver a change log alongside the optimized package.

---

## Output Format

```yaml
optimized_content_package:
  topic: string
  product: string
  optimization_run: number           # 1 for first pass, 2+ for revision cycles
  consistency_report:
    keyword_cta_consistent: boolean
    keyword_used: string
    product_name_consistent: boolean
    disclaimer_present_all_formats: boolean
    issues_found: [string]           # list of issues found and fixed
  feed_carousel: object              # final version (same schema as create-instagram-feed output)
  reels_script: object               # final version (same schema as create-instagram-reels output)
  stories_sequence: object           # final version (same schema as create-instagram-stories output)
  change_log: [string] | null        # list of changes made, null if no reviewer feedback
  ready_for_review: boolean          # true when all P1 issues are resolved
```

## Output Example

```yaml
optimized_content_package:
  topic: "Probioticos e ansiedade: o que o seu intestino tem a ver com seu humor"
  product: "Corebiome"
  optimization_run: 1
  consistency_report:
    keyword_cta_consistent: true
    keyword_used: "INTESTINO"
    product_name_consistent: true
    disclaimer_present_all_formats: true
    issues_found:
      - "Stories frame 5 tinha versao abreviada do disclaimer — confirmado como aceitavel para stories por Pedro; mantido."
      - "Hashtag #probiotico aparecia tanto no feed quanto no reels caption — removido do reels para evitar duplicidade de indexacao."
  feed_carousel:
    topic: "Probioticos e ansiedade: o que o seu intestino tem a ver com seu humor"
    product: "Corebiome"
    disclaimer_required: true
    slides: [...]
    caption:
      hook_line: "90% da sua serotonina nao vem do seu cerebro. 🧠"
      body: "Ela vem do intestino. E quando o microbioma ta desequilibrado, o humor desequilibra junto..."
      keyword_cta: "Comente INTESTINO aqui embaixo e eu mando mais informacoes no seu direct. 👇"
      disclaimer: "Consulte seu medico, prescritor ou farmaceutico antes de iniciar qualquer suplementacao."
      signature: "💙"
      hashtags: "#saude #bemestar #microbioma #intestino #ansiedade #saudemental #farmaciamanipulacao #corebiome #salvador #bahia #soteropolitana #asufarma #saudebahia"
    char_count: 821
  reels_script: {...}
  stories_sequence: {...}
  change_log: null
  ready_for_review: true
```

## Quality Criteria

- Keyword CTA must be identical across all 3 formats before the package is marked `ready_for_review: true`
- Character count is re-verified in the optimized feed caption; any count over 2200 is a blocker
- If reviewer feedback was provided, every P2 and P3 item has a corresponding change_log entry

## Veto Conditions

- Package cannot be marked `ready_for_review: true` if any P1 feedback item from Vera is unresolved
- Package cannot be marked `ready_for_review: true` if `disclaimer_present_all_formats: false` for a non-dermocosmetico product
