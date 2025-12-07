# 📊 Projeto CRM E-commerce — SQL + Segmentação + Análise de Clientes

Este projeto simula a atuação de um **Analista de CRM Júnior**, utilizando SQL e uma base de dados fictícia para:

- identificar usuários inativos
- analisar comportamento de compra
- descobrir clientes de alto valor (VIPs)
- gerar insights acionáveis para campanhas de CRM
- criar estratégias de reativação e retenção

Os dados incluem:
- `usuarios.csv` → atributos básicos dos clientes
- `compras_teste.csv` → histórico simplificado de compras

---

# 🧠 Objetivos do Projeto
- Criar segmentações (inativos, VIPs, ticket alto, churn)
- Analisar compras por usuário
- Identificar os **Top 3 clientes de maior valor**
- Calcular participação na receita
- Preparar ações de CRM baseadas nos insights
- Criar material para portfólio e currículo

---




# 🛠 SQL PRINCIPAL — Top 3 Clientes que Mais Gastaram

```sql
select u.user_id, u.nome, 
	count(c.id_compra) as total_compras,
	sum(c.valor_compra) as total_gasto
from usuarios u 
join compras c
on u.user_id = c.user_id
group by u.user_id, u.nome
order by total_gasto desc, total_compras desc
limit 3;

-- 
SELECT u.user_id, u.nome,
       SUM(c.valor_compra) AS total_gasto,
       ROUND(100.0 * SUM(c.valor_compra) / t.total_geral, 2) AS pct_receita -- Calcula a participação percentual do total gasto desse cliente sobre a receita total.
FROM usuarios u
JOIN compras c
  ON u.user_id = c.user_id
CROSS JOIN (
    SELECT SUM(valor_compra) AS total_geral
    FROM compras
) t
GROUP BY u.user_id, u.nome, t.total_geral
ORDER BY total_gasto DESC
LIMIT 3;
```

# 🏆 Resultados — Top 3 Clientes
Nome	Total Gasto	% da Receita

Tiago Costa	R$ 210,90	37,22%

Ana Lima	R$ 200,50	35,38%

Mariana Almeida	R$ 99,99	17,64%


---
# 📌 Insight de Negócio (CRM)

Insight:
Os três principais clientes concentram quase toda a receita registrada.
Isso sugere a necessidade de uma régua VIP personalizada, com benefícios específicos como:

Frete grátis por 48 horas

Acesso antecipado a ofertas

Cupom exclusivo de agradecimento

Comunicação via email + WhatsApp

Impacto:
Aumenta a retenção e reduz risco de churn em clientes de alto valor.

Esses 3 clientes representam mais de 90% da receita total registrada no dataset.

--- 

# 🧩 Query — Quantidade de compras por usuário
```SQL
SELECT usuarios.nome, COUNT(*) AS total_compras
FROM usuarios
JOIN compras
  ON usuarios.user_id = compras.user_id
GROUP BY usuarios.nome;
```
---

# 🎯 Habilidades Demonstradas

Manipulação de dados (CSV)

SQL (SELECT, JOIN, GROUP BY, agregações)

Criação de segmentações de CRM

Identificação de clientes de alto valor

Geração de insights estratégicos

Interpretação de métricas de comportamento

Raciocínio analítico aplicado a CRM/Growth

---

## 📬 Autor

Yuri Borges
Projeto desenvolvido para portfólio e treinamento de análise de CRM.

