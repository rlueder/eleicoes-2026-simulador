# Simulador 1º turno — Eleições 2026

Simulador interativo de cenários do primeiro turno das eleições presidenciais brasileiras de 2026, a partir de pesquisas de intenção de voto reais.

**🔗 Ao vivo:** https://rlueder.github.io/eleicoes-2026-simulador/

Escolha a pesquisa-base, mexa nas três alavancas — destino dos indecisos, anulação e voto útil — e veja se a conta fecha para vitória sem segundo turno. Cada cenário gera um link compartilhável (o estado fica no fragmento da URL).

## Como a conta é feita

- Vitória no 1º turno = **mais de 50% dos votos válidos** (excluídos brancos e nulos), conforme o art. 77, §2º, da Constituição.
- Os indecisos não destinados ao protagonista nem à anulação se distribuem proporcionalmente entre o adversário e os demais candidatos.
- A migração por voto útil é retirada apenas dos demais candidatos.

> ⚠️ Exercício matemático de cenários, **não previsão eleitoral**. Boa parte das diferenças simuladas cabe dentro da margem de erro amostral, e o modelo ignora efeitos de segunda ordem (desistências, rejeição, comparecimento).

## Adicionando novas pesquisas

Basta editar [`polls.json`](polls.json) — nenhuma alteração de código é necessária. Cada rodada é um objeto no array `polls`:

```json
{
  "id": "instituto-2026-06",
  "label": "Instituto · junho 2026",
  "institute": "Instituto",
  "released": "2026-06-10",
  "fieldwork": "5 a 8 de junho de 2026",
  "method": "entrevistas presenciais",
  "sample": 2004,
  "marginPP": 2,
  "confidence": 95,
  "tse": "BR-00000/2026",
  "contractor": "Contratante",
  "sourceUrl": "https://exemplo.com/reportagem",
  "numbers": {
    "lula": 39,
    "flavio": 29,
    "outros": 13,
    "branco": 9,
    "indecisos": 10
  },
  "note": "Observações sobre o cenário (lista de candidatos, ressalvas etc.)."
}
```

Os campos `numbers` devem somar 100. `tse`, `sourceUrl` e `note` podem ser `null`. As rodadas são ordenadas automaticamente da mais recente para a mais antiga pelo campo `released` (`AAAA-MM-DD`).

## Rodando localmente

A página busca `polls.json` via `fetch`, então é preciso servir os arquivos por HTTP (abrir o `index.html` direto do disco usa o conjunto de dados embutido como fallback):

```sh
python3 -m http.server 8000
# http://localhost:8000
```

Sem dependências, sem build — apenas HTML, CSS e JavaScript puros.

## Licença

[MIT](LICENSE)
