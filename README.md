Link para o notebook através do nbviewer (Recomendado para uma melhor visualização): https://nbviewer.jupyter.org/github/Leonardodsch/fraud-detection/blob/main/notebooks/cycle06-business_performance.ipynb

# Financial Fraud Detection

Disclaimer: O Contexto a seguir, é completamente fictício, a empresa, o contexto, as perguntas de negócio foram criadas apenas para o desenvolvimento do projeto, e se baseiam em um projeto do site https://sejaumdatascientist.com/.

## Contexto de negócio 

A Blocker Fraude Company é uma empresa especializada na detecção de fraudes em transações financeiras feitas através de dispositivos móveis. A empresa tem um serviço chamado “Blocker Fraud” no qual garante o bloqueio de transações fraudulentas.

E o modelo de negócio da empresa é do tipo Serviço com a monetização feita por performance do serviço prestado, ou seja, o usuário paga uma taxa fixa sobre o sucesso na detecção de fraude das transações do cliente.

Porém, a Blocker Fraud Company está em fase de expansão no Brasil e para adquirir clientes mais rapidamente, ela adotou uma estratégia muito agressiva. A estratégia funciona da seguinte forma:

1. A empresa vai receber 25% do valor de cada transação detectada verdadeiramente como fraude.
2. A empresa vai receber 5% do valor de cada transação detectada como fraude, porém a transação é verdadeiramente legítima.
3. A empresa vai devolver 100% do valor para o cliente, a cada transação detectada como legítima, porém a transação é verdadeiramente uma fraude.

Com essa estratégia agressiva a empresa assume os riscos em falhar na detecção de fraude e é remunerada na detecção assertiva das fraudes.

Para o cliente, é um excelente negócio contratar a Blocker Fraud Company. Apesar da taxa cobrada ser muito alta sobre o sucesso, 25%, a empresa reduz seus custos com transações fraudulentas detectadas corretamente e ainda o prejuízo causado por um erro do serviço de anti-fraude será coberto pela própria Blocker Fraud Company.

Para a empresa, além de conseguir muitos clientes com essa estratégia arriscada em garantir o reembolso no caso de uma falha na detecção de fraude do cliente, ela depende somente da precisão e da acurácia dos modelos construídos pelos seus Cientistas de Dados, ou seja, quanto mais preciso for o modelo “Blocker Fraud”, maior o faturamento da empresa. Porém, se o modelo tiver baixa precisão, a empresa poderá ter um prejuízo enorme.

## O Desafio

Você foi contratado como um Consultor de Ciência de Dados para criar um modelo de alta precisão e acurácia na detecção de fraudes de transações feitas através de dispositivos móveis.

Ao final da sua consultoria, você precisa entregar ao CEO da Blocker Fraud Company um modelo em produção no qual seu acesso será feito via API, ou seja, os clientes enviarão suas transações via API para que o seu modelo as classifique como fraudulentas ou legítimas.

Além disso, você precisará entregar um relatório reportando a performance e os resultados do seu modelo em relação ao lucro e prejuízo que a empresa terá ao usar o modelo que você produziu. No seu relatório deve conter as respostas para as seguintes perguntas:

1. Qual a Precisão e Acurácia do modelo?
2. Qual a Confiabilidade do modelo em classificar as transações como legítimas ou fraudulentas?
3. Qual o Faturamento Esperado pela Empresa se classificarmos 100% das transações com o modelo?
4. Qual o Prejuízo Esperado pela Empresa em caso de falha do modelo?
5. Qual o Lucro Esperado pela Blocker Fraud Company ao utilizar o modelo?

## Dados 

O conjunto de dados que será utilizado para criar a solução está disponível na plataforma do Kaggle. Esse é o link: https://www.kaggle.com/ealaxi/paysim1

Cada linha representa um cliente e cada coluna contém alguns atributos que descrevem esse cliente. O conjunto de dados inclui informações sobre:

- **step** - mapeia uma unidade de tempo no mundo real. Neste caso, 1 etapa corresponde a 1 hora de tempo. Total de etapas 744 (simulação de 30 dias).

- **type** - CASH-IN, CASH-OUT, DEBIT, PAYMENT and TRANSFER.

- **amount** - valor da transação em moeda local.

- **nameOrig** - cliente que iniciou a transação

- **oldbalanceOrg** - saldo inicial antes da transação

- **newbalanceOrig** - saldo após a transação

- **nameDest** - cliente que é o destinatário da transação

- **oldbalanceDest** - saldo inicial  do destinatário antes da transação. Observe que não há informações para clientes que começam com M (Merchants).

- **newbalanceDest** - novo saldo do destinatário após a transação. Observe que não há informações para clientes que começam com  M (Merchants).

