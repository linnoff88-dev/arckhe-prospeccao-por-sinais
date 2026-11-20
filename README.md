# ðŸ“¡ ProspecÃ§Ã£o por Sinais

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![ProspecÃ§Ã£o por Sinais](guia/assets/banner.jpg)](https://inematds.github.io/prospeccao-por-sinais/guia/)

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

## O que Ã©

Este Ã© um kit gratuito para quem vende para empresas e quer prospectar sem disparar e-mail para lista fria. A ideia Ã© procurar **sinais**, ou seja, acontecimentos pÃºblicos que mostram que uma empresa pode precisar de vocÃª agora (uma vaga aberta, um produto lanÃ§ado, um diretor novo), e sÃ³ entÃ£o achar a pessoa que decide e escrever uma mensagem que cita esse sinal. O Claude Code faz o trabalho pesado usando o Clay (uma plataforma de dados de empresas e contatos) e entrega uma planilha para vocÃª revisar. VocÃª precisa do Claude Code, de uma conta no Clay (tem plano grÃ¡tis e teste) e de uma tarde para preencher o contexto do seu negÃ³cio.

## ðŸ“– Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/prospeccao-por-sinais/guia/**

## Antes de comeÃ§ar

- **Claude Code** â‰¥ 2.1.91 (precisa de assinatura paga do Claude): `curl -fsSL https://claude.ai/install.sh | bash` (Mac/Linux), `irm https://claude.ai/install.ps1 | iex` (Windows) ou `npm install -g @anthropic-ai/claude-code` â€” docs: https://docs.claude.com/en/docs/claude-code/overview
- **Conta no Clay** (grÃ¡tis ou teste de 14 dias).
- **git** (ou baixe o [.zip](https://github.com/inematds/prospeccao-por-sinais/archive/refs/heads/main.zip)) e, sÃ³ para a skill opcional de sinais, **Node.js** (`npx`).

## O processo, do inÃ­cio ao fim

Quem faz: ðŸ§  vocÃª no Claude Code Â· âš™ï¸ Clay/script Â· ðŸ¤– agente (Claude Code trabalhando sozinho)

| # | Passo | Comando | Quem |
|---|-------|---------|------|
| 1 | Baixar o kit e abrir o Claude Code na pasta | `git clone https://github.com/inematds/prospeccao-por-sinais.git` Â· `cp -r prospeccao-por-sinais/kit ~/minha-prospeccao` Â· `cd ~/minha-prospeccao` Â· `claude` | ðŸ§  |
| 2 | Instalar o plugin do Clay (Claude Code â‰¥ 2.1.91) | `/plugin marketplace add clay-run/agent-plugins` Â· `/plugin install clay@clay-plugins` Â· "Rode a skill clay:setup" | ðŸ§  |
| 3 | Preencher o contexto do negÃ³cio | editar `contexto/*.md` (modelo em `contexto/exemplo/`) | ðŸ§  |
| 4 | Definir os sinais | editar `sinais.yaml` Â· opcional: `npx skills add clay-run/clay-skill-creator --skill customer-signal-generator` | ðŸ§  + ðŸ¤– |
| 5 | ICP: lista de empresas (10 linhas primeiro) | Passo 1 de `prompts/passo-a-passo.md` | ðŸ¤– + âš™ï¸ |
| 6 | Sinal de contrataÃ§Ã£o monitorado | Passo 2 | ðŸ¤– + âš™ï¸ |
| 7 | Agente de pesquisa (lanÃ§amento de produto) | Passo 3 | ðŸ¤– + âš™ï¸ |
| 8 | Decisor sÃ³ onde hÃ¡ sinal (condiÃ§Ã£o de execuÃ§Ã£o: soma dos pesos dos sinais ativos â‰¥ 30) | Passo 4 | ðŸ¤– + âš™ï¸ |
| 9 | E-mail em cascata + verificaÃ§Ã£o | Passo 5 | âš™ï¸ |
| 10 | Mensagem com contexto (assunto + corpo citando o sinal) | Passo 6 â€” ou tudo de uma vez com `/goal` (`prompts/goal-prospeccao.md`) | ðŸ¤– |
| 11 | CSV final para revisÃ£o | `saida/leads-AAAA-MM-DD.csv` (colunas em `colunas-csv.md`) | ðŸ¤– |
| 12 | RevisÃ£o humana | ler as linhas com `revisar = sim`, corrigir | ðŸ§  |
| 13 | Importar no sequenciador e enviar devagar | importar CSV â†’ campanha; domÃ­nio secundÃ¡rio aquecido, poucos envios/dia, spam < 0,3% | ðŸ§  + âš™ï¸ |
| 14 | SupressÃ£o | quem pediu para sair vai para `supressao.csv` no mesmo dia | ðŸ§  |

Regra de ouro (estÃ¡ no `kit/CLAUDE.md`): o agente **nunca gasta crÃ©dito sem pedir**, **roda 10 linhas antes** e **nunca envia nada**.

## O kit

```
kit/
â”œâ”€â”€ CLAUDE.md                 regras do agente (crÃ©dito, 10 linhas, revisÃ£o, opt-out, LGPD)
â”œâ”€â”€ contexto/                 6 modelos: perfil-do-negocio, oferta, casos, provas, faq, tom-de-voz
â”‚   â””â”€â”€ exemplo/              os mesmos 6, preenchidos com uma empresa FICTÃCIA
â”œâ”€â”€ prompts/
â”‚   â”œâ”€â”€ goal-prospeccao.md    prompt para /goal com linha de chegada verificÃ¡vel
â”‚   â””â”€â”€ passo-a-passo.md      um prompt por passo do fluxo
â”œâ”€â”€ sinais.yaml               sinais de exemplo com janela de validade e peso
â”œâ”€â”€ colunas-csv.md            colunas da planilha de saÃ­da
â”œâ”€â”€ checklist-lgpd.md         checklist prÃ¡tico (nÃ£o Ã© parecer jurÃ­dico)
â””â”€â”€ supressao.csv             quem pediu para sair
```

## Custos (documentaÃ§Ã£o pÃºblica do Clay, conferido em 01/11/2026)

- GrÃ¡tis: 100 crÃ©ditos/mÃªs. Teste de 14 dias: 1.000 crÃ©ditos. Plano Launch: a partir de US$ 185/mÃªs (2.500 crÃ©ditos + 15.000 aÃ§Ãµes).
- Na cascata, os fornecedores padrÃ£o de e-mail e celular devolvem o crÃ©dito quando nÃ£o acham; celular nÃ£o estÃ¡ disponÃ­vel no grÃ¡tis nem no teste.
- Fonte: https://github.com/clay-run/public-docs

## ReferÃªncias

- Plugin do Clay para agentes: https://github.com/clay-run/agent-plugins
- Gmail â€” diretrizes para remetentes: https://support.google.com/a/answer/81126?hl=pt-BR
- LGPD (Lei 13.709/2018): https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm Â· ANPD: https://www.gov.br/anpd

---

ConteÃºdo aberto e gratuito do [INEMA.CLUB](https://inema.club).

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>