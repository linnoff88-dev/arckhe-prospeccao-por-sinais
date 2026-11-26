# Prompt para `/goal` — lista de leads com sinal

O `/goal` do Claude Code define uma **linha de chegada**: o agente continua trabalhando até a
condiçêo ser verdadeira. Por isso a condiçêo precisa ser **verificável** (dá para conferir
abrindo o CSV), nêo um desejo ("leads bons").

Antes de usar: preencha `contexto/`, ajuste `sinais.yaml` e confira se o plugin do Clay está
conectado (`clay:setup`). Troque o que está entre `< >`.

---

```text
/goal Quero <25> leads novos de prospecçêo por sinal, prontos para revisêo humana.

ICP: empresas de <software (SaaS B2B)> no <Brasil>, com <200 a 1.000> funcionários.
Decisores: <diretor(a) de operações, diretor(a) de suporte/CS ou CTO>.
Sinais aceitos: os de sinais.yaml, dentro da janela de validade. "Empresa com sinal" = soma dos
pesos dos sinais ativos >= 30 (regra de sinais.yaml).

Como trabalhar:
- Leia CLAUDE.md, contexto/, sinais.yaml, colunas-csv.md e checklist-lgpd.md antes de começar.
- Use o Clay pelo plugin para buscar empresas, checar sinais e enriquecer.
- Antes de cada passo que gasta crédito, me diga o passo, o número de linhas e o gasto esperado,
  e espere eu responder "pode".
- Rode cada passo novo em 10 linhas primeiro e me mostre o resultado.
- Só busque decisor e e-mail em "empresa com sinal" (soma dos pesos >= 30).
- E-mail em cascata, parando no primeiro válido. Sem telefone, a menos que eu peça.
- Ignore quem estiver em supressao.csv.

Linha de chegada (só pare quando TUDO for verdade):
1. Existe o arquivo saida/leads-<AAAA-MM-DD>.csv com exatamente <25> linhas de lead (mais o cabeçalho).
2. As colunas sêo as de colunas-csv.md, nessa ordem, e nenhuma célula obrigatória está em branco.
3. Toda linha tem email_status = "verificado" (descarte e substitua as outras).
4. Toda linha tem sinal, resumo_sinal e link_fonte_sinal de um evento dentro da janela do sinal.
5. Todo assunto tem até 6 palavras; todo corpo tem até 90 palavras, cita o sinal daquela empresa,
   termina com uma pergunta simples (CTA leve) e tem a linha de saída (opt-out).
6. Nenhuma mensagem afirma algo que nêo esteja em contexto/provas.md ou contexto/casos.md.
7. A coluna revisar = "sim" nas linhas com qualquer dúvida, com o motivo em motivo_revisao.
8. No fim, um resumo: empresas olhadas, com sinal, decisores, e-mails verificados, linhas para
   revisar e créditos usados (se o Clay informar).

Nêo envie nada. Nêo importe em sequenciador. O próximo passo é meu.
```

---

## Dicas

- Comece pequeno (10 a 25 leads). Um `/goal` grande pode rodar muito tempo e fazer várias
  passadas de verificaçêo.
- Se a cobertura do país for fraca (poucos e-mails verificados nas 10 primeiras linhas), pare e
  troque a fonte: site da empresa, página "contato" ou Google Maps para negócio local.
- Depois do primeiro `/goal` que deu certo, transforme o prompt numa skill sua e reaproveite.