- **isFraud** - São as transações feitas pelos agentes fraudulentos dentro da simulação. Neste conjunto de dados específico, o comportamento fraudulento dos agentes visa lucrar ao assumir o controle das contas dos clientes e tentar esvaziar os fundos transferindo para outra conta e retirando do sistema.

- **isFlaggedFraud** - O modelo de negócios visa controlar as transferências em massa de uma conta para outra e sinaliza tentativas ilegais. Uma tentativa ilegal neste conjunto de dados é uma tentativa de transferir mais de 200.000 em uma única transação.


## Planejamento da solução

**1. Entendimento do negócio e problemas e serem resolvidos** - Buscar entender os reais motivos da necessidade da previsão de detecção de fraudes e como o probelma pode ser resolvido através de machine learning, quais aspectos serão considerados na hora da predição e quão melhor a solução proposta pode ser considerando os modelos de predição utilizados atualmente na empresa.    

**2. Coleta de dados** - Acesso a plataforma do Kaggle para download dos arquivos que serão usados.

**3. Limpeza dos dados** - Os dados são analisados usando diferentes técnicas para verificar a existência de dados faltantes, outliers (valor discrepantes) , ou qualquer tipo de inconsistências para que assim possam ser tratados devidamente e não impactar nas análises futuras. 

**4. Exploração dos dados** - Busca um melhor entendimento do negócio através da geração de insights e das variáveis mais importantes na modelagem do modelo de Machine Learning. Diversas hipóteses foram levantadas e validadas para obtenção de um conhecimento de negócio mais profundo, verificando também a correlação entre os atributos para que se possa ter uma ideia da importância de cada um para o modelo de machine learning. 

**5. Preparação dos dados** - Os dados foram transformados, balanceados e regularizados para que atendam as premissas de funcionamento dos algoritmos de machine learning, nesta etapa é importante deixar os dados preparados para que os algoritmos possam ter o melhor desempenho possível, e possíveis inconsistencias no dataset não interfiram no resultado final.

**6. Seleção de features** - Após a preparação dos dados nesta seção algoritmos, como o Boruta e o feature importance, selecionarão as melhores colunas a serem utilizadas para o treinamento do modelo de machine learning. Elas serão analisadas e selecionadas de acordo com descobertas feitas na análise exploratória e levando em conta o contexto de nagócio.

**7. Aplicação dos algoritmos de machine learning** - Nesta etapa foram escolhidos os algoritmos de machine learning que seriam usados e então os mesmos foram treinados com os dados já preparados e prontos, cada algoritmo foi testado usando seus devidos parâmetros e posteriormente estratégias de cross validation foram usadas para verificar o real resultado do medelo, bem como tecnicas de hyperparameter fine tunning para encontrar os melhores parâmetros para o modelo escolhido. 

**8. Avaliação do algoritmo** - O algoritmo é avaliado com base em algumas métricas e nesse ponto verifica-se ou não a necessidade de realizar mais um ciclo para melhorar o desempenho final.

**9. Tradução do erro em métricas de negócio** - Com o melhor modelo escolhido, treinado e otimizado a taxa de erro encontrada é trasnformada em métricas de negócio para que se saiba concretamente quanto de retorno financeiro a solução trouxe para a empresa. 

**10. Deploy do modelo em produção** - O modelo é colocado em produção no ambiente cloud Heroku para que as predições possam ser utilizadas através de requisições a uma API.

O projeto utiliza a metodologia CRISP-DM, que consiste desenvolver o projeto de forma ciclica entendendo todos os passos do projeto e buscando entregar valor ao negócio o mais rápido possível e aperfeiçoar a solução a cada ciclo.

<p align="center">
  <img width="500" height="400" src="https://user-images.githubusercontent.com/76128123/129281894-1a9389f5-e953-4c7d-ad6a-cadbc62e9abc.png"/>
</p>

## Melhores Insights

-  **Valores de transações menores de 2 milhões possuem 50% a mais de fraudes**

<p align="center">
  <img width="650" height="400" src="https://user-images.githubusercontent.com/76128123/130164842-ea115d15-cb0a-4c5d-8087-9cc8ec6218e7.png"/>
</p>

- **Operações do tipo CASH OUT possuem 3% a mais de fraudes. Obs: Apenas operações do tipo TRANSFER e CASH OUT possuem casos de fraude.**

<p align="center">
  <img width="650" height="400" src="https://user-images.githubusercontent.com/76128123/130165042-d1f723d0-37e5-462d-bf6f-c10827eabbda.png"/>
</p>

- **Operações realizadas nos 15 primeiros dias possuem o mesmo número de fraudes das operações realizadas nos ultimos 15 dias.**

<p align="center">
  <img width="650" height="400" src="https://user-images.githubusercontent.com/76128123/130165110-63f8c51b-2a42-4f6d-b827-b5fa2b15841d.png"/>
</p>

## Machine Learning Models

## Resultados

## Conclusões
