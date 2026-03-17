---
task: compile-post-package
agent: squads/asufarma-edu/agents/designer
order: 3
input:
  - content-draft.md (caption, hashtags, reel script, disclaimer status)
  - carousel_designs output (from design-carousel task)
  - stories_designs output (from design-stories task)
output:
  - post-package.md (complete ready-to-post package)
  outputFile: squads/asufarma-edu/output/post-package.md
---

## Process

1. **Gather all inputs.** Confirm that both previous tasks are complete: `carousel_designs` list has a PNG export URL for every slide, and `stories_designs` list has a PNG export URL for every frame. Load `squads/asufarma-edu/output/content-draft.md` to extract: caption text, hashtags, reel script, and disclaimer status.

2. **Verify disclaimer compliance.** If `disclaimer_required: true` in the content draft, confirm the disclaimer text ("Consulte seu medico, prescritor ou farmaceutico.") is present in the caption. If missing, add it before the hashtag block. Log this check explicitly in the post package.

3. **Assemble the post-package.md file.** Write a clean, copy-paste-ready document structured as:
   - Section 1: Carousel Slides (numbered list of PNG URLs + Canva design IDs in posting order)
   - Section 2: Caption (complete text ready to paste into Instagram — includes hook, body, keyword CTA, disclaimer if required, 💙 signature, hashtags)
   - Section 3: Stories Frames (numbered list of PNG URLs + interactive element instructions per frame)
   - Section 4: Reel Script (formatted for reading aloud — timestamps, pacing cues)
   - Section 5: Compliance Check (disclaimer confirmed or noted as not required, with reason)
   - Section 6: Design Notes (brief summary of any deviations from visual direction, for team reference)

4. **Save and confirm.** Write the compiled document to `squads/asufarma-edu/output/post-package.md`. Confirm the file was saved successfully and report the file path as the primary output.

## Output Format

```markdown
# Post Package — [Tema] — [Data]

**Status:** ✅ Pronto para publicar
**Squad:** Asufarma Edu
**Designer:** Diana Design 💙

---

## 1. Carrossel — [X] Slides

| Slide | Canva ID | PNG Export |
|-------|----------|------------|
| 1 | [ID] | [URL] |
| ... | ... | ... |

---

## 2. Caption (pronta para copiar)

[texto completo da legenda — hook, corpo, CTA, disclaimer, 💙, hashtags]

**Contagem de caracteres:** [X] / 2200

---

## 3. Stories — [X] Frames

| Frame | Canva ID | PNG Export | Elemento Interativo |
|-------|----------|------------|---------------------|
| 1 | [ID] | [URL] | [tipo ou "—"] |
| ... | ... | ... | ... |

---

## 4. Script do Reel

[script formatado com timestamps e cues de leitura]

---

## 5. Checklist de Compliance

- [ ] Disclaimer presente: [SIM / NÃO NECESSÁRIO — [motivo]]
- [ ] Keyword CTA confirmado: [PALAVRA]
- [ ] Produto mencionado corretamente: [nome exato]
- [ ] Brand kit aplicado: kAG4986LZbc

---

## 6. Notas de Design

[lista de desvios do visual direction, se houver — ou "Nenhum desvio. Visual direction aplicada integralmente."]
```

## Output Example

