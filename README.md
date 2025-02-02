# Projeto Detecção de Fraude

Classificação para transações fraudentas ou não

![deteccao_fraude](img/imagem_projeto.jpg)

## 1.	Problema de negócio
A detecção inadequada ou a falta de dados precisos sobre transações fraudulentas pode levar a prejuízos financeiros significativos, subnotificação ou supernotificação de fraudes, além de dificultar o monitoramento eficaz de comportamentos fraudulentos. Isso também pode resultar em ineficiência na alocação de recursos para investigação, levando a custos desnecessários com falsos alarmes ou, por outro lado, à não detecção de fraudes reais, o que prejudica a segurança do sistema e a confiança do cliente. A falta de precisão na classificação de transações impacta diretamente a eficácia das políticas de segurança e a confiança dos consumidores, além de prejudicar a análise de dados financeiros para futuras estratégias de prevenção.

## 2.	Objetivo
Criar um sistema robusto de detecção de fraudes que permita a identificação precisa de transações fraudulentas em tempo real. Este sistema visa reduzir a ocorrência de fraudes, minimizar os custos com investigações desnecessárias, e melhorar a alocação de recursos para a análise de transações suspeitas. Além disso, o sistema deve possibilitar a atualização contínua das regras de detecção com base nos dados mais recentes, contribuindo para a evolução das estratégias de prevenção e garantindo maior confiança e segurança nas transações financeiras.

## 3.	Premissas do negócio
Seguem abaixo a premissa para quantificar o impacto financeiro do algoritmo na detecção ou não de transações fraudentas:
Fórmula utilizada:
Custo de Falsos Positivos = Custo por Investigação * Número de Falsos Positivos
Onde 
- **Custo por Investigação** é o custo médio para investigar uma transação que o modelo classificou como fraude, mas que na verdade é legítima.
- **Número de Falsos Positivos** é o total de transações legítimas que foram classificadas como fraudes pelo modelo.
- **custo_por_investigacao** é 100 unidades monetárias

## 4.	Estratégia adotada para solução

Passo 1 - Descrição dos dados: O objetivo deste passo é ter um entendimento inicial de como os dados estão relacionados com o problema de negócio proposto, para tal, lançando mão de algumas métricas estatísticas de posição e distribuição.

Passo 2 - Engenharia de atributos: Neste passo foram criadas novas variáveis a partir das variáveis originais a fim de melhorar a qualidade dos dados facilitando seu o entendimento.

Passo 3 - Filtragem das variáveis: No processo de filtragem, busca-se selecionar e reter apenas as variáveis relevantes para a análise ou modelagem, com base nos objetivos do negócio e nas características do problema em questão.
 
Passo 4 - Análise exploratória: A análise exploratória dos dados (EDA) tem como principal objetivo proporcionar uma compreensão mais aprofundada dos dados, tais como: Compreender a distribuição das variáveis numéricas e categóricas, identificar outliers (valores atípicos), se existe desbalanceamento da variável resposta, correlações entre as variáveis entre outras análises.

Passo 5 - Preparação dos dados: Neste tópico, os dados serão transformados, ou seja, as variáveis categóricas serão convertidas em números, pois os algoritmos de machine learning não tem uma boa performance com dados não numéricos. Os dados também precisarão ser reescalados, ou seja, colocar as variáveis em uma escala comum.
 
Passo 6 - Seleção das variáveis: Neste passo o principal objetivo é selecionar as variáveis mais relevantes e descartar as menos importantes, para que estas sejam submetidas aos algoritmos de machine learning. Esta seleção é feita através de algoritmos específicos de seleção, com isso, busca-se reduzir a dimensionalidade dos dados sem perder em performance ao resultado final.

Passo 7 - Treinar o modelo com as variáveis mais relevantes: Com a definição do melhor modelo de machine learning e as variável mais relevantes, busca-se otimizar ainda mais a performance do modelo com alguns ajustes finos em seus hiperparâmetros.
 
