# SQL - JOIN

Esclarecimento de possíveis dúvidas e questões resolvidas

## Teoria
Exitem três joins mais utilizados: INNER JOIN(JOIN), LEFT JOIN, RIGHT JOIN

1) A tabela do conjunto a esquerda é a 'ORIGEM'(FROM).
2)Básico de teoria do conjunto LEFT (OUTER) JOIN é o complemento de B em relação a A, se b for o Right Side.(se aplica da mesma forma para o RIGHT (OUTER) JOIN)
3)INNER JOIN ou JOIN é a interseção ou intersecção.
4)FULL OUTER JOIN, raramente é utilizado, normalmente se faz da mesma maneira que se calcula o n(AUB) = nA + nB -n(AinterB)(dessa maneira precisar determinar qual das interseções será excluida). No LEFT E NO RIGHT deve-se utilizar IF NULL.

Existem ainda três JOIN que não são tão utilizados: UNION, UNION ALL, CROSS JOIN

[Union](https://www.w3schools.com/sql/sql_union.asp)
[CROSS JOIN](https://www.w3resource.com/sql/joins/cross-join.php) 
[SELF JOIN](https://www.w3schools.com/sql/sql_join_self.asp)

## Exercícios

1) Forneca uma tabela que fornece a região para cada sales_rep junto com suas contas associadas . Desta vez apenas para a Midwestregião. Sua tabela final deve incluir três colunas: o nome da região , o nome do representante de vendas e o nome da conta . Classifique as contas em ordem alfabética (AZ) de acordo com o nome da conta.
```SQL
SELECT r.name region, s.name rep, a.name account
FROM sales_reps s
JOIN region r
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
WHERE r.name = 'Midwest'
ORDER BY a.name;
```

2) Forneça uma tabela que fornece a região para cada sales_rep junto com suas contas associadas . Desta vez, apenas para contas em que o representante de vendas tem um nome que começa com S e na Midwest região. Sua tabela final deve incluir três colunas: o nome da região , o nome do representante de vendas e o nome da conta . Classifique as contas em ordem alfabética (AZ) de acordo com o nome da conta.
```SQL
SELECT r.name region, s.name rep, a.name account
FROM sales_reps s
JOIN region r
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
WHERE r.name = 'Midwest' AND s.name LIKE 'S%'
ORDER BY a.name;
```

3) Forneça uma tabela que fornece a região para cada sales_rep junto com suas contas associadas . Desta vez, apenas para contas em que o representante de vendas tem um sobrenome que começa com K e na Midwest região. Sua tabela final deve incluir três colunas: o nome da região , o nome do representante de vendas e o nome da conta . Classifique as contas em ordem alfabética (AZ) de acordo com o nome da conta.
```SQL
SELECT r.name region, s.name rep, a.name account
FROM sales_reps s
JOIN region r
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
WHERE r.name = 'Midwest' AND s.name LIKE '% K%'
ORDER BY a.name;
```

4) Forneça o nome de cada região para cada pedido , bem como o nome da conta e o preço unitário pago (total_amt_usd / total) pelo pedido. No entanto, você só deve fornecer os resultados se a quantidade padrão do pedido exceder 100. Sua tabela final deve ter 3 colunas: nome da região , nome da conta e preço unitário 
```SQL
SELECT r.name region, a.name account, o.total_amt_usd/(o.total + 0.01) unit_price
FROM region r
JOIN sales_reps s
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
JOIN orders o
ON o.account_id = a.id
WHERE o.standard_qty > 100;
```

5) Forneça o nome de cada região para cada pedido , bem como o nome da conta e o preço unitário pago (total_amt_usd / total) pelo pedido. No entanto, você só deve fornecer os resultados se a quantidade do pedido padrão for superior 100e a quantidade do pedido do pôster for superior 50. Sua tabela final deve ter 3 colunas: nome da região , nome da conta e preço unitário . Classifique primeiro pelo menor preço unitário .
colunas: nome da região , nome da conta e preço unitário 
```SQL
SELECT r.name region, a.name account, o.total_amt_usd/(o.total + 0.01) unit_price
FROM region r
JOIN sales_reps s
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
JOIN orders o
ON o.account_id = a.id
WHERE o.standard_qty > 100 AND o.poster_qty > 50
ORDER BY unit_price;
```

6) Forneça o nome de cada região para cada pedido , bem como o nome da conta e o preço unitário pago (total_amt_usd / total) pelo pedido. No entanto, você só deve fornecer os resultados se a quantidade do pedido padrão for superior 100e a quantidade do pedido do pôster for superior 50. Sua tabela final deve ter 3 colunas: nome da região , nome da conta e preço unitário . Classifique primeiro pelo maior preço unitário .
```SQL
SELECT r.name region, a.name account, o.total_amt_usd/(o.total + 0.01) unit_price
FROM region r
JOIN sales_reps s
ON s.region_id = r.id
JOIN accounts a
ON a.sales_rep_id = s.id
JOIN orders o
ON o.account_id = a.id
WHERE o.standard_qty > 100 AND o.poster_qty > 50
ORDER BY unit_price DESC;
```

7) Quais são os diferentes canais usados ​​pelo ID da conta 1001 ? Sua tabela final deve ter apenas 2 colunas: nome da conta e os diferentes canais . Você pode tentar SELECT DISTINCT para restringir os resultados a apenas os valores exclusivos.
```SQL
SELECT DISTINCT a.name, w.channel
FROM accounts a
JOIN web_events w
ON a.id = w.account_id
WHERE a.id = '1001';
```

8) Encontre todos os pedidos ocorridos em 2015. Sua tabela final deve ter 4 colunas: ocorrido_at , nome da conta , total do pedido e total_amt_usd do pedido .
```SQL
SELECT o.occurred_at, a.name, o.total, o.total_amt_usd
FROM accounts a
JOIN orders o
ON o.account_id = a.id
WHERE o.occurred_at BETWEEN '01-01-2015' AND '01-01-2016'
ORDER BY o.occurred_at DESC;
```

## Contributing
SQL for Data Analysis [Udacity](https://udacity.com)

## License
[MIT](https://choosealicense.com/licenses/mit/)
