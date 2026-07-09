# Panorama comercial — editais e contratos

Relatório executivo (HTML estático) para os sócios diretores da Companhia de Impacto, com panorama de editais e contratos: meta, composição da receita, desempenho por frente de trabalho, concentração de carteira e visão 2027.

**v1 — MVP para aprovação do gestor comercial.** Dados carregados manualmente a partir das abas "Resumo de projetos" e "Metas". Blocos de Pipeline (04) e Mercado (07) aguardam envio das abas "Detalhamento" e "Mercado".

## Estrutura do repositório

```
index.html   → o relatório completo (GitHub Pages publica este arquivo automaticamente)
```

Só existe esse arquivo por enquanto — de propósito. Quando a atualização automática for implementada, o mesmo `index.html` continua sendo o alvo: um script vai ler as planilhas e regravar só o bloco `DATA` dentro dele, sem mudar a estrutura do repositório.

## Onde ficam os dados (dentro do index.html)

Todo o conteúdo dinâmico do relatório mora num único bloco, isolado de propósito:

```js
const DATA = { ... }
```

Esse é o **único ponto que precisa ser tocado** para atualizar o relatório — manualmente hoje, automaticamente no futuro. Todo o resto (cálculo de percentuais, barras, donut, formatação de moeda) é renderizado em JavaScript a partir desse objeto.

## Como atualizar manualmente por enquanto

1. Recalcular os valores a partir dos CSVs mais recentes das abas "Resumo de projetos" e "Metas"
2. Substituir o conteúdo do bloco `const DATA = { ... }` em `index.html`
3. Commit + push — o GitHub Pages republica sozinho em 1–2 minutos

## Plano de automação (próxima etapa, não implementado ainda)

Fluxo já desenhado, pendente de execução: Google Sheets → GitHub Actions (cron semanal) → script Python (lê planilha, gera o bloco `DATA`, regrava `index.html`) → commit automático → GitHub Pages republica. n8n fica reservado para integrações futuras (Monday.com, ActiveCampaign) que se beneficiam mais de orquestração do que este fluxo simples de leitura → geração → commit.

## Pendências conhecidas

- Meta por Frente de Trabalho (bloco 03) — a definir com o gestor comercial (Rodolfo); hoje o bloco mostra só a distribuição relativa do realizado, sem meta
- Aba "Detalhamento" (forecast) — necessária para o bloco 04 (Pipeline e cobertura da meta)
- Aba "Mercado" — necessária para o bloco 07 (tipo de mercado e tipo de contrato), aguardando atualização dos contratos de 2026 pelo gestor comercial
