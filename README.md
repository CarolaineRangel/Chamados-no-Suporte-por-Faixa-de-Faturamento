Introdução
Esta análise investiga a relação entre os motivos dos chamados de suporte e as faixas de faturamento dos clientes, utilizando dados do Freshdesk a partir de janeiro de 2023. Além da avaliação de correlações estatísticas, aplicamos técnicas de clusterização para revelar padrões de comportamento entre os clientes.

Critérios de Inclusão
Foram considerados na análise apenas os chamados que:

Possuem motivo de nível 1 preenchido;

Estão associados a uma data de won (aquisição);

Possuem instalação identificada no atendimento.

O faturamento foi calculado com base no somatório de vendas até a data de abertura do ticket. Assim, um mesmo cliente pode aparecer em diferentes faixas de faturamento ao longo do tempo, permitindo uma análise mais dinâmica sobre quando e como o suporte é acionado em diferentes fases da jornada.

O tempo entre a venda e o chamado é calculado pela diferença entre a data de aquisição (Won) e a data de abertura do ticket.

1. Análise Exploratória
Distribuição de Chamados por Motivo e Faixa de Faturamento
O gráfico de calor mostra a frequência relativa dos motivos de chamados (nível 1) por faixa de faturamento:

<img width="1471" height="989" alt="image" src="https://github.com/user-attachments/assets/6b9f7e61-6c04-482a-ab6a-11fe0df5cb43" />

Principais Observações:

Clientes com faturamento > R$400K concentram a maior parte dos chamados, especialmente para o motivo "Instabilidade" (29,6%).

Motivos como “Dúvida” e “Solicitação” estão presentes de forma consistente em todas as faixas, sem diferenciação clara.

Teste de Associação (Cramér’s V)
Para avaliar a associação estatística entre motivo e faixa de faturamento, utilizamos o Cramér’s V, onde:

0 = Nenhuma associação

1 = Associação forte

Resultados:

| Nível do Motivo | Cramér’s V | Interpretação                |
|-----------------|------------|------------------------------|
| Nível 1         | 0.0735     | Baixíssima correlação        |
| Nível 2         | 0.0623     | Sem correlação significativa |
| Nível 3         | 0.0630     | Sem correlação significativa |

Conclusão:

Não há relação estatística significativa entre o motivo do chamado e a faixa de faturamento. Ou seja, clientes de diferentes portes acionam o suporte pelos mesmos motivos, dificultando qualquer previsão com base apenas no valor de faturamento.

Tempo desde a Venda ("Won") até o Chamado
Ao analisarmos o tempo entre a aquisição do cliente (won) e a abertura do primeiro chamado, encontramos um Cramér’s V de 0,2779, sugerindo associação moderada.

Por que isso importa?
Porque ajuda a entender quando os diferentes perfis de cliente e quando é maior sua necessidade de suporte.

Distribuição por Faixa de Faturamento:

<img width="1449" height="989" alt="image" src="https://github.com/user-attachments/assets/b9dc8f8c-b53f-466c-a3e4-81e631f01adf" />

Distribuição por Faixa de Faturamento:

Clientes com alto faturamento (> R$400K) tendem a acionar o suporte entre o 3º e o 20º mês.

Clientes com faturamento até R$5K concentram os chamados nos primeiros 2 meses, indicando possíveis dificuldades iniciais, especialmente na implementação.

2. Clusterização: Identificação de Padrões
Clusterização por Motivo do Chamado (K-Prototypes)
Mesmo considerando as faixas de faturamento e os motivos de nível 1, a ausência de correlação se mantém.

Foram identificados 4 clusters com os seguintes perfis:

<img width="1390" height="790" alt="image" src="https://github.com/user-attachments/assets/05eab188-cebc-419e-a6de-b896935b6ca3" />

| Cluster | Principais Motivos Associados                                                     | Faixas de Faturamento mais Presentes                                                                 |
|--------|-------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| 0      | Bug, Sugestão, Chat Cliente Ausente, Campanhas, Solicitação, Instabilidade        | Aparece com mais frequência nas faixas altas (ex.: "L. 200 a 250k", "M. 250 a 400k", "N. 400k+")     |
| 1      | Instabilidade, Chat Duplicado, Bug, Implementação                                  | Aparece em vários níveis, mas com destaque nas faixas médias-altas                                   |
| 2      | Instabilidade, Dúvidas, Sugestões                                                  | Distribuído entre faixas baixas e médias (ex.: "H. 50 a 80k", "K. 150 a 200k")                       |
| 3      | Dúvida, Solicitação, Implementação, Elogio                                         | Extremamente presente em quase todas as faixas, principalmente nas faixas menores                    |

Clusterização por Motivo de 2ª Ordem
A distribuição dos motivos de segundo nível reforça o padrão:

<img width="1183" height="1190" alt="image" src="https://github.com/user-attachments/assets/83d3b504-de10-42fb-bcc5-769aa1ea9ed2" />

Podemos visualizar a seguinte segmentação por cluster:

| Cluster | Principais Motivos de Chamado                          | Proporção Alta (%)                                             |
|--------|----------------------------------------------------------|------------------------------------------------------------------|
| 0      | Financeiro, Delivery, PDV, Outros, Fiscal               | Financeiro (17%), Delivery (16%), PDV (11%)                     |
| 1      | Financeiro, Delivery, Impressões, PDV, Outros           | Financeiro (17%), Delivery (15%), Impressões (15%), PDV (11%)   |
| 2      | Delivery, Impressões, Financeiro, PDV, Sem Tag          | Delivery (16%), Impressões (15%), Financeiro (12%), PDV (11%)   |
| 3      | Impressões, Delivery, PDV, Sem Tag, Produto             | Impressões (18%), Delivery (18%), PDV (16%)                     |

👉 Nenhuma segmentação clara por faturamento. Os motivos se distribuem de forma parecida entre os diferentes perfis.

Clusterização por Tempo até o Chamado
Agrupando pelo tempo desde a venda, os clusters revelam comportamentos distintos:

<img width="1391" height="790" alt="image" src="https://github.com/user-attachments/assets/744899b1-46e0-4e76-95ea-47ba3bb7eca7" />

| Cluster | Tempo até o Chamado | Faixa de Faturamento mais Presente        |
|--------|----------------------|--------------------------------------------|
| 0      | 3-10 meses           | Todas as faixas, especialmente menores    |
| 1      | 6-10 meses           | De 5k até 250k                            |
| 2      | 11-30 meses          | Faixas médias a altas                     |
| 3      | 0-2 meses            | Todas as faixas                           |

Interpretação:

O tempo entre o chamado revela comportamentos de engajamento distintos ao longo da jornada.

Clientes que chamam cedo (0-2 meses) estão mais nos clusters iniciais.

Clientes que demoram mais para acionar o suporte tendem a ter faturamento maior e estão nos clusters 1 e 2.

3. Conclusão
Não há associação significativa entre motivo do chamado e faixa de faturamento. Todos os perfis acionam o suporte por razões semelhantes.

Tempo até o chamado tem associação moderada com o faturamento. Esse é um ponto mais relevante para segmentação e entendimento do comportamento do cliente.

Clusterização com base nos motivos não diferencia perfis de faturamento, mas a clusterização por tempo até o chamado apresenta segmentações mais consistentes.

Clientes com menor faturamento tendem a ter problemas e acionar o suporte mais cedo, especialmente nos primeiros 2 meses.

Clientes com maior faturamento acionam o suporte de forma mais distribuída ao longo do tempo, podendo indicar maior complexidade ou uso mais intensivo da solução.