Passo 8 - Performance do negócio: Nesta etapa, o termo "performance do negócio" refere-se ao impacto que os modelos e análises têm nos resultados e metas de uma organização, pois busca garantir que as soluções propostas realmente tragam benefícios tangíveis para a empresa.

## 5.	Top 3 insights
Hipótese 1: Pessoas que vivem no interior de Santa Catarina não teriam tendência a contrair covid?
Falsa: Pessoas que vivem no interior de Santa Catarina teriam sim maior tendência a contrair covid.

![deteccao_fraude](img/grafico_hipotese_1.JPG)

Hipótese 2: Cidades da região sul tem maior tendência a contrair doenças respiratórias?
Falsa: Cidades da região sul não tem maior tendência a contrair doenças respiratórias e sim a região sudeste.

![deteccao_fraude](img/grafico_hipotese_2.JPG)

Hipótese 3: Pessoas que tomaram antiviral tiveram menos sintomas graves?
Falsa: Pessoas que não tomaram antiviral tiveram mais sintomas graves.

![deteccao_fraude](img/grafico_hipotese_3.JPG)

## 6.	Aplicação do modelo de machine learning
Foram feitos testes com vários algoritmos de machine learning, utilizando a técnica de cross-validation e ajuste fino dos parâmetros.

![Comparativo](img/comparativo_algoritmos.JPG)

## 7.	Performance do modelo de machine learning
O algoritmo de machine learning escolhido foi o XGBRegressor, pois para o problema de negócio em questão a métrica mais relevante seria o RECALL e este algoritmo teve o melhor desempenho neste quesito.
 
![deteccao_fraude](img/melhor_algoritmo.JPG)

## 8.	Resultado do negócio
Para avaliar qual modelo é melhor em termos de custo, iremos considerar o custo associado aos falsos negativos (quando o modelo não identifica corretamente um caso positivo). 

O recall representa a proporção de casos positivos que o modelo identifica corretamente em relação ao total de casos positivos reais. 

Portanto, um recall mais alto indica que o modelo está identificando mais casos positivos. Iremos multiplicar o número de falsos negativos de cada classe pelo custo associado a essa classe.
Para título de comparação em relação aos custos hospitalares envolvidos, definiu-se valores para cada tipo de SRAG:

• influenza -> 50 unidades monetárias;
 
• outro vírus respiratório -> 60 unidades monetárias;

• agente etiológico -> 80 unidades monetárias;

• não especificado -> 30 unidades monetárias;

• COVID-19 -> 90 unidades monetárias.
 
 ![deteccao_fraude](img/resultado_negocio.JPG)

Neste caso, a proporção do custo de internação por paciente em relação a uma classificação com algoritmo de média em comparação com o melhor algoritmo resulta em uma redução de mais de 60%.

## 9.	Conclusão
Neste projeto, avaliamos diferentes modelos de classificação para identificar casos de Síndrome Respiratória Aguda Grave (SRAG) e os comparamos em termos de custo associado aos falsos negativos. Utilizando o recall como métrica principal, buscamos maximizar a identificação correta de casos positivos, minimizando os custos hospitalares associados a cada tipo de SRAG.

Os resultados mostraram que a proporção do custo de internação por paciente utilizando o melhor algoritmo em comparação com um algoritmo de média resultou em uma redução de mais de 60%. Este achado destaca a importância de uma classificação precisa para otimizar a alocação de recursos e reduzir os custos hospitalares. A implementação de um modelo de classificação eficaz pode melhorar significativamente a resposta a surtos de SRAG, auxiliando na tomada de decisões mais informadas e na implementação de medidas de saúde pública mais eficazes.

Criado um formulário eletrônico na Web onde é possivel preencher os dados do paciente para obter a classificação prevista. 
![deteccao_fraude](img/formulario_medico.jpg)

## 10.	Próximos passos
•	Utilizar outras técnicas para tratamento de grandes dados;

•	Testar outros algoritmos de machine learning;

•	Implementar mais variáveis para definir melhor o comportamento dos clientes;

•	Fazer o deploy deste projeto em ambiente cloud. 
