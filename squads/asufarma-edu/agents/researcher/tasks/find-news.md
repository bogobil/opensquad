---
task: find-news
agent: squads/asufarma-edu/agents/researcher
order: 1
input:
  - current_date
  - seasonal_context (month, upcoming holidays, Salvador calendar events)
  - optional: topic_seed (user-provided keyword to bias search)
output:
  - raw_topics_list (YAML array, 8-12 items)
---

## Process

1. **Trend scan.** Search for health, wellness, and nutrition topics trending in Brazil in the current week. Prioritize: Instagram Reels trending audio themes, Google Trends BR health category, recent peer-reviewed publications covered by Brazilian health media (Drauzio Varella, Sempre Questione, VEJA Saude, SBEM news). Use `web_search` with queries like "tendencias saude bem-estar Brasil [current_month] [current_year]" and "suplementacao nutricional novidades [current_year]".

2. **Regulatory and seasonal cross-check.** For each candidate topic, fetch ANVISA bulletins or CFF news to confirm the topic is content-safe. Apply Salvador/BA seasonal lens: is this topic amplified by current weather, upcoming holidays, Carnaval season, school year, or summer/winter cycle? Boost topics that have a natural Salvador hook. Use `web_fetch` for ANVISA RSS or official bulletins when a topic has regulatory sensitivity.

3. **Competitor gap check.** Search recent @pharmapele and similar pharmacy Instagram accounts (via public web search) to identify what topics have been heavily covered recently. Deprioritize saturated topics; flag white-space opportunities — topics the reference accounts have NOT covered that Asufarma could own.

---

## Output Format

```yaml
raw_topics:
  - title: string                  # punchy topic title, max 8 words
    summary: string                # 2-3 sentences describing the topic
    source_url: string             # primary source URL
    source_type: string            # journal | health_media | anvisa | trend_signal
    seasonal_hook: string | null   # specific Salvador/BA seasonal angle, if applicable
    competitor_coverage: low | medium | high
    confidence: high | medium | low
    suggested_format: carousel | reels | stories | blog_post
    raw_score: number              # 1-10, preliminary (before rank-stories)
```

## Output Example

```yaml
raw_topics:
  - title: "Melatonina nao e so pra dormir"
    summary: "Pesquisas recentes mostram que a melatonina tem papel antioxidante e imunomodulador alem do ciclo circadiano. O publico leigo desconhece esses efeitos secundarios, abrindo espaco para conteudo educativo diferenciado."
    source_url: "https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6859545/"
    source_type: journal
    seasonal_hook: "Pos-Carnaval: recuperacao do ciclo de sono apos dias de festas"
    competitor_coverage: medium
    confidence: high
    suggested_format: carousel
    raw_score: 8

  - title: "Probioticos e saude mental: o eixo intestino-cerebro"
    summary: "Estudos do eixo gut-brain mostram que o microbioma influencia humor, ansiedade e foco. Tema em ascensao no Brasil com destaque para postbioticos como Corebiome."
    source_url: "https://www.sciencedirect.com/science/article/pii/S0149763421001780"
    source_type: journal
    seasonal_hook: null
    competitor_coverage: low
    confidence: high
    suggested_format: carousel
    raw_score: 9

  - title: "Creatina nao engorda — desmistificando"
    summary: "Mito persistente de que creatina causa retencao de gordura. Conteudo com alto potencial de compartilhamento por contradizer crenca popular com evidencia."
    source_url: "https://jissn.biomedcentral.com/articles/10.1186/s12970-017-0173-z"
    source_type: journal
    seasonal_hook: "Inicio de ano: resolucoes fitness, academia lotada em Salvador"
    competitor_coverage: high
    confidence: high
    suggested_format: reels
    raw_score: 7
```

## Quality Criteria

- Minimum 8 topics delivered; no topic included without a source URL
- At least 3 topics must have a specific Salvador/BA seasonal or cultural hook
- At least 1 topic must represent a white-space opportunity (competitor_coverage: low)

## Veto Conditions

- Any topic whose primary source is a tabloid, influencer post, or AI-generated article without peer review backing is excluded
- Any topic that would require a therapeutic claim Asufarma is not licensed to make (e.g., "trata depressao") is excluded before delivery
