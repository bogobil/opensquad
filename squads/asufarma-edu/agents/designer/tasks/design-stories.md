---
task: design-stories
agent: squads/asufarma-edu/agents/designer
order: 2
input:
  - content-draft.md (stories frames section — copy + visual direction per frame)
output:
  - stories_designs (list of Canva design IDs + PNG export URLs, one per frame)
---

## Process

1. **Extract stories frames from the content draft.** Load `squads/asufarma-edu/output/content-draft.md` and navigate to the stories section. Identify each frame: frame number, copy/overlay text, interactive element (poll, question sticker, swipe-up CTA), background direction, and mood.

2. **Generate each stories frame in Canva.** For EACH frame, call `canva:generate-design` with:
   - `design_type`: `"your_story"`
   - `brand_kit_id`: `"kAG4986LZbc"`
   - `query`: Compose a detailed prompt with the frame copy, overlay text position, interactive element placement, background direction (color, gradient, or lifestyle scene), Asufarma brand palette reference, and any grafismo pattern as edge accent. Stories have vertical composition — queries must specify 9:16 aspect ratio elements.
   Auto-select the FIRST candidate unless it renders text illegibly or uses off-brand colors. In those cases, select the next candidate or regenerate with a more specific query.

3. **Create and export each frame.** Call `canva:create-design-from-candidate` to save to the Canva account. Then call `canva:export-design` with format `"png"` and dimensions `1080x1920`. Confirm export URL accessibility before logging as complete.

4. **Log all outputs.** Compile the structured list: frame number, Canva design ID, export URL, interactive element type, and any deviation from the draft's visual direction.

## Output Format

```yaml
stories_designs:
  topic: string
  total_frames: number
  brand_kit_id: "kAG4986LZbc"
  frames:
    - frame_number: number
      canva_design_id: string
      export_url: string
      dimensions: "1080x1920"
      interactive_element: string | null   # "poll", "question_sticker", "cta_swipe", null
      visual_direction_applied: string
      deviation_note: string | null
```

## Output Example

```yaml
stories_designs:
  topic: "Magnésio e TPM: por que sua suplementação pode estar errada"
  total_frames: 4
  brand_kit_id: "kAG4986LZbc"
  frames:
    - frame_number: 1
      canva_design_id: "DAGxxxxxST01"
      export_url: "https://export.canva.com/png/DAGxxxxxST01/story1.png"
      dimensions: "1080x1920"
      interactive_element: null
      visual_direction_applied: "Fundo turquesa #6dbfb8 com grafismo de cápsulas e folhas nas bordas, texto hook centralizado em azul marinho bold, logo monograma A+F no topo"
      deviation_note: null

    - frame_number: 2
      canva_design_id: "DAGxxxxxST02"
      export_url: "https://export.canva.com/png/DAGxxxxxST02/story2.png"
      dimensions: "1080x1920"
      interactive_element: "poll"
      visual_direction_applied: "Fundo bege #f5f2e8, pergunta de enquete em azul marinho, espaço reservado para sticker de poll no terço inferior, ilustração de molécula em verde oliva"
      deviation_note: null

    - frame_number: 3
      canva_design_id: "DAGxxxxxST03"
      export_url: "https://export.canva.com/png/DAGxxxxxST03/story3.png"
      dimensions: "1080x1920"
      interactive_element: "question_sticker"
      visual_direction_applied: "Fundo azul marinho #073263, texto educativo em branco, espaço para question sticker centralizado, grafismo de pestle e frasco em bege como textura"
      deviation_note: null

    - frame_number: 4
      canva_design_id: "DAGxxxxxST04"
      export_url: "https://export.canva.com/png/DAGxxxxxST04/story4.png"
      dimensions: "1080x1920"
      interactive_element: "cta_swipe"
      visual_direction_applied: "Fundo verde oliva #96b472, texto CTA em branco bold, seta animável para swipe up, logo Asufarma horizontal centralizado, endereço da unidade mais próxima no rodapé"
      deviation_note: "Swipe-up substituído por Link Sticker — formato mais adequado ao tipo de conta"
```

## Quality Criteria

- Every frame has a confirmed `canva_design_id` AND `export_url` at 1080x1920 — no null values
- Interactive element type logged for each frame (null if static) so the poster knows which sticker to add in-app
- Visual composition respects vertical 9:16 format — no elements cut off at portrait edges

## Veto Conditions

- If any frame export URL is inaccessible, retry the export before delivering — do not log a broken URL as complete output
- If text is illegible due to background contrast in the generated design, regenerate with explicit contrast instruction before accepting the candidate
