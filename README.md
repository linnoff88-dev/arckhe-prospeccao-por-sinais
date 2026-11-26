ï»¿# ê°Å¸âÂ¡ ProspecêÂ§êÂ£o por Sinais

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![ProspecêÂ§êÂ£o por Sinais](guia/assets/banner.jpg)](https://inematds.github.io/prospeccao-por-sinais/guia/)

**ê°Å¸â¡Â§ê°Å¸â¡Â· [PortuguêÂªs](README.md) êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

## O que êÂ©

Este êÂ© um kit gratuito para quem vende para empresas e quer prospectar sem disparar e-mail para lista fria. A ideia êÂ© procurar **sinais**, ou seja, acontecimentos pêÂºblicos que mostram que uma empresa pode precisar de vocêÂª agora (uma vaga aberta, um produto lanêÂ§ado, um diretor novo), e sêÂ³ entêÂ£o achar a pessoa que decide e escrever uma mensagem que cita esse sinal. O Claude Code faz o trabalho pesado usando o Clay (uma plataforma de dados de empresas e contatos) e entrega uma planilha para vocêÂª revisar. VocêÂª precisa do Claude Code, de uma conta no Clay (tem plano grêÂ¡tis e teste) e de uma tarde para preencher o contexto do seu negêÂ³cio.

## ê°Å¸ââ Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/prospeccao-por-sinais/guia/**

## Antes de comeêÂ§ar

- **Claude Code** ê¢â°Â¥ 2.1.91 (precisa de assinatura paga do Claude): `curl -fsSL https://claude.ai/install.sh | bash` (Mac/Linux), `irm https://claude.ai/install.ps1 | iex` (Windows) ou `npm install -g @anthropic-ai/claude-code` ê¢â¬â docs: https://docs.claude.com/en/docs/claude-code/overview
- **Conta no Clay** (grêÂ¡tis ou teste de 14 dias).
- **git** (ou baixe o [.zip](https://github.com/inematds/prospeccao-por-sinais/archive/refs/heads/main.zip)) e, sêÂ³ para a skill opcional de sinais, **Node.js** (`npx`).

## O processo, do inêÂ­cio ao fim

Quem faz: ê°Å¸Â§Â  vocêÂª no Claude Code êÂ· ê¢Å¡â¢ê¯Â¸Â Clay/script êÂ· ê°Å¸Â¤â agente (Claude Code trabalhando sozinho)

| # | Passo | Comando | Quem |
|---|-------|---------|------|
| 1 | Baixar o kit e abrir o Claude Code na pasta | `git clone https://github.com/inematds/prospeccao-por-sinais.git` êÂ· `cp -r prospeccao-por-sinais/kit ~/minha-prospeccao` êÂ· `cd ~/minha-prospeccao` êÂ· `claude` | ê°Å¸Â§Â  |
| 2 | Instalar o plugin do Clay (Claude Code ê¢â°Â¥ 2.1.91) | `/plugin marketplace add clay-run/agent-plugins` êÂ· `/plugin install clay@clay-plugins` êÂ· "Rode a skill clay:setup" | ê°Å¸Â§Â  |
| 3 | Preencher o contexto do negêÂ³cio | editar `contexto/*.md` (modelo em `contexto/exemplo/`) | ê°Å¸Â§Â  |
| 4 | Definir os sinais | editar `sinais.yaml` êÂ· opcional: `npx skills add clay-run/clay-skill-creator --skill customer-signal-generator` | ê°Å¸Â§Â  + ê°Å¸Â¤â |
| 5 | ICP: lista de empresas (10 linhas primeiro) | Passo 1 de `prompts/passo-a-passo.md` | ê°Å¸Â¤â + ê¢Å¡â¢ê¯Â¸Â |
| 6 | Sinal de contrataêÂ§êÂ£o monitorado | Passo 2 | ê°Å¸Â¤â + ê¢Å¡â¢ê¯Â¸Â |
| 7 | Agente de pesquisa (lanêÂ§amento de produto) | Passo 3 | ê°Å¸Â¤â + ê¢Å¡â¢ê¯Â¸Â |
| 8 | Decisor sêÂ³ onde hêÂ¡ sinal (condiêÂ§êÂ£o de execuêÂ§êÂ£o: soma dos pesos dos sinais ativos ê¢â°Â¥ 30) | Passo 4 | ê°Å¸Â¤â + ê¢Å¡â¢ê¯Â¸Â |
| 9 | E-mail em cascata + verificaêÂ§êÂ£o | Passo 5 | ê¢Å¡â¢ê¯Â¸Â |
| 10 | Mensagem com contexto (assunto + corpo citando o sinal) | Passo 6 ê¢â¬â ou tudo de uma vez com `/goal` (`prompts/goal-prospeccao.md`) | ê°Å¸Â¤â |
| 11 | CSV final para revisêÂ£o | `saida/leads-AAAA-MM-DD.csv` (colunas em `colunas-csv.md`) | ê°Å¸Â¤â |
| 12 | RevisêÂ£o humana | ler as linhas com `revisar = sim`, corrigir | ê°Å¸Â§Â  |
| 13 | Importar no sequenciador e enviar devagar | importar CSV ê¢â â campanha; domêÂ­nio secundêÂ¡rio aquecido, poucos envios/dia, spam < 0,3% | ê°Å¸Â§Â  + ê¢Å¡â¢ê¯Â¸Â |
| 14 | SupressêÂ£o | quem pediu para sair vai para `supressao.csv` no mesmo dia | ê°Å¸Â§Â  |

Regra de ouro (estêÂ¡ no `kit/CLAUDE.md`): o agente **nunca gasta crêÂ©dito sem pedir**, **roda 10 linhas antes** e **nunca envia nada**.

## O kit

```
kit/
ê¢âÅê¢ââ¬ê¢ââ¬ CLAUDE.md                 regras do agente (crêÂ©dito, 10 linhas, revisêÂ£o, opt-out, LGPD)
ê¢âÅê¢ââ¬ê¢ââ¬ contexto/                 6 modelos: perfil-do-negocio, oferta, casos, provas, faq, tom-de-voz
ê¢ââ   ê¢ââê¢ââ¬ê¢ââ¬ exemplo/              os mesmos 6, preenchidos com uma empresa FICTêÂCIA
ê¢âÅê¢ââ¬ê¢ââ¬ prompts/
ê¢ââ   ê¢âÅê¢ââ¬ê¢ââ¬ goal-prospeccao.md    prompt para /goal com linha de chegada verificêÂ¡vel
ê¢ââ   ê¢ââê¢ââ¬ê¢ââ¬ passo-a-passo.md      um prompt por passo do fluxo
ê¢âÅê¢ââ¬ê¢ââ¬ sinais.yaml               sinais de exemplo com janela de validade e peso
ê¢âÅê¢ââ¬ê¢ââ¬ colunas-csv.md            colunas da planilha de saêÂ­da
ê¢âÅê¢ââ¬ê¢ââ¬ checklist-lgpd.md         checklist prêÂ¡tico (nêÂ£o êÂ© parecer jurêÂ­dico)
ê¢ââê¢ââ¬ê¢ââ¬ supressao.csv             quem pediu para sair
```

## Custos (documentaêÂ§êÂ£o pêÂºblica do Clay, conferido em 01/11/2026)

- GrêÂ¡tis: 100 crêÂ©ditos/mêÂªs. Teste de 14 dias: 1.000 crêÂ©ditos. Plano Launch: a partir de US$ 185/mêÂªs (2.500 crêÂ©ditos + 15.000 aêÂ§êÂµes).
- Na cascata, os fornecedores padrêÂ£o de e-mail e celular devolvem o crêÂ©dito quando nêÂ£o acham; celular nêÂ£o estêÂ¡ disponêÂ­vel no grêÂ¡tis nem no teste.
- Fonte: https://github.com/clay-run/public-docs

## ReferêÂªncias

- Plugin do Clay para agentes: https://github.com/clay-run/agent-plugins
- Gmail ê¢â¬â diretrizes para remetentes: https://support.google.com/a/answer/81126?hl=pt-BR
- LGPD (Lei 13.709/2018): https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm êÂ· ANPD: https://www.gov.br/anpd

---

ConteêÂºdo aberto e gratuito do [INEMA.CLUB](https://inema.club).

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>