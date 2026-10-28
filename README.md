# Olist — Vendas e Receita

Projeto de análise exploratória **simples e independente**, usando exclusivamente quatro bases originais do conjunto público **Brazilian E-Commerce Public Dataset by Olist**.

## Objetivo

Analisar o desempenho comercial por meio de:

1. exploração inicial dos dados e dos status dos pedidos;
2. evolução mensal do número de pedidos, valor comercializado e ticket médio;
3. participação das vendas por categoria, UF e município;
4. produtos líderes em unidades vendidas e em valor vendido.

**Conceito importante:** o indicador de valor comercializado soma preços dos produtos de **pedidos entregues**, sem frete. Não é receita contábil da Olist, faturamento líquido nem lucro. O nome `receita` aparece na discussão comercial como **valor de vendas de produtos**.

## Vídeo executivo
Vídeo YouTube: https://www.youtube.com/watch?v=AxX04mmgn8E

## Apresentação e Relatório executivo
Estará no /entregaveis

## Quais arquivos usar

Adicione em `data/raw/` os seguintes arquivos do dataset Olist:

- `olist_orders_dataset.csv`
- `olist_order_items_dataset.csv`
- `olist_products_dataset.csv`
- `olist_customers_dataset.csv`

O conjunto é disponibilizado como *Brazilian E-Commerce Public Dataset by Olist*: https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce

Os arquivos não estão incluídos neste pacote. Eles podem ser copiados do projeto anterior, se estiverem disponíveis localmente. Não é necessário usar pagamentos, reviews, sellers ou dados externos.

## Como executar no VS Code

1. Extraia o ZIP e abra a pasta `olist-vendas-e-receita` no VS Code.
2. Copie os quatro CSVs para `data/raw/`.
3. Abra um terminal na pasta do projeto e execute:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

4. Abra `notebooks/01_analise_vendas_receita.ipynb`, selecione o kernel `.venv` e clique em **Run All**.

Se já possuir um `.venv` com pandas, matplotlib, numpy, ipykernel e jupyter, também poderá utilizá-lo.

## O que será gerado

- `outputs/graficos/`: oito gráficos PNG (3 de evolução, 3 de participação e 2 de produtos);
- `outputs/tabelas/`: oito tabelas CSV em UTF-8 com `;` como separador;
- `outputs/resumo_comercial.md`: principais indicadores, descobertas e recomendações iniciais.

## Métricas

- **Pedidos:** pedidos entregues distintos (`order_id`) com itens válidos.
- **Unidades:** quantidade de linhas de itens de pedidos (`order_items`), equivalente a unidades comercializadas na estrutura Olist.
- **Valor de vendas:** soma de `order_items.price` (sem frete) de pedidos entregues.
- **Ticket médio:** valor de vendas / quantidade de pedidos entregues distintos.
- **Participação:** valor por categoria, UF ou município dividido pelo valor comercializado no recorte.
- **Município:** localidade de destino do cliente, agrupada com a UF para evitar homônimos.
- **Top produtos:** classificação separada por unidades e valor dos produtos.

A janela é configurada no início do notebook para **janeiro de 2017 até agosto de 2018**. Esse recorte evita extremos mais incompletos da base histórica. Altere `INICIO` e `FIM_EXCLUSIVO` se desejar outro período.

## Limitações

O dataset não informa o nome comercial dos produtos nem dados para calcular lucro, margem ou comissão da plataforma. Assim, rankings utilizam o `product_id` e a categoria, e recomendações são exploratórias. O conjunto de dados descreve transações históricas, não o desempenho atual da Olist.
