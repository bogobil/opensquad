---
task: suggest-products
agent: squads/asufarma-edu/agents/product-specialist
order: 3
input:
  - ranked_brief (output of rank-stories.md)
output:
  - enriched_brief (YAML, ranked_brief + product annotations)
---

## Process

1. **Map products to stories.** For each of the 5 ranked stories, identify the best-fit Asufarma product(s). Always check flagship products first: Melatonina Gummie, Colageno Verisol, Creatina Caramelo, Corebiome, Ormonelle. If no flagship fits, identify a secondary catalog product or ingredient that Asufarma could highlight. If no current product fits, flag as "sem produto definido — sugestao de novidade" and propose what category could fill the gap.

2. **Label disclaimer type.** For each product suggestion, classify as: `DERMOCOSMETICO` (topical skincare formula — no medical disclaimer required) or `SUPLEMENTO` (supplements, nutraceuticals — disclaimer required) or `FARMACO` (compounded medications — disclaimer required, extra regulatory care). This label is passed directly to Iago to control disclaimer usage.

3. **Add creative hooks.** For each product suggestion, write one customer scenario or creative hook sentence that gives Iago a narrative starting point. The hook should be specific to Salvador life and the target audience segment (e.g., "A baiana que treina de manha na orla e quer recuperar o sono sem depender de remedios quimicos").

---

## Output Format

```yaml
enriched_brief:
  stories:
    - rank: number
      title: string                    # inherited from ranked_brief
      product_name: string             # exact Asufarma product name
      product_category: string         # flagship | secondary | novelty_suggestion
      disclaimer_type: DERMOCOSMETICO | SUPLEMENTO | FARMACO
      key_benefit_claim: string        # one compliant benefit sentence
      creative_hook: string            # customer scenario / narrative starting point
      novelty_note: string | null      # if product gap detected, propose a new category
      rotation_safe: boolean           # true if product was NOT used in last 2 cycles
```

## Output Example

```yaml
enriched_brief:
  stories:
    - rank: 1
      title: "Probioticos e ansiedade: o que o seu intestino tem a ver com seu humor"
      product_name: "Corebiome"
      product_category: flagship
      disclaimer_type: SUPLEMENTO
      key_benefit_claim: "O Corebiome contribui para o equilibrio do microbioma intestinal, que esta diretamente associado ao bem-estar emocional segundo estudos recentes do eixo intestino-cerebro."
      creative_hook: "A soteropolitana que cuida da ansiedade sem querer depender so de terapia — ela quer entender o que acontece no proprio corpo e agir com solucoes naturais e personalizadas."
      novelty_note: null
      rotation_safe: true

    - rank: 2
      title: "Melatonina gummie: o que acontece no seu corpo em cada hora da noite"
      product_name: "Melatonina Gummie"
      product_category: flagship
      disclaimer_type: SUPLEMENTO
      key_benefit_claim: "A Melatonina Gummie da Asufarma apoia a regulacao do ciclo circadiano de forma pratica e gostosa, com dosagem personalizada para cada perfil."
      creative_hook: "Quem voltou do Carnaval com o sono destruido e precisa de uma solucao real — nao so um chazinho — antes de voltar para a rotina."
      novelty_note: null
      rotation_safe: true

    - rank: 5
      title: "Vitamina D e imunidade: por que quase todo mundo em SSA tem deficiencia"
      product_name: null
      product_category: novelty_suggestion
      disclaimer_type: SUPLEMENTO
      key_benefit_claim: "A suplementacao de Vitamina D3 + K2 contribui para a imunidade e saude ossea, especialmente em populacoes com exposicao solar insuficiente apesar do clima ensolarado."
      creative_hook: "Inusitado: Salvador tem sol o ano todo mas a deficiencia de Vitamina D e altissima. Esse contraste e o gancho do conteudo."
      novelty_note: "Asufarma nao tem um produto Vitamina D D3+K2 como flagship. Sugere-se criacao de um combo D3+K2 manipulado como produto de temporada."
      rotation_safe: true
```

## Quality Criteria

- All 5 stories receive a product annotation; none is left blank without a `novelty_note` explanation
- Disclaimer type is explicitly set for every story — no omissions
- At least one `novelty_note` per enriched brief cycle, proposing an emerging product or ingredient

## Veto Conditions

- A product whose `rotation_safe` is false (used in last 2 cycles) cannot be suggested without an explicit flag and justification from Pedro
- No claim in `key_benefit_claim` may use the words "cura", "trata", "elimina", "emagrece" — if Pedro drafts one with these terms, it is self-vetoed and rewritten before delivery
