---
task: create-instagram-stories
agent: squads/asufarma-edu/agents/instagram-creator
order: 7
input:
  - feed_carousel or reels_script (the produced content for the same topic)
  - enriched_brief_story
output:
  - stories_sequence (YAML, 4-6 frame sequence)
---

## Process

1. **Design the sequence flow.** Stories are a fast-scroll vertical experience. Each frame has one job. Plan a 4-6 frame sequence: Frame 1 (attention hook — teases the carousel/reel), Frames 2-3 (quick education — one fact or stat per frame), Frame 4 (interactive — poll, quiz, or question sticker to drive engagement), Frame 5 (product frame — benefit + soft CTA), Frame 6 optional (swipe-up link or "DM us" frame). Stories support the feed/reels post — they are not standalone replacements.

2. **Write frame copy.** Stories copy is ultra-short: 5-10 words per frame maximum. The visual does the heavy lifting. Write what appears as text overlay. For interactive frames, write the poll question and both answer options, or the quiz question with correct answer flagged.

3. **Write visual directions.** Each frame needs a specific visual direction: background (solid Asufarma color or photo), text overlay position and style, sticker type (poll, quiz, question, countdown), and any animation suggestion (fade, bounce, draw). Reference brand palette explicitly.

---

## Output Format

```yaml
stories_sequence:
  topic: string
  product: string
  disclaimer_required: boolean
  frames:
    - frame_number: number
      type: hook | education | interactive | product | cta
      copy: string                    # text overlay, max 10 words
      visual_direction: string        # specific design instruction
      sticker: poll | quiz | question | countdown | none
      sticker_content:                # only if sticker != none
        question: string
        options: [string, string]     # for poll/quiz
        correct_answer: string | null # for quiz only
      disclaimer_note: string | null  # reminder if this frame needs disclaimer
```

## Output Example

```yaml
stories_sequence:
  topic: "Probioticos e ansiedade: o que o seu intestino tem a ver com seu humor"
  product: "Corebiome"
  disclaimer_required: true
  frames:
    - frame_number: 1
      type: hook
      copy: "90% da sua serotonina nao vem do cerebro 🤯"
      visual_direction: "Fundo azul marinho #073263. Texto grande branco centralizado. GIF ou animacao de cerebro com ponto de interrogacao. Logo Asufarma no topo. Mood: chocante mas elegante."
      sticker: none
      sticker_content: null
      disclaimer_note: null

    - frame_number: 2
      type: education
      copy: "Ela vem do seu intestino. Sério."
      visual_direction: "Fundo bege #f5f2e8. Ilustracao de intestino estilizado em verde oliva. Texto em azul marinho bold. Animacao de texto aparecendo letra por letra (typewriter)."
      sticker: none
      sticker_content: null
      disclaimer_note: null

    - frame_number: 3
      type: interactive
      copy: "Voce ja ouviu falar do eixo intestino-cerebro?"
      visual_direction: "Fundo turquesa #6dbfb8. Texto em branco. Poll sticker centralizado. Mood descontraido — esse frame e sobre engajamento."
      sticker: poll
      sticker_content:
        question: "Voce ja ouviu falar do eixo intestino-cerebro?"
        options: ["Sim, claro! 🧠", "Primeira vez 👀"]
        correct_answer: null
      disclaimer_note: null

    - frame_number: 4
      type: education
      copy: "Microbioma desequilibrado = ansiedade, irritabilidade, cansaco mental"
      visual_direction: "Fundo bege. Tres icones em linha (cerebro, raio, bateria) em verde oliva. Texto pequeno em azul marinho. Animacao de icones aparecendo em sequencia."
      sticker: none
      sticker_content: null
      disclaimer_note: null

    - frame_number: 5
      type: product
      copy: "Corebiome: equilibrio do microbioma. Do seu jeito. 💙"
      visual_direction: "Foto do produto Corebiome em destaque. Fundo bege. Badge 'Manipulacao Personalizada' em verde oliva. Logo Asufarma. Texto do slogan em azul marinho pequeno no rodape."
      sticker: none
      sticker_content: null
      disclaimer_note: "Incluir texto micro no rodape: 'Consulte seu farmaceutico.' (versao abreviada para stories)"

    - frame_number: 6
      type: cta
      copy: "Comenta INTESTINO no nosso feed e recebe no direct 👇"
      visual_direction: "Fundo azul marinho. Seta animada apontando para baixo. Texto turquesa bold. Perfil @asufarma_manipulacao em destaque. Link sticker se disponivel."
      sticker: none
      sticker_content: null
      disclaimer_note: null
```

## Quality Criteria

- Every sequence has at least one interactive frame (poll, quiz, or question sticker)
- No frame copy exceeds 10 words; visual direction carries the teaching load
- CTA in final frame reinforces the keyword from the feed post caption for cross-format consistency

## Veto Conditions

- A product frame for a non-dermocosmetico product without any disclaimer reference (even abbreviated) is rejected
- Stories with 3 or fewer frames are rejected — minimum sequence is 4 frames
