# API de controle de estoque

Esta API permite cadastrar itens, organizar onde ficam armazenados e acompanhar as quantidades disponíveis. Cada entrada ou saída atualiza o saldo e fica registrada no histórico.

Os dados são organizados em:

- Galpões, que representam áreas de armazenamento.
- Locais, definidos por galpão, corredor, prateleira, nível e código.
- Itens, com nome, código, quantidade, unidade e local.
- Movimentações, que registram entradas e saídas de itens.

## O que a API faz

- Cadastra e consulta galpões e locais.
- Cadastra, pesquisa, altera e remove itens.
- Pesquisa itens por nome, código ou localização.
- Registra entradas e saídas e consulta o histórico.
- Não permite retirar mais unidades do que há no estoque.
- Informa se a API está ativa.

## Rotas

Todas as rotas começam com `/api`.

- Galpões: `GET /warehouses`, `GET /warehouses/:id`, `POST /warehouses`.
- Locais: `GET /locations`, `GET /locations/:id`, `POST /locations`.
- Itens: `GET /items`, `GET /items/:id`, `POST /items`, `PUT /items/:id`, `DELETE /items/:id`.
- Estoque: `POST /items/:id/stock-in` para entrada e `POST /items/:id/stock-out` para saída.
- Histórico: `GET /stock-movements`.
- Status: `GET /health`.

As listas podem ser filtradas: itens por `name`, `code` ou `location`; locais por `warehouseId`; movimentações por `itemId` ou `type=in`/`type=out`.

## Exemplo de movimentação

Envie para `POST /api/items/1/stock-in` para adicionar unidades ao item de ID `1`:

```json
{
  "quantity": 3,
  "note": "Reposição semanal"
}
```

Para registrar uma saída, use `/api/items/1/stock-out`. A observação é opcional e a quantidade deve ser maior que zero.
