# Droid Tycoon Calculator

Calculadora de fusão de androides da ilha Droid Tycoon do Fortnite.

## Como usar

Abra o `index.html` no navegador. Não precisa de build nem de dependências.

## V1 — Aba "Padrão" ✅

Baseada em `docs/v1.png` (17 receitas de fusão padrão).

- 3 caixas para informar componentes (com autocomplete).
- A busca é afunilada a cada componente: com `ARG` no Componente 1, aparecem WHL-EX, ARM-CORE e as demais receitas que usam ARG.
- **A ordem dos slots não importa** para definir o droid; **a quantidade importa** (`ARG + ARG` só bate com receitas que têm 2x ARG).
- Combinação inexistente → resultado **ALEATÓRIO**.
- 3 componentes que formam uma receita → mostra o droid resultante.

## V2 — Aba "Flagelo (Scourge)" ✅

Baseada em `docs/v2.0.png` e `docs/v2.1.png`.

As receitas Scourge são **as mesmas 17 da V1**; o que muda é o **tier** de cada componente. Por isso a aba reutiliza os mesmos dados (`RECIPES`) e só adiciona um seletor de tier por slot.

Tiers: Scourge, Stellar, Kyber, Beskar, Rainbow, Diamond, Gold, Base.

Regras aplicadas (conforme o documento):

1. **Slot 1 = Scourge (âncora).** Scourge empata com Stellar no peso de raridade, e o slot mais à esquerda desempata. Para o droid, a posição continua não importando; ela só importa para o tier.
2. **Slots 2 e 3: apenas Kyber, Stellar ou Scourge.** Qualquer tier inferior (Base, Gold, Diamond, Rainbow, Beskar) ativa a regra do menor tier e o resultado não sai Scourge.
3. **Ideal: 1 Scourge + 2 Kyber/Stellar.** Economiza 2/3 do estoque de Scourge. 3 Scourge gera o Scourge tier base (ineficiente).

Resultados possíveis da aba:

| Situação | Resultado |
|---|---|
| Scourge no Slot 1 + Kyber/Stellar/Scourge nos demais | Scourge Equivalente (ou tier base com 3 Scourge) |
| Algum tier inferior | Não sai Scourge |
| Nenhum Scourge | Não sai Scourge |
| Scourge presente, mas fora do Slot 1 | Scourge não garantido (caso não coberto pelo documento) |
| Componentes que não formam receita | ALEATÓRIO |

> As regras de tier seguem o documento e **ainda não foram validadas no jogo**.

## Estrutura

- `index.html` — página única (HTML + CSS + JS vanilla), com as duas abas.
- `docs/` — imagens de referência das receitas e regras.

## Source

[Star Wars Droid Tycoon - Fusion Recipes & Scourge Equivalents](https://docs.google.com/spreadsheets/d/1XHNAyen1vCPaDLuKN17lJYUkNHrCM-uXqtiDXD8O3Ls/edit?pli=1&gid=1#gid=1)