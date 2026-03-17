---
task: score-content
agent: squads/asufarma-edu/agents/reviewer
order: 9
input:
  - optimized_content_package (output of optimize-content.md)
output:
  - content_scorecard (YAML, scored breakdown per dimension per format)
---

## Process

1. **Compliance audit.** Check each format (feed, reels, stories) against: (a) disclaimer presence for non-dermocosmetico products — required text is exactly "Consulte seu medico, prescritor ou farmaceutico" or abbreviated equivalent in stories, (b) no prohibited language ("cura", "trata", "elimina", "emagrece", "milagroso"), (c) product name matches exactly ("Corebiome", not "Core Biome"; "Melatonina Gummie", not "Melatonina Gummy"), (d) brand name is "Asufarma" not "Assofarma" or any variant. Assign sub-score 0-25.

2. **Technical accuracy check.** Cross-reference any statistic, study claim, or ingredient mechanism against Raquel's source list from the ranked_brief. Flag any claim that is not traceable to a source. Verify that benefit language is compliant ("contribui para", "apoia", "auxilia" — never "trata" or "cura"). Assign sub-score 0-20.

3. **Brand voice and creative quality scoring.** Evaluate: (a) does the hook stop the scroll? (b) is the Salvador/Bahia identity present or is it generic? (c) is the tone warm and credible without being corporate or condescending? (d) are visual directions specific and on-brand? (e) is the keyword CTA strong and consistent? Assign sub-score 0-40 (Brand Voice 0-20 + Creative/Engagement 0-20). Format completeness (all required elements present): 0-15.

---

## Output Format

```yaml
content_scorecard:
  topic: string
  product: string
  total_score: number               # sum of all sub-scores, max 100
  sub_scores:
    compliance: number              # 0-25
    technical_accuracy: number      # 0-20
    brand_voice: number             # 0-20
    creative_engagement: number     # 0-20
    format_completeness: number     # 0-15
  compliance_flags: [string]        # list of compliance issues found (empty = clean)
  accuracy_flags: [string]          # list of accuracy issues found (empty = clean)
  quality_flags: [string]           # list of quality/voice issues found (empty = clean)
  highlights: [string]              # 2-3 things done well
  verdict: APROVADO | APROVADO_COM_AJUSTES | REPROVADO
  priority_flags:
    p1: [string]                    # compliance blockers — must fix before approval
    p2: [string]                    # quality issues — should fix
    p3: [string]                    # optional improvements
```

## Output Example

```yaml
content_scorecard:
  topic: "Probioticos e ansiedade: o que o seu intestino tem a ver com seu humor"
  product: "Corebiome"
  total_score: 88
  sub_scores:
    compliance: 23
    technical_accuracy: 18
    brand_voice: 19
    creative_engagement: 18
    format_completeness: 10
  compliance_flags:
    - "Stories frame 5 usa disclaimer abreviado ('Consulte seu farmaceutico.') — aceitavel para stories, mas verificar se Lucas aprova essa abreviacao para comunicacao oficial."
  accuracy_flags: []
  quality_flags:
    - "Slide 4 do carousel tem duas frases longas em uma so — recomendado quebrar em dois slides para melhor legibilidade no mobile."
  highlights:
    - "Hook do carousel e reels e excelente — dado surpreendente que contradiz crenca popular sem sensacionalismo."
    - "CTA keyword INTESTINO e consistente em todos os formatos."
    - "Identidade soteropolitana bem presente na creative_hook e na caption do feed."
  verdict: APROVADO_COM_AJUSTES
  priority_flags:
    p1: []
    p2:
      - "Slide 4: quebrar em dois slides. Copy atual: 'Quando esse microbioma esta desequilibrado: ansiedade, irritabilidade, cansaco mental. Soa familiar?' — sugestao: slide 4a mostra os 3 sintomas, slide 4b faz a pergunta 'Soa familiar?'"
    p3:
      - "Considerar adicionar numero de unidades no CTA slide do carousel para facilitar conversao presencial ('Center Lapa, SSA Shopping, Madison Plaza')."
      - "Audio do reels: verificar trending audio na semana da publicacao — sugestao de genero esta correta mas pode haver opcao melhor."
```

## Quality Criteria

- Every compliance_flag includes a specific description of what was found and where (format + slide/frame/segment)
- Total score below 70 automatically triggers REPROVADO verdict
- Highlights section always has 2-3 items — positive feedback is required, not optional

## Veto Conditions

- Any p1 flag automatically forces verdict to REPROVADO regardless of total score
- If brand name "Assofarma" appears anywhere in the content package, it is a P1 flag and automatic veto
