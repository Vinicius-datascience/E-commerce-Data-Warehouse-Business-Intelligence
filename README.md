# 🛒 E-Commerce Data Warehouse & Analytics Dashboard

> **Projeto End-to-End:** Estruturação de Data Warehouse, Modelagem Dimensional (Star Schema), Engenharia de Dados em DAX e Construção de Dashboard Executivo para Tomada de Decisão em E-Commerce.

---

## 📌 Visão Geral do Projeto
Este projeto tem como objetivo transformar dados públicos de uma operação de e-commerce brasileira em informações estratégicas para apoiar a tomada de decisão.
A partir do conjunto de dados públicos da Olist, foram desenvolvidas etapas de organização, transformação e modelagem dos dados em um Data Warehouse, seguidas da construção de um dashboard interativo no Power BI.
A solução permite analisar indicadores de vendas, pedidos, clientes, produtos e logística, além de identificar padrões de comportamento, pontos de atenção e oportunidades de melhoria para o negócio.
O projeto reúne conceitos e práticas de SQL, PostgreSQL, modelagem dimensional, análise de dados, DAX e Business Intelligence, demonstrando o fluxo de trabalho desde os dados de origem até a apresentação dos resultados.

---

## 🎯 Objetivos do projeto
	●	Estruturar dados de diferentes áreas do e-commerce em uma base organizada para análise.
	●	Desenvolver um Data Warehouse com modelagem dimensional.
	●	Integrar informações comerciais, cadastrais e operacionais.
	●	Criar indicadores para acompanhar o desempenho do negócio.
	●	Explorar padrões de vendas, recorrência de clientes e eficiência logística.
	●	Traduzir os resultados das análises em insights e recomendações estratégicas.

---

## 💼 Problema de Negócio
Uma operação de e-commerce gera dados de diferentes processos, como vendas, pedidos, clientes, produtos, pagamentos e entregas.
Quando essas informações são analisadas isoladamente, torna-se mais difícil obter uma visão integrada do negócio, acompanhar indicadores e identificar oportunidades de melhoria.
Diante desse cenário, o projeto busca responder a perguntas relevantes para a gestão:

  - 	Como evoluíram as vendas e os pedidos ao longo do período analisado?
	
  - 	Quais categorias de produtos apresentam maior participação no faturamento?
	
  - 	Qual é o comportamento de compra dos clientes?
	
  - 	Qual é a proporção de clientes que realizaram mais de um pedido?
	
  - 	Como o desempenho comercial varia entre os estados brasileiros?
	
  - 	Quais diferenças regionais existem nos indicadores logísticos?
	
  - 	Quais oportunidades podem contribuir para melhorar a recorrência de compra e a experiência do cliente?
A proposta é organizar os dados em uma estrutura analítica consistente e disponibilizar indicadores que facilitem a exploração dessas questões.

---

## 📂 Fonte de Dados e Escopo da Análise
O projeto utiliza o conjunto de dados público Brazilian E-Commerce Public Dataset by Olist, disponibilizado na plataforma Kaggle.
A base reúne informações relacionadas a pedidos, clientes, produtos, vendedores, pagamentos, avaliações e localização geográfica.
Principais conjuntos de dados utilizados:

| Conjunto de dados	| Finalidade analítica |
|---|---|
| Orders | Acompanhamento dos pedidos, datas e status operacionais |
| Order Items	| Análise das vendas, dos produtos e do frete |
| Customers	| Análise da base de clientes e da distribuição geográfica |
| Products | Análise das categorias e características dos produtos |
| Sellers |	Análise dos vendedores |
| Payments |	Informações sobre os pagamentos dos pedidos |
| Reviews |	Informações relacionadas às avaliações dos clientes |
| Geolocation	| Apoio às análises geográficas |
| Product Category Translation |	Tradução dos nomes das categorias de produtos |

## Dimensão dos dados
A exploração das bases identificou os seguintes volumes:

