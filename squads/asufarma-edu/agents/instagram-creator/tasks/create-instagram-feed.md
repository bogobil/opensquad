---
task: create-instagram-feed
agent: squads/asufarma-edu/agents/instagram-creator
order: 5
input:
  - selected_angle (from content_angles, selected: true)
  - enriched_brief_story (the matching story from enriched_brief)
output:
  - feed_carousel (YAML, full carousel script + caption + hashtags)
---

## Process

1. **Build the slide sequence.** Structure the carousel as: Slide 1 (hook — one bold statement, zero context), Slides 2-5 (body — one idea per slide, max 2 short sentences + visual direction), Slide 6-7 (product introduction — benefit-first, then soft CTA), Last slide (CTA slide — keyword trigger + disclaimer if required). Total: 6-8 slides. Each slide has copy and a visual direction note in Asufarma brand palette.

2. **Write the caption.** Open with the hook (same as Slide 1 or a variation). Add 3-5 lines of body context that expand on the topic with warmth and specificity. Write the keyword CTA ("Comente [PALAVRA] e eu mando no direct"). Add the disclaimer if required (non-dermocosmetico). Close with blue heart 💙 and hashtag block.

3. **Hashtag strategy.** Include 12-15 hashtags in two tiers: (a) broad audience reach (#saude #bemestar #suplementacao #farmaciamanipulacao), (b) Salvador/Bahia localization (#salvador #bahia #soteropolitana #saudebahia), (c) topic-specific (#melatonina #sono #circadiano — match the content). Never repeat hashtags from the previous post.

---

## Output Format

```yaml
feed_carousel:
  topic: string
  product: string
  disclaimer_required: boolean
  slides:
    - slide_number: number
      copy: string                  # text on the slide
      visual_direction: string      # design instruction with colors, mood, elements
  caption:
    hook_line: string
    body: string
    keyword_cta: string             # "Comente [PALAVRA] e eu mando no direct"
    disclaimer: string | null
    signature: "💙"
    hashtags: string                # space-separated hashtag block
  char_count: number                # total caption character count (must be <= 2200)
```

## Output Example

```yaml
feed_carousel:
  topic: "Probioticos e ansiedade: o que o seu intestino tem a ver com seu humor"
  product: "Corebiome"
  disclaimer_required: true
  slides:
    - slide_number: 1
      copy: "90% da sua serotonina nao vem do seu cerebro."
      visual_direction: "Fundo azul marinho #073263. Texto grande, branco, centralizado. Sem imagem — so tipografia bold. Logo Asufarma pequeno no canto inferior direito."

    - slide_number: 2
      copy: "Ela vem do seu intestino. E se o seu intestino nao esta bem, o seu humor tambem nao vai estar."
      visual_direction: "Fundo bege #f5f2e8. Ilustracao minimalista de intestino em verde oliva #96b472. Texto em azul marinho. Mood: cientifico mas acessivel."

    - slide_number: 3
      copy: "Isso se chama eixo intestino-cerebro. Bilhoes de bacterias no seu gut se comunicam direto com o seu sistema nervoso."
      visual_direction: "Fundo turquesa #6dbfb8 suave. Diagrama simples mostrando conexao intestino-cerebro. Icone de bacteria estilizado. Texto branco."

    - slide_number: 4
      copy: "Quando esse microbioma esta desequilibrado: ansiedade, irritabilidade, cansaco mental. Soa familiar?"
      visual_direction: "Fundo bege. Tres icones simples: cabeca + raio (ansiedade), rosto (irritabilidade), bateria vazia (cansaco). Verde oliva e azul marinho."

    - slide_number: 5
      copy: "A boa noticia: da pra cuidar disso com suplementacao direcionada e personalizada."
      visual_direction: "Fundo verde oliva #96b472. Texto branco bold. Mood: solucao, otimismo. Seta simples apontando para o proximo slide."

    - slide_number: 6
      copy: "Corebiome: o postbiotico que apoia o equilibrio do seu microbioma — e do seu humor. Manipulado do seu jeito na Asufarma."
      visual_direction: "Foto ou render do produto Corebiome. Fundo bege. Nome do produto em destaque em azul marinho. Badge 'Manipulacao Personalizada'."

    - slide_number: 7
      copy: "Quer saber se o Corebiome e pra voce? Comente INTESTINO no direct. 💙"
      visual_direction: "CTA slide. Fundo azul marinho. Texto turquesa e branco. Logo Asufarma centralizado. Endereco das unidades no rodape (Center Lapa, SSA Shopping, Madison Plaza)."

  caption:
    hook_line: "90% da sua serotonina nao vem do seu cerebro. 🧠"
    body: "Ela vem do intestino. E quando o microbioma ta desequilibrado, o humor desequilibra junto — ansiedade, irritabilidade, aquele cansaco mental que nao passa.\n\nIsso tem nome: eixo intestino-cerebro. E tem solucao.\n\nO Corebiome e um postbiotico manipulado na Asufarma que apoia o equilibrio do seu microbioma de forma personalizada. Porque saude e bem-estar do seu jeito. ✨"
    keyword_cta: "Comente INTESTINO aqui embaixo e eu mando mais informacoes no seu direct. 👇"
    disclaimer: "Consulte seu medico, prescritor ou farmaceutico antes de iniciar qualquer suplementacao."
    signature: "💙"
    hashtags: "#saude #bemestar #microbioma #intestino #probioticos #ansiedade #saudemental #farmaciamanipulacao #manipulacao #corebiome #salvador #bahia #soteropolitana #asufarma #saudebahia"
  char_count: 847
```

## Quality Criteria

- Slide count is between 6 and 8; no slide exceeds 2 short sentences of body copy
- Caption character count is verified and must not exceed 2200
- Keyword CTA uses a single uppercase word ("INTESTINO", "SONO", "CREATINA") — never a phrase

## Veto Conditions

- If `disclaimer_required: true` and the disclaimer field is null or empty, the task output is rejected before delivery to Vera
- If the caption opens with "Ola pessoal" or "Hoje vamos falar sobre", the caption is rewritten before delivery
