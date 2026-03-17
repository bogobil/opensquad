---
task: rank-stories
agent: squads/asufarma-edu/agents/researcher
order: 2
input:
  - raw_topics (output of find-news.md)
  - squad_cycle_history (optional: list of topics produced in last 4 cycles to avoid repetition)
output:
  - ranked_brief (YAML, top 5 stories with full metadata)
---

## Process

1. **Score each topic.** Apply a weighted scoring matrix to each topic from `raw_topics`. Dimensions: (a) Timeliness (is this trending NOW or is it evergreen? trending = +3, evergreen = +1), (b) Brand fit (does it connect naturally to Asufarma's catalog? direct product tie = +3, adjacent = +1), (c) Engagement potential (does it challenge a myth, teach a surprising fact, or invite interaction? high = +3, medium = +1), (d) Competitor white space (low competitor coverage = +2, high = 0), (e) Salvador cultural relevance (clear SSA hook = +2, generic = 0). Sum scores, normalize to 0-10.

2. **Repetition filter.** If `squad_cycle_history` is provided, any topic overlapping thematically with the last 2 cycles (same ingredient or same health category) is penalized -2 from its score. Identical topics are removed entirely.

3. **Select and enrich top 5.** Take the top 5 scoring topics. For each, write an expanded brief: what is the core insight, why it matters to Asufarma's audience in Salvador, what emotional or informational angle is most promising for Instagram, and which product family it connects to. Assign a final priority rank (1 = highest priority for production).

---

## Output Format

```yaml
ranked_brief:
  generated_at: string           # ISO date
  cycle_note: string             # brief note on what was filtered or boosted and why
  stories:
    - rank: number               # 1-5
      title: string
      core_insight: string       # 2-3 sentences: what the audience will learn
      emotional_angle: string    # the feeling or tension this content taps into
      salvador_hook: string | null
      product_family: string     # Asufarma product family or ingredient category
      source_url: string
      final_score: number        # 0-10
      recommended_format: carousel | reels | stories | blog_post
      urgency: hot | warm | cold
```

## Output Example

```yaml
ranked_brief:
  generated_at: "2026-03-16"
  cycle_note: "Topico sobre proteina whey removido por sobreposicao com ciclo anterior. Creatina rebaixada para rank 4 por alta cobertura concorrente. Corebiome promovido por white space e relevancia sazonal."
  stories:
    - rank: 1
      title: "Probioticos e ansiedade: o que o seu intestino tem a ver com seu humor"
      core_insight: "O eixo intestino-cerebro e hoje uma das areas mais ativas da neurociencia. Bacteria especificas do microbioma produzem precursores de serotonina. Corebiome (postbiotico) tem perfil diferenciado nesse contexto."
      emotional_angle: "Ansiedade e um tema universal em Salvador pos-pandemia. Dar ao publico uma explicacao biologica — e uma solucao manipulada — gera salvamentos e compartilhamentos."
      salvador_hook: "Ritmo acelerado de SSA em periodo de preparacao pro Sao Joao — estresse sazonal alto"
      product_family: "Corebiome (postbiotico)"
      source_url: "https://www.sciencedirect.com/science/article/pii/S0149763421001780"
      final_score: 9.2
      recommended_format: carousel
      urgency: warm

    - rank: 2
      title: "Melatonina gummie: o que acontece no seu corpo em cada hora da noite"
      core_insight: "A maioria das pessoas toma melatonina sem entender as fases do sono em que ela age. Visualizar o ciclo cronobiologico e altamente educativo e gera salvamentos."
      emotional_angle: "Curiosidade sobre o proprio corpo — 'eu nao sabia que era assim' e o gatilho de compartilhamento mais forte no Instagram de saude."
      salvador_hook: "Pos-Carnaval: Salvador voltando ao ritmo, ciclo de sono desregulado"
      product_family: "Melatonina Gummie"
      source_url: "https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6859545/"
      final_score: 8.8
      recommended_format: carousel
      urgency: hot
```

## Quality Criteria

- Top 5 stories span at least 3 different product families (no single product dominates)
- Every story has a clear `emotional_angle` — this is required, not optional
- The `cycle_note` explains all filtering decisions transparently

## Veto Conditions

- A story with `confidence: low` from find-news.md cannot rank above position 3 without an explicit note explaining why
- If all top 5 stories map to the same product family, the ranking must be rebalanced before delivery