| Indicador	| Quantidade |
|---|---|
| Pedidos |	99.441 |
| Clientes | cadastrados na base	96.096 |
| Itens de pedidos |	112.650 |
| Produtos distintos na base original	| 32.951 |
| Vendedores |	3.095 |
| Registros de pagamentos |	103.886 |
| Registros de avaliações	| 99.224 |
| Registros de geolocalização |	1.000.163 |
| Categorias de produtos |	71 |

Período dos dados: setembro de 2016 a outubro de 2018, considerando a cobertura identificada na base de origem.
> Nota sobre a cobertura temporal: o período final apresenta cobertura parcial. Por esse motivo, a evolução mensal das vendas deve ser interpretada considerando a disponibilidade dos dados, evitando conclusões equivocadas a partir de meses incompletos.

---

## 📐 Arquitetura do Data Warehouse & Modelagem

Para organizar as informações e facilitar as análises, foi desenvolvido um Data Warehouse em PostgreSQL, com separação entre as estruturas de preparação dos dados e as tabelas destinadas à análise.
Organização dos schemas

	staging: camada de preparação e armazenamento inicial dos dados importados.
	
    dw: camada analítica, organizada por meio de tabelas fato e dimensão.

Essa separação favorece a organização do processo de tratamento e a construção de uma estrutura adequada para consultas analíticas.

## Modelo dimensional

A camada analítica utiliza uma abordagem de modelagem dimensional baseada em Star Schema (Esquema Estrela).
O modelo reúne duas tabelas fato e quatro tabelas dimensão.
* **Tabelas Fato:**
  * `dw_fact_orders`: Registra o ciclo de vida dos pedidos, status e métricas operacionais.
  * `dw_fact_sales`: Registra as transações no nível de item de produto, faturamento e frete.

* **Tabelas Dimensão:**
  * `dw_dim_customer`: Dados demográficos e localização dos clientes.
  * `dw_dim_product`: Categorias, subcategorias e atributos dos produtos.
  * `dw_dim_seller`: Mapeamento de vendedores e origens.
  * `dw_dim_date`: Tabela dCalendario completa para análise de inteligência temporal.

A separação entre fatos e dimensões permite explorar diferentes perspectivas do negócio, relacionando indicadores comerciais e operacionais a atributos de clientes, produtos, vendedores e datas.
> Importante: os indicadores de faturamento apresentados neste projeto representam os valores de produtos e frete considerados na análise. Eles não devem ser interpretados como lucro líquido ou margem de lucro.


---

## 🔄 Etapas de Desenvolvimento
O projeto foi desenvolvido em etapas, partindo dos dados de origem até a construção da camada de visualização.

Etapa 1 — Exploração dos dados

Análise inicial dos arquivos disponibilizados para compreender sua estrutura, identificar campos relevantes e conhecer as informações disponíveis.

Principais atividades:
	
  - 	Identificação das tabelas e de seus relacionamentos.
	
  - 	Verificação dos volumes de registros.
	
  - 	Exploração dos atributos comerciais e operacionais.
	
  - 	Identificação dos campos necessários às análises propostas.

Etapa 2 — Preparação e organização dos dados

Organização dos dados importados no PostgreSQL, utilizando a camada staging como estrutura de preparação.
Essa etapa estabelece uma separação entre os dados de origem e as tabelas organizadas para análise.

Etapa 3 — Construção do Data Warehouse

Criação da estrutura analítica no schema dw, com tabelas fato e dimensão.
O objetivo foi organizar as informações de acordo com suas finalidades analíticas e permitir consultas integradas sobre vendas, pedidos, clientes, produtos, vendedores e datas.

Etapa 4 — Modelagem e integração

Estruturação do modelo dimensional para conectar os indicadores às diferentes perspectivas de análise.
Essa organização permite investigar, por exemplo, o desempenho de categorias de produtos, a distribuição geográfica dos clientes e os resultados comerciais ao longo do tempo.

Etapa 5 — Construção dos indicadores

