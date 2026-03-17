---
task: generate-feedback
agent: squads/asufarma-edu/agents/reviewer
order: 10
input:
  - content_scorecard (output of score-content.md)
  - optimized_content_package (the content being reviewed)
output:
  - feedback_report (YAML + human-readable summary for Lucas/Bogo)
---

## Process

1. **Structured feedback generation.** Convert the content_scorecard into an actionable feedback report. For each P1, P2, and P3 flag, write a specific fix instruction — not just "fix this" but "change THIS to THAT". Include the exact location (format, slide number, field name) and the proposed corrected text or direction. If the verdict is APROVADO, generate a brief celebration note and a learning capture (what worked well that should be replicated in future cycles).

2. **Human-readable summary.** Write a 5-10 line plain-text summary in Portuguese for Lucas (Marketing) and Bogo (Content). This summary should: state the verdict clearly, list the 1-3 things that need fixing (if any), and highlight what was done well. Tone is collegial — Vera is a trusted partner, not a gatekeeper. Format for easy WhatsApp sharing.

3. **Next-cycle recommendations.** Based on patterns observed in this review, suggest 1-2 improvements for the next production cycle. These are not fixes for the current content but structural learnings (e.g., "o meme educativo neste ciclo foi muito textual — tentar versao mais visual na proxima").

---

## Output Format

```yaml
feedback_report:
  topic: string
  verdict: APROVADO | APROVADO_COM_AJUSTES | REPROVADO
  total_score: number
  fix_instructions:
    p1: []                          # each item: {location, issue, fix_instruction}
    p2: []
    p3: []
  learning_capture: string | null   # what worked well, to replicate (only if APROVADO or APROVADO_COM_AJUSTES)
  next_cycle_recommendations: [string]
  human_summary: string             # plain text, 5-10 lines, Portuguese, for Lucas/Bogo
```

## Output Example

```yaml
feedback_report:
  topic: "Probioticos e ansiedade: o que o seu intestino tem a ver com seu humor"
  verdict: APROVADO_COM_AJUSTES
  total_score: 88
  fix_instructions:
    p1: []
    p2:
      - location: "feed_carousel > slides > slide_number: 4"
        issue: "Slide 4 tem duas ideias distintas em uma unica tela, tornando a leitura rapida dificil no mobile."
        fix_instruction: "Dividir em dois slides: slide 4a ('Quando o microbioma esta desequilibrado: ansiedade, irritabilidade, cansaco mental') e slide 4b ('Soa familiar?') com visual de pergunta e fundo turquesa #6dbfb8."
    p3:
      - location: "feed_carousel > slides > last_slide"
        issue: "CTA slide nao lista os enderecos das unidades — oportunidade de conversao presencial perdida."
        fix_instruction: "Adicionar no rodape do CTA slide: 'Center Lapa | SSA Shopping | Madison Plaza' em tipografia pequena, bege #f5f2e8 sobre fundo azul marinho."
      - location: "reels_script > audio_suggestion"
        issue: "Sugestao de audio esta generica — verificar trending audio na semana de publicacao para aumentar distribuicao organica."
        fix_instruction: "Lucas ou Bogo verificam trending audio no Instagram no dia do agendamento e aplicam na edicao. Genero musical sugerido esta correto (lo-fi/instrumental)."
  learning_capture: "O dado de abertura ('90% da serotonina vem do intestino') e um dos hooks mais fortes ja produzidos — a estrutura 'dado cientifico contraintuitivo + percentual especifico' deve ser replicada em futuros carousels de desmistificacao."
  next_cycle_recommendations:
    - "O meme educativo no formato stories funcionou bem conceitualmente mas ficou textual. Proxima vez: usar imagem de meme template real (ex: formato 'Drake pointing') com menos texto overlay e deixar o meme fazer o trabalho visual."
    - "Considerar criar um segundo reels curto (15-20s) exclusivamente de CTA — 'voce salvou o carousel? o link do Corebiome ta na bio' — para reforcar conversao 24h depois da publicacao principal."
  human_summary: |
    Oi Lucas, oi Bogo! 👋

    Conteudo do Corebiome foi pra revisao e saiu APROVADO COM AJUSTES — nota 88/100. Ta muito bom!

    Uma coisa pra corrigir antes de publicar (P2):
    - Slide 4 do carousel ta com duas ideias juntas. Sugestao: dividir em dois slides. Instrucao completa no feedback detalhado.

    Duas sugestoes opcionais (P3 — podem fazer se tiver tempo):
    - Adicionar enderecos das unidades no ultimo slide do carousel.
    - Confirmar audio trending na hora de editar o reels.

    O que ficou ótimo: o hook '90% da serotonina nao vem do cerebro' e um dos melhores que produzimos. Vale replicar essa estrutura.

    Asufarma. Saude e bem-estar do seu jeito. 💜
```

## Quality Criteria

- Every P1 and P2 fix instruction includes exact location, exact issue, and exact proposed fix — no ambiguity
- `human_summary` is 5-10 lines, readable on a phone screen, written for a non-technical marketing context
- `learning_capture` is present for any verdict of APROVADO or APROVADO_COM_AJUSTES

## Veto Conditions

- A feedback report with REPROVADO verdict that has no P1 fix instructions is invalid — REPROVADO requires at least one P1 flag
- A feedback report that lists P2 fixes without specific locations is rejected — vague feedback is not acceptable from Vera
