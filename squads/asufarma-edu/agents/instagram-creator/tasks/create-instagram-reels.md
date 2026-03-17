---
task: create-instagram-reels
agent: squads/asufarma-edu/agents/instagram-creator
order: 6
input:
  - selected_angle (from content_angles, best_format: reels)
  - enriched_brief_story (the matching story from enriched_brief)
output:
  - reels_script (YAML, full spoken script + production notes + caption)
---

## Process

1. **Write the spoken script.** Structure: Hook (0-3s) — one sentence that creates an irresistible curiosity gap or challenges a belief, no greeting. Conflict/Curiosity build (3-12s) — deepen the tension, introduce the problem the audience recognizes from their own life. Content delivery (12-45s) — teach the core insight in conversational spoken language, simple vocabulary, one idea at a time. Product bridge (45-55s) — introduce Asufarma's product as the natural solution, not a hard sell. CTA (last 5s) — keyword trigger + where to find Asufarma. Total: 45-60 seconds at natural speaking pace.

2. **Write production notes.** For each script segment, add a visual production note: what should appear on screen (text overlays, b-roll suggestions, transitions, brand color accents). Notes should be specific enough for a creator or editor to execute. Reference Asufarma's palette and logo placement.

3. **Write the reels caption.** Reels captions are shorter than feed — 3-5 lines max before the "more" fold. Hook line first, brief body, keyword CTA, disclaimer if required, hashtags (10-12). No essays.

---

## Output Format

```yaml
reels_script:
  topic: string
  product: string
  disclaimer_required: boolean
  duration_estimate: string         # e.g., "50-55 segundos"
  segments:
    - segment: string               # hook | conflict | content | product_bridge | cta
      timecode: string              # e.g., "0s-3s"
      spoken_text: string           # exactly what is said
      production_note: string       # visual/editing instruction
  caption:
    hook_line: string
    body: string
    keyword_cta: string
    disclaimer: string | null
    signature: "💙"
    hashtags: string
  audio_suggestion: string | null   # trending audio or music mood suggestion
```

## Output Example

```yaml
reels_script:
  topic: "Melatonina gummie: o que acontece no seu corpo em cada hora da noite"
  product: "Melatonina Gummie"
  disclaimer_required: true
  duration_estimate: "50-55 segundos"
  segments:
    - segment: hook
      timecode: "0s-3s"
      spoken_text: "Voce toma melatonina mas provavelmente ta tomando na hora errada."
      production_note: "Close no rosto, luz natural, expressao de revelacao. Overlay de texto: 'HORA ERRADA' em turquesa #6dbfb8 com fonte bold."

    - segment: conflict
      timecode: "3s-12s"
      spoken_text: "A maioria das pessoas toma logo antes de dormir. Mas o seu corpo comeca a produzir melatonina 2 horas antes de voce sentir sono. Se voce ta esperando a cama pra tomar, provavelmente perdeu a janela ideal."
      production_note: "Corte rapido. Grafico simples de relogio aparecendo em overlay — 2h antes do horario de dormir marcado em verde oliva."

    - segment: content
      timecode: "12s-42s"
      spoken_text: "O ciclo circadiano funciona assim: quando a luz diminui, o seu cerebro manda sinal pro pineal liberar melatonina. Isso prepara o corpo pra cada fase do sono — sono leve, sono profundo, REM. Se voce interfere nesse timing, o sono fragmenta. Por isso a melatonina manipulada funciona melhor — a dose e ajustada ao seu perfil, nao uma dose generica de caixa."
      production_note: "Animacao simples das fases do sono (linhas em azul marinho e turquesa). Cortes a cada frase. Mantenha ritmo rapido — 1 corte por 4-5 segundos."

    - segment: product_bridge
      timecode: "42s-50s"
      spoken_text: "A Melatonina Gummie da Asufarma vem com a dose certa pra voce, gostosa, e sem aquele gosto amargo de capsula. Saude do seu jeito."
      production_note: "Produto em cena — mao segurando o frasco da Melatonina Gummie. Fundo bege #f5f2e8. Logo Asufarma aparece em fade."

    - segment: cta
      timecode: "50s-55s"
      spoken_text: "Quer o guia de horario ideal pra melatonina? Comenta SONO aqui embaixo."
      production_note: "Texto overlay grande: 'COMENTE SONO' em azul marinho sobre fundo turquesa. Sorriso direto pra camera."

  caption:
    hook_line: "Voce ta tomando melatonina na hora errada. ⏰"
    body: "O timing e tudo no ciclo circadiano. Assiste ate o fim pra entender o seu sono de verdade."
    keyword_cta: "Comente SONO e eu mando o guia de horario ideal no direct. 👇"
    disclaimer: "Consulte seu medico, prescritor ou farmaceutico antes de iniciar qualquer suplementacao."
    signature: "💙"
    hashtags: "#melatonina #sono #circadiano #qualidadedosono #farmaciamanipulacao #asufarma #salvador #bahia #suplementacao #bemestar"
  audio_suggestion: "Musica lo-fi instrumental suave OU trending audio relacionado a sono/relaxamento — verificar trending no momento da producao."
```

## Quality Criteria

- Hook segment is 3 seconds or fewer; spoken text is one sentence max
- Total script at natural speaking pace fits 45-60 seconds
- Production notes are specific: name colors by hex or name, specify overlay position, suggest transition type

## Veto Conditions

- Any script that opens with "Ola gente" or any greeting is rewritten before delivery
- If `disclaimer_required: true` and disclaimer is absent from caption, the output is rejected
