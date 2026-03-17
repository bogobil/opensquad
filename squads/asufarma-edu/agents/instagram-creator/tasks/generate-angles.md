---
task: generate-angles
agent: squads/asufarma-edu/agents/instagram-creator
order: 4
input:
  - enriched_brief (output of suggest-products.md)
output:
  - content_angles (YAML, 3 angle options per top story)
---

## Process

1. **Angle ideation.** For the top-ranked story in the enriched_brief, generate 3 distinct creative angles. Each angle must use a different content approach: (a) Educational myth-bust ("Voce acredita nisso sobre X? A ciencia diz o contrario"), (b) Story-first narrative (a relatable character in a Salvador scenario that mirrors the audience's life), (c) Meme educativo (a Brazilian internet format that packages the insight as shareable humor with real information).

2. **Format match.** For each angle, identify which Instagram format it fits best (feed carousel, reels, stories) and why. Some angles are inherently more visual/motion-oriented (reels) while others suit slide-by-slide teaching (carousel). Justify briefly.

3. **Hook stress test.** Write the hook sentence (slide 1 or first spoken word in reels) for each angle. Apply the scroll-stop test: would this make someone stop mid-scroll? Is the curiosity gap wide enough? Is it honest (not clickbait)? Reject and replace any hook that could be dismissed as obvious or sensationalist.

---

## Output Format

```yaml
content_angles:
  story_rank: number
  story_title: string
  angles:
    - angle_id: string              # e.g., "A1", "A2", "A3"
      approach: myth-bust | story-first | meme-educativo
      concept: string               # 2-3 sentences describing the angle
      hook: string                  # the exact first line/slide/spoken word
      best_format: carousel | reels | stories
      format_rationale: string      # 1 sentence why this format fits
      estimated_engagement: high | medium | low
      selected: boolean             # only one should be true after review
```

## Output Example

```yaml
content_angles:
  story_rank: 1
  story_title: "Probioticos e ansiedade: o que o seu intestino tem a ver com seu humor"
  angles:
    - angle_id: "A1"
      approach: myth-bust
      concept: "A maioria das pessoas acha que ansiedade e 'coisa da cabeca'. O carousel desmonta essa ideia mostrando que 90% da serotonina e produzida no intestino, nao no cerebro. O produto (Corebiome) aparece no ultimo slide como solucao natural e personalizada."
      hook: "90% da sua serotonina nao vem do seu cerebro."
      best_format: carousel
      format_rationale: "Dado surpreendente + explicacao em etapas = carousel com alto potencial de salvamento."
      estimated_engagement: high
      selected: true

    - angle_id: "A2"
      approach: story-first
      concept: "Mariana, 34 anos, Salvador. Faz yoga, toma cha, mas ainda sente aquela ansiedade de fundo que nao passa. O reels acompanha a jornada dela descobrindo que o problema estava no microbioma — e a solucao veio da Asufarma."
      hook: "Ela fazia tudo certo. Mas esqueceu do intestino."
      best_format: reels
      format_rationale: "Narrativa emocional funciona melhor em video — o rosto, o tom de voz, a jornada sao recursos de reels."
      estimated_engagement: high
      selected: false

    - angle_id: "A3"
      approach: meme-educativo
      concept: "Formato 'Eu tentando controlar minha ansiedade: respiracao, meditacao, caminhada na orla. Meu intestino: e eu, Jose?' Meme de reconhecimento que ensina o eixo intestino-cerebro de forma leve e compartilhavel."
      hook: "Eu: fiz tudo pra controlar a ansiedade. Meu intestino:"
      best_format: stories
      format_rationale: "Meme funciona bem em stories por ser rapido, visual, e facil de compartilhar no whatsapp de Salvador."
      estimated_engagement: medium
      selected: false
```

## Quality Criteria

- All 3 angles must use genuinely different approaches — no two can be variations of the same idea
- Every hook must be 10 words or fewer and must not start with "Voce sabia que" or "Hoje vamos falar"
- Exactly one angle is marked `selected: true` with a clear implication of being the production path

## Veto Conditions

- Any angle that requires a therapeutic claim ("trata ansiedade", "cura depressao") is vetoed before delivery
- Any hook that uses exaggeration or fear tactics ("isso esta DESTRUINDO sua saude") is rejected and replaced