```markdown
# Post Package — Magnésio e TPM — 2026-03-16

**Status:** ✅ Pronto para publicar
**Squad:** Asufarma Edu
**Designer:** Diana Design 💙

---

## 1. Carrossel — 8 Slides

| Slide | Canva ID | PNG Export |
|-------|----------|------------|
| 1 | DAGxxxxxABC1 | https://export.canva.com/png/DAGxxxxxABC1/slide1.png |
| 2 | DAGxxxxxABC2 | https://export.canva.com/png/DAGxxxxxABC2/slide2.png |
| 3 | DAGxxxxxABC3 | https://export.canva.com/png/DAGxxxxxABC3/slide3.png |
| 4 | DAGxxxxxABC4 | https://export.canva.com/png/DAGxxxxxABC4/slide4.png |
| 5 | DAGxxxxxABC5 | https://export.canva.com/png/DAGxxxxxABC5/slide5.png |
| 6 | DAGxxxxxABC6 | https://export.canva.com/png/DAGxxxxxABC6/slide6.png |
| 7 | DAGxxxxxABC7 | https://export.canva.com/png/DAGxxxxxABC7/slide7.png |
| 8 | DAGxxxxxABC8 | https://export.canva.com/png/DAGxxxxxABC8/slide8.png |

---

## 2. Caption (pronta para copiar)

Você escolheu o magnésio errado. 🧲

Não é culpa sua — a maioria das pessoas compra óxido de magnésio porque é barato e está em todo lugar. Mas absorção de 4%? Isso é quase nada.

Para TPM, cólicas e humor em colapso, o que funciona é o magnésio bisglicinato: quelado, absorção acima de 80%, sem laxante como efeito colateral.

A Asufarma manipula no formato certo, na dose certa, pra você.

Comenta MAGNÉSIO aqui embaixo e a gente manda mais no seu direct. 👇

Consulte seu médico, prescritor ou farmacêutico antes de iniciar qualquer suplementação.

💙 #saude #magnesio #tpm #saudefeminina #suplementacao #farmaciamanipulacao #manipulacao #bisglicinato #hormonios #bemestar #salvador #bahia #soteropolitana #asufarma #saudebahia

**Contagem de caracteres:** 712 / 2200

---

## 3. Stories — 4 Frames

| Frame | Canva ID | PNG Export | Elemento Interativo |
|-------|----------|------------|---------------------|
| 1 | DAGxxxxxST01 | https://export.canva.com/png/DAGxxxxxST01/story1.png | — |
| 2 | DAGxxxxxST02 | https://export.canva.com/png/DAGxxxxxST02/story2.png | Poll |
| 3 | DAGxxxxxST03 | https://export.canva.com/png/DAGxxxxxST03/story3.png | Question Sticker |
| 4 | DAGxxxxxST04 | https://export.canva.com/png/DAGxxxxxST04/story4.png | Link Sticker → carrossel |

---

## 4. Script do Reel

[0-3s — HOOK] "O magnésio que você tá tomando pode não estar fazendo nada."
[3-6s — CONFLITO] "Sabe por quê? Absorção. Óxido de magnésio: 4%. Bisglicinato: 80%."
[6-20s — CONTEÚDO] "TPM, cólica, humor — tudo isso tem conexão com o magnésio intracelular. E a forma importa muito mais do que a dose."
[20-30s — SOLUÇÃO] "Na Asufarma a gente manipula magnésio bisglicinato no formato que o seu corpo absorve de verdade."
[30-35s — CTA] "Comenta MAGNÉSIO aqui embaixo. A gente te manda tudo no direct. 💙"

---

## 5. Checklist de Compliance

- [x] Disclaimer presente: SIM — adicionado antes dos hashtags
- [x] Keyword CTA confirmado: MAGNÉSIO
- [x] Produto mencionado corretamente: Magnésio Bisglicinato Asufarma
- [x] Brand kit aplicado: kAG4986LZbc

---

## 6. Notas de Design

- Slide 3: Fundo alterado de bege para turquesa — melhor legibilidade para slide com texto denso
- Slide 6: Foto lifestyle gerada via mcp-image (sem stock adequado disponível no Canva)
- Stories Frame 4: Swipe-up substituído por Link Sticker (mais adequado ao tipo de conta)
```

## Quality Criteria

- All carousel slide URLs and stories frame URLs confirmed accessible before including in package
- Caption character count verified and displayed alongside 2200 limit
- Disclaimer check explicitly listed in Section 5 — either "SIM" with confirmation, or "NÃO NECESSÁRIO" with reason

## Veto Conditions

- If carousel or stories outputs have any missing URLs (null or broken), return to the respective design task to complete before assembling the package
- If disclaimer is required but missing from caption, add it before finalizing the package — do not deliver a package with a missing disclaimer