Desenvolvimento de medidas e indicadores analíticos utilizados no dashboard, incluindo métricas de vendas, pedidos, clientes, ticket médio, recorrência e logística.
O DAX foi utilizado na camada analítica do Power BI para apoiar os cálculos e as análises apresentadas no relatório.

Etapa 6 — Desenvolvimento do dashboard

Construção de um relatório interativo no Power BI, organizado em cinco páginas temáticas.
A estrutura foi planejada para facilitar a navegação entre a visão executiva, as análises detalhadas e as recomendações decorrentes dos resultados.

---

## 🖥️ Navegação e Estrutura do Dashboard

O relatório é composto por **5 páginas focadas na jornada do negócio**:

### 1️⃣ Visão Executiva (Executive Overview)
* **Objetivo:** Fornecer à alta gestão uma visão rápida dos KPIs globais de desempenho (Faturamento, Pedidos, Clientes e Ticket Médio).
* **Destaques:** Acompanhamento temporal de vendas, concentração geográfica de entregas e distribuição de status dos pedidos.
![Visão Executiva](./caminho_da_imagem/executivo.png)

---

### 2️⃣ Vendas & Produtos (Sales Analytics)
* **Objetivo:** Analisar a performance comercial por categoria e identificar o mix de produtos.
* **Destaques:** Análise de Pareto/Matriz de faturamento, Treemap de participação por categoria e Gráfico de Dispersão (Volume Vendido vs. Faturamento).
![Vendas](./caminho_da_imagem/vendas.png)

---

### 3️⃣ Clientes & Recorrência (Customer Insights)
* **Objetivo:** Avaliar o comportamento de compra da base, distribuição geográfica e taxa de retenção.
* **Destaques:** Segmentação de frequência de pedidos, valor médio gerado por cliente por estado e métricas de LTV/Recorrência.

---

### 4️⃣ Logística & Operação (Supply Chain & Logistics)
* **Objetivo:** Mapear a eficiência de entrega, custos de frete por estado e prazos médios por região.
* **Destaques:** Diagnóstico de gargalos logísticos em estados críticos (ex: RR e AP) e evolução de custos operacionais.

---

### 5️⃣ Principais Descobertas da Análise

A análise dos dados permitiu identificar padrões relevantes sobre o comportamento dos clientes, a distribuição do faturamento e a operação logística.
Insight 1 — Baixa recorrência de compra
Aproximadamente 3,12% dos clientes identificados realizaram mais de um pedido no período analisado.
Esse resultado demonstra uma forte concentração de clientes com apenas uma compra registrada na base histórica.
Oportunidade identificada: investigar estratégias de relacionamento e incentivo à segunda compra, considerando que o histórico disponível não permite concluir, isoladamente, que esses clientes abandonaram a marca.

Insight 2 — Concentração do faturamento em categorias
Algumas categorias apresentam participação expressiva no faturamento analisado.

Entre os destaques estão:

| Categoria |	Faturamento aproximado |
|---|---|
|Beleza e Saúde |	R$ 1,258 milhão |
| Relógios e Presentes |	R$ 1,205 milhão |

Esses resultados indicam categorias relevantes para o desempenho comercial da operação.
* Oportunidade identificada: avaliar ações comerciais, campanhas e estratégias de estoque considerando a participação dessas categorias e seu potencial de crescimento.

Insight 3 — Volume de clientes não significa maior valor médio por cliente
A distribuição geográfica dos clientes e o valor médio associado a eles apresentam diferenças entre os estados.
Isso indica que a quantidade de clientes de uma região, isoladamente, não representa toda a sua contribuição comercial.
Oportunidade identificada: considerar estratégias regionais distintas, combinando aquisição de clientes, aumento do ticket médio e incentivo à recorrência.

Insight 4 — Diferenças regionais no desempenho logístico
A análise identificou variações nos prazos médios de entrega entre os estados.

Entre os resultados observados, Roraima apresentou prazo médio próximo de 29 dias, enquanto o Amapá apresentou média próxima de 27 dias.
Oportunidade identificada: investigar os fatores associados aos prazos elevados, considerando rotas, transportadoras, custos e características regionais da operação.

