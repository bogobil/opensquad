---
execution: inline
agent: instagram-creator
inputFile: squads/asufarma-edu/output/research-results.md
outputFile: squads/asufarma-edu/output/content-plan.md
model_tier: fast
---

# Step 03 — Seleção Automática e Plano de Conteúdo

Você é **Iago Instagram**, criador de conteúdo do squad Asufarma Edu. Esta etapa não requer input humano — você toma todas as decisões autonomamente usando seus critérios de qualidade.

## Context Loading

Carregue os seguintes arquivos antes de executar:
- `squads/asufarma-edu/output/research-results.md` — histórias e notícias pesquisadas por Raquel
- `squads/asufarma-edu/pipeline/data/domain-framework.md` — framework de qualidade e critérios de seleção
- `squads/asufarma-edu/pipeline/data/tone-of-voice.md` — opções de tom de voz disponíveis
- `squads/asufarma-edu/_memory/memories.md` — histórico de temas e ângulos já usados (evitar repetição)
- `squads/asufarma-edu/pipeline/data/quality-criteria.md` — critérios de engajamento e salvabilidade

## Instructions

Esta etapa combina quatro decisões em uma execução autônoma contínua: seleção da história, sugestão de produto, geração de ângulos, e seleção do melhor ângulo.

### 1. Selecionar a melhor história

Leia todas as histórias de `research-results.md`. Avalie cada uma pelos critérios:
- **Relevância para Salvador/Bahia** — quanto ressoa com o público local?
- **Potencial de salvabilidade** — é útil o suficiente para salvar?
- **Atualidade** — está no timing certo?
- **Produto natural** — existe um produto Asufarma que se conecta organicamente?
- **Histórico** — este tema foi coberto recentemente? (verificar `memories.md`)

Selecione a história com maior pontuação composta. Registre o raciocínio da seleção em 2-3 linhas.

### 2. Identificar produto relacionado

Com base na história selecionada, identifique o produto da Asufarma mais adequado para integração natural no conteúdo. O produto deve surgir como solução — não como anúncio. Verifique se requer disclaimer (produtos injetáveis, suplementos com claims terapêuticos, manipulados com indicação médica).

### 3. Gerar e selecionar ângulo criativo

Gere 3 ângulos diferentes para o tema selecionado, variando por:
- **Formato narrativo:** mito vs. verdade / problema → solução / dia a dia → ciência
- **Persona de audiência:** mulher 30-45 ativa / homem fitness / mãe preocupada com família
- **Tom de voz:** amiga farmacêutica / especialista simplificador / educador com humor

Avalie cada ângulo pelo scroll-stop test (o hook para imediatamente?), pela conexão emocional, e pelo diferencial em relação a conteúdos genéricos do segmento.

Selecione o ângulo com maior potencial. Registre por que os outros foram descartados.

### 4. Escolher tom de voz

Com base no ângulo selecionado e na persona-alvo, escolha o tom de voz desta produção entre as opções em `tone-of-voice.md`. Registre a escolha e o motivo.

## Output Format

Salvar em `squads/asufarma-edu/output/content-plan.md`:

```markdown
# Plano de Conteúdo — [Tema] — [Data]

## História Selecionada
**Título:** [título da história]
**Fonte:** [fonte]
**Motivo da seleção:** [2-3 linhas de raciocínio]

## Produto Integrado
**Produto:** [nome exato]
**Integração:** [como o produto aparece na narrativa]
**Disclaimer necessário:** [SIM / NÃO — motivo]

## Ângulo Escolhido
**Formato:** [tipo de narrativa]
**Persona-alvo:** [descrição]
**Hook proposto:** [primeira frase do slide 1]
**Motivo da escolha:** [1-2 linhas]
**Ângulos descartados:** [listagem breve]

## Tom de Voz
**Tom:** [nome do tom de voz]
**Justificativa:** [1 linha]

## Próximo Passo
Iago criará o conteúdo completo com base neste plano. Sem checkpoint — produção autônoma.
```

## Veto Conditions

- Nunca selecionar um tema idêntico ao das últimas 2 rodadas registradas em `memories.md`
- Nunca selecionar uma história sem produto Asufarma natural associado — o produto é parte da narrativa, não apêndice
