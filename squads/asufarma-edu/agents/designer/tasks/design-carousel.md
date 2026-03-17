---
task: design-carousel
agent: squads/asufarma-edu/agents/designer
order: 1
input:
  - content-draft.md (carousel slides section — copy + visual direction per slide)
output:
  - carousel_designs (list of Canva design IDs + PNG export URLs, one per slide)
---

## Process

1. **Read the approved content draft.** Load `squads/asufarma-edu/output/content-draft.md` and extract the carousel slides section. For each slide, capture: slide number, copy text, and visual direction note. Note whether `disclaimer_required` is true.

2. **Generate each slide in Canva.** For EACH slide, call `canva:generate-design` with:
   - `design_type`: `"instagram_post"`
   - `brand_kit_id`: `"kAG4986LZbc"`
   - `query`: Compose a detailed prompt combining the slide copy text, visual direction from the draft (dominant color, mood, composition, graphic elements), Asufarma brand palette reference, and typography instruction (Raleway for body, Avenue for titles). Include grafismo elements as background texture when the visual direction calls for it.
   Auto-select the FIRST candidate returned unless it violates brand palette or renders text illegibly. In that case, select the next available candidate.

3. **Create and export each design.** For each accepted candidate, call `canva:create-design-from-candidate` to save the design to the Asufarma Canva account. Then call `canva:export-design` with format `"png"` and dimensions `1080x1080` (or `1080x1350` if the visual direction specifies portrait). Confirm the export URL is accessible before logging it as complete.

4. **Handle lifestyle photo needs.** If any slide's visual direction calls for a real lifestyle photograph and no suitable Canva stock image matches the description, generate the image using `mcp-image` with a detailed prompt matching Asufarma's aesthetic (warm natural light, health/beauty context, Salvador/Bahia color warmth). Upload the generated image to Canva before running `generate-design` for that slide.

5. **Log all outputs.** Compile a structured list of all slide results: slide number, Canva design ID, export URL, and dimensions. Flag any slide where the final design deviated from the original visual direction, with a brief note explaining why.

## Output Format

```yaml
carousel_designs:
  topic: string
  total_slides: number
  brand_kit_id: "kAG4986LZbc"
  slides:
    - slide_number: number
      canva_design_id: string
      export_url: string
      dimensions: "1080x1080" | "1080x1350"
      visual_direction_applied: string   # brief note on what was executed
      deviation_note: string | null      # if design differs from draft direction
```

## Output Example

```yaml
carousel_designs:
  topic: "Magnésio e TPM: por que sua suplementação pode estar errada"
  total_slides: 8
  brand_kit_id: "kAG4986LZbc"
  slides:
    - slide_number: 1
      canva_design_id: "DAGxxxxxABC1"
      export_url: "https://export.canva.com/png/DAGxxxxxABC1/slide1.png"
      dimensions: "1080x1080"
      visual_direction_applied: "Fundo azul marinho #073263, tipografia Raleway bold branca centralizada, sem imagem, logo horizontal Asufarma no canto inferior direito"
      deviation_note: null

    - slide_number: 2
      canva_design_id: "DAGxxxxxABC2"
      export_url: "https://export.canva.com/png/DAGxxxxxABC2/slide2.png"
      dimensions: "1080x1080"
      visual_direction_applied: "Fundo bege #f5f2e8, ilustração minimalista de célula muscular em verde oliva #96b472, texto em azul marinho, mood científico-acessível"
      deviation_note: null

    - slide_number: 3
      canva_design_id: "DAGxxxxxABC3"
      export_url: "https://export.canva.com/png/DAGxxxxxABC3/slide3.png"
      dimensions: "1080x1080"
      visual_direction_applied: "Fundo turquesa #6dbfb8 — desvio: draft pedia bege, mas contraste com texto branco ficou superior no turquesa para este slide denso em texto"
      deviation_note: "Fundo alterado de bege para turquesa para melhor legibilidade"

    - slide_number: 4
      canva_design_id: "DAGxxxxxABC4"
      export_url: "https://export.canva.com/png/DAGxxxxxABC4/slide4.png"
      dimensions: "1080x1080"
      visual_direction_applied: "Fundo bege, três ícones estilizados em verde oliva (crampo/calor/irritabilidade), texto azul marinho, grafismo de folhas como textura lateral"
      deviation_note: null

    - slide_number: 5
      canva_design_id: "DAGxxxxxABC5"
      export_url: "https://export.canva.com/png/DAGxxxxxABC5/slide5.png"
      dimensions: "1080x1080"
      visual_direction_applied: "Tabela comparativa óxido vs bisglicinato de magnésio — fundo azul acinzentado #71a3c1, texto branco, headers em turquesa"
      deviation_note: null

    - slide_number: 6
      canva_design_id: "DAGxxxxxABC6"
      export_url: "https://export.canva.com/png/DAGxxxxxABC6/slide6.png"
      dimensions: "1080x1080"
      visual_direction_applied: "Fundo verde oliva, foto lifestyle gerada com mcp-image (mulher em ambiente de spa, luz natural, tons terrosos), texto branco bold"
      deviation_note: "Foto lifestyle gerada via mcp-image — sem stock adequado em Canva"

    - slide_number: 7
      canva_design_id: "DAGxxxxxABC7"
      export_url: "https://export.canva.com/png/DAGxxxxxABC7/slide7.png"
      dimensions: "1080x1080"
      visual_direction_applied: "Produto Magnésio Bisglicinato Asufarma em destaque, fundo bege, nome do produto em azul marinho, badge Manipulação Personalizada em turquesa"
      deviation_note: null

    - slide_number: 8
      canva_design_id: "DAGxxxxxABC8"
      export_url: "https://export.canva.com/png/DAGxxxxxABC8/slide8.png"
      dimensions: "1080x1080"
      visual_direction_applied: "CTA slide — fundo azul marinho, texto COMENTA MAGNÉSIO em turquesa bold, logo Asufarma centralizado, endereço das 3 unidades no rodapé em branco"
      deviation_note: null
```

## Quality Criteria

- Every slide has a confirmed `canva_design_id` AND `export_url` — no placeholder or null values
- `brand_kit_id: "kAG4986LZbc"` applied to 100% of designs — verified at generation call
- All export URLs return accessible PNG files at 1080x1080 (or 1080x1350 if portrait)

## Veto Conditions

- If any slide's export URL is inaccessible or returns an error, the task is incomplete — do not deliver partial output; retry the failed export before logging
- If a generated design uses colors clearly outside the Asufarma palette (e.g., red, orange, bright green), regenerate that slide with a more explicit color instruction before accepting
