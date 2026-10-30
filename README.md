# 📊 Dashboard Comercial - Análise de Faturamento Líquido

Projeto End-to-End de Análise de Dados focado no acompanhamento de faturamento comercial e classificação por status de pedido, utilizando **Google BigQuery** para tratamento via SQL e **Power BI** para visualização e modelagem em DAX.

---

## 🎯 Objetivo
Analisar a performance de vendas dos clientes aplicando a regra de negócio comercial onde o faturamento deve contabilizar apenas vendas efetivas, excluindo pedidos devolvidos (`Returned`).

---

## 🚀 O Grande Marco do Projeto: Meu Primeiro *Inner Join* Múltiplo!
Este projeto marcou a minha primeira modelagem avançada unindo **três tabelas diferentes** em SQL no BigQuery (`users`, `orders` e `order_items`). Essa estrutura permitiu cruzar dados cadastrais de clientes com informações de pedidos e itens detalhados de venda.

### 🛠️ Código SQL Utilizado no BigQuery:
```sql
SELECT 
    usuarios.first_name AS nome,
    usuarios.last_name AS sobrenome,
    pedidos.order_id AS pedidos_unicos,
    pedidos.status AS status_pedido,
    ROUND(itens.sale_price, 2) AS preco_venda_item
FROM bigquery-public-data.thelook_ecommerce.users AS usuarios

INNER JOIN bigquery-public-data.thelook_ecommerce.orders AS pedidos
    ON usuarios.id = pedidos.user_id

INNER JOIN bigquery-public-data.thelook_ecommerce.order_items AS itens
    ON itens.order_id = pedidos.order_id
    
LIMIT 10;


💡 Regra de Negócio & DAX
Para calcular o Faturamento Líquido expurgando as devoluções de forma dinâmica, foi aplicada a seguinte medida DAX no Power BI:

Faturamento Liquido = 
CALCULATE(
    SUM('Consulta'[preco_venda_item]),
    'Consulta'[status_pedido] <> "Devolvido"
)

📈 Demonstração do Dashboard

🛠️ Tecnologias
Google BigQuery / SQL

Power BI Desktop & DAX

Git & GitHub