> Os resultados refletem o conjunto de dados histórico analisado. Eles devem ser interpretados dentro do período e da cobertura da base, sem pressupor que representem necessariamente a situação atual do mercado.

----

## 💡 7. Recomendações para o Negócio
A partir das descobertas, foram identificadas três frentes prioritárias de oportunidade.

Prioridade 1 — Recorrência e relacionamento com clientes

Desafio: baixa proporção de clientes com mais de um pedido registrado.
Recomendações:
*	Avaliar campanhas de pós-venda.
*	Estudar incentivos para a segunda compra.
*	Segmentar ações por categoria e perfil de consumo.
*	Acompanhar indicadores de recompra e frequência de pedidos.

Resultado esperado: ampliar as oportunidades de relacionamento e estimular novas compras.

Prioridade 2 — Desempenho comercial

Desafio: concentração de parte relevante do faturamento em determinadas categorias e diferenças entre regiões.
Recomendações:
*	Monitorar categorias com maior contribuição para o faturamento.
*	Avaliar oportunidades de crescimento em outras categorias.
*	Desenvolver estratégias comerciais considerando as características regionais.
*	Acompanhar a evolução do ticket médio e da participação das categorias.

Resultado esperado: apoiar decisões comerciais mais direcionadas e identificar oportunidades de crescimento.

Prioridade 3 — Eficiência logística

Desafio: diferenças regionais nos prazos de entrega.
Recomendações:
*	Investigar os fatores associados aos prazos mais elevados.
*	Avaliar alternativas de transporte e distribuição.
*	Comparar prazos de entrega e custos de frete por região.
*	Monitorar indicadores de desempenho logístico.

Resultado esperado: identificar oportunidades de melhoria nos prazos e na eficiência operacional.

> Importante: as recomendações representam oportunidades identificadas a partir dos dados. Sua implementação e seus impactos precisam ser avaliados em etapas posteriores.

---

## 🛠️ Tecnologias e Ferramentas

| Tecnologia |	Aplicação no projeto |
|---|---|
|PostgreSQL	| Armazenamento, organização e consultas aos dados |
| SQL	| Consultas e estruturação da camada analítica |
| pgAdmin	| Administração e gerenciamento do banco de dados |
| Power BI	| Construção do dashboard interativo |
| DAX	| Criação de medidas e indicadores analíticos |
| Modelagem dimensional| 	Organização das tabelas fato e dimensão |
| Git e GitHub |	Versionamento e documentação do projeto |

___

## 📈 Resultados do Projeto

O projeto resultou na construção de uma solução analítica que conecta a organização dos dados à exploração de indicadores de negócio.
Entre os principais resultados estão:
*	Estruturação de um Data Warehouse em PostgreSQL.
*	Organização dos dados em tabelas fato e dimensão.
*	Desenvolvimento de um modelo analítico para integrar diferentes áreas do e-commerce.
*	Construção de um dashboard com cinco páginas temáticas.
*	Análise de indicadores comerciais, de clientes e de logística.
*	Identificação de padrões de compra e concentração do faturamento.
*	Elaboração de recomendações baseadas nas descobertas da análise.

Além do desenvolvimento técnico, o projeto demonstra a aplicação de uma abordagem orientada a problemas de negócio: organizar dados, construir indicadores, interpretar resultados e comunicar oportunidades de melhoria.

---

## 👨🏾‍💻 Sobre o Projeto

Este projeto faz parte do meu desenvolvimento profissional na área de Análise de Dados, Ciência de Dados e Business Intelligence.
A iniciativa reúne conhecimentos de SQL, PostgreSQL, modelagem dimensional, Power BI e análise de dados, com foco em transformar dados em informações relevantes para apoiar decisões de negócio.
Meu objetivo é continuar desenvolvendo soluções analíticas que combinem conhecimento técnico, visão de negócio e comunicação clara dos resultados.
Conecte-se comigo no LinkedIn e explore outros projetos no GitHub.









