# Projeto Final Bootcamp Data Science aplicada

Projeto de data science para o ultimo modulo do bootcamp de data science aplicada como requisito para certificação.

Indice:
- [Problemática](https://github.com/kaicque/Projeto-Final-Bootcamp-DS#problem%C3%A1tica)
- [Objetivo do trabalho](https://github.com/kaicque/Projeto-Final-Bootcamp-DS#objetivo-do-trabalho)
- [Escopo do projeto](https://github.com/kaicque/Projeto-Final-Bootcamp-DS/blob/main/README.md#escopo-do-projeto)
- - [Dados para analise](https://github.com/kaicque/Projeto-Final-Bootcamp-DS#dados-para-analise)
- - [Ciclo de análise e tratamento dos dados](https://github.com/kaicque/Projeto-Final-Bootcamp-DS#ciclo-de-an%C3%A1lise-e-tratamento-dos-dados)
- - [Teste de modelos de machine learning e melhoria de performance](https://github.com/kaicque/Projeto-Final-Bootcamp-DS#teste-de-modelos-de-machine-learning-e-melhoria-de-performance)
- - [Resultados dos modelos de machine learning](https://github.com/kaicque/Projeto-Final-Bootcamp-DS#resultados-dos-modelos-de-machine-learning)
- [Conclusão](https://github.com/kaicque/Projeto-Final-Bootcamp-DS#conclus%C3%A3o)
- [Agradecimentos](https://github.com/kaicque/Projeto-Final-Bootcamp-DS#agradecimentos)
- [Referência e documentação](https://github.com/kaicque/Projeto-Final-Bootcamp-DS#refer%C3%AAncia-e-documenta%C3%A7%C3%A3o)




https://github.com/kaicque/Projeto-Final-Bootcamp-DS/blob/main/README.md#escopo-do-projeto



# Problemática:

A pandemia causada pela doença da covid-19 fez com que o todo o mundo tomasse ações de isolamento nunca antes visto. Para evitar o contágio de uma doença sem registro histórico foi tomada a ação de isolamento social/quarentena. Mas isso não foi o suficiente para evitasse o contágio da população e a necessidade de cuidados médicos. 

Por falta de conhecimento de como tratar da doença, os hospitais viram seus leitos de UTI alcançarem níveis de lotação nunca antes praticados. Infelizmente em decorrência da doença e da lotação de UTI, muitas pessoas perderam suas vidas ou pessoas queridas. 

# Objetivo do trabalho:

Nosso objetivo que guiou o estudo é prever os pacientes que necessitaram de UTI de forma antecipada com a aplicação de modelos de machine learning. Para que com isso possam ser tomadas ações de dimensionamento de leitos, de funcionários e tentar remanejar pacientes que não correm risco para outros hospitais aos quais teriam leitos disponível afim de atender todas as pessoas necessitadas de cuidados médicos. 

# Escopo do projeto:

O desenvolvimento do trabalho foi dividido em 2 notebooks: 

* [Tratamento e analise dos dados;](https://github.com/kaicque/Projeto-Final-Bootcamp-DS/blob/main/Notebooks/Tratamento_dados.ipynb)
* [Desenvolvimento do modelo de machine learning.](https://github.com/kaicque/Projeto-Final-Bootcamp-DS/blob/main/Notebooks/Machine_Learning.ipynb)

E os dados utilizados podem ser encontrados no repositório do [git](https://github.com/kaicque/Projeto-Final-Bootcamp-DS/tree/main/Dados)

## Dados para analise:

Foi disponibilizado pelo hospital Sírio-Libanês no [Kaggle](https://www.kaggle.com/S%C3%ADrio-Libanes/covid19), o histórico médico de pacientes das unidades do estado de São Paulo e distrito federal. Nesses dados foram considerados diversos exames do paciente com a doença, durante o período em que ele ficou no hospital a fim de tentar prever o quanto antes quais pacientes provavelmente precisariam de cuidados intensivos.

Os dados disponibilizados contam com:

* Informações demográficas do paciente (03 - colunas)
* Doenças anteriores agrupadas de pacientes (09 - colunas)
* Resultado de exames de sangue (36 - colunas)
* Sinais vitais (06 - colunas)
* Intervalo de tempo em que o paciente ficou no hospital (01 - coluna)
* Confirmação da necessidade de internação (01 - coluna)

Além disso os dados, foram expandido quando pertinente à média, mediana, máximo, mínimo, diferença e diferença relativa.

No total a base de dados contem 1925 linhas que conta a história do período em que o paciente ficou no hospital.

## Ciclo de análise e tratamento dos dados:

Como nosso objetivo é prever de forma antecipada qual paciente necessitará de internação, foi filtrada somente a primeira janela de tempo em que o paciente ficou no hospital. 

Além do filtro de janela em que o paciente ficou no hospital, foram retirados da base os pacientes que foram para a UTI na primeira janela a fim de cumprir com o requisito de antecipar quais pacientes iriam precisar de UTI nas próximas janelas de tempo. 

Na descrição da base de dados no [Kaggle](https://www.kaggle.com/S%C3%ADrio-Libanes/covid19) cita que os pacientes onde não tiveram mudanças significativas nos resultados de exames entre uma janela e outra, foi deixado em branco. Por conta disso foi tratados os dados para preencher os dados faltantes com o resultado de exames anteriores ou posteriores, nessa ordem. 

Como os dados foram expandidos com média; mediana; máximo; mínimo; diferença; diferença relativa, é previsto que tenha dados com auto correlação. Esses dados com alta taxa de correlação podem atrapalhar o desempenho do modelo de machine learning, e por conta disso foram removidos da base de dados.

Por fim, após ter analisado como estavam os dados, feito os filtros e tratamentos, foi analisado como estava a distribuição dos pacientes que necessitaram de UTI em janelas futuras e os que não precisaram. 

A conclusão é que os dados dos que foram ou não para UTI estavam bem próximos, descartando possível viés de má distribuição dos dados. 


## Teste de modelos de machine learning e melhoria de performance:


Para iniciar o projeto de machine learning, foi utilizado a biblioteca ***LazyPredict*** para analisar melhores candidatos a  modelos de machine learning com maior taxa de precisão para esse conjunto de dados trabalhado.

Após o uso do LazyPredict, foi filtrado os 5 melhores modelos considerando os indicadores de precisão dos modelos. Como tivemos empate para o 2º e 3º lugar, foi escolhidos os seguintes **3** modelos com o intuito de diferenciar o modo de funcionamento de cada um.

Os modelos foram:
* XGBClassifier
* LogisticRegression
* ExtraTreesClassifier

Para facilitar o estudo dos modelos, foi elaborada algumas funções para automatizar a execução e conferência dos modelos. 

O roteiro de analise dos modelos foi organizado da seguinte forma para padronizar a execução:
-   Acurácia, AUC e Classification report
-   Matriz de confusão do modelo
-   Cross Validation
-   Gráfico da Curva ROC

Após a primeira bateria de teste dos modelos, com o intuito de buscar melhores resultados nos modelos, foi utilizado a biblioteca ***featurewiz***, que faz uma analise da combinação de colunas de dados e faz uma proposta de quais usar no modelo. 

## Resultados dos modelos de machine learning:

Com os resultados dos modelos e suas pontuações de precisão, foi visto que mesmo antes da utilização do ***featurewiz***, o modelo **ExtraTreesClassifier** apresentava os melhores resultados. Obtendo a **acurácia** de **81%** ele foi considerado o melhor modelo de machine learning entre os testados. 


# Conclusão:

Mesmo obtendo os melhores resultados e uma taxa de falso positivo e falso negativo relativamente baixos, nosso objetivo que é ter uma assertividade de 100%, e ele não foi atendido em sua totalidade. Como estamos tratando de vidas e os erros podem levar o paciente a óbito. 

Por isso é indicado cautela na implementação do modelo em produção. 

Em busca de melhores resultados, é proposto próximos passos para melhorar o resultado obtido:
-   Inclusão de outras janelas de tempo em que o paciente está no hospital.
-   Reavaliar juntamente com um especialista de enfermagem a exclusão das colunas com auto correlação. 

# Agradecimentos:
Primeiramente meu imenso agradecimento a todo o time da Alura, por tornar esse estudo e desafio possível.

Ao Scuba Team por toda a disponibilidade e auxilio nas dúvidas e desesperos no decorrer do curso. 

Aos professores pelo empenho e didática que tornaram a minha entrada no mundo de Data Science menos dolorosa, mesmo sem conhecimento prévio de python e o mundo de programação. 

E por ultimo, mas não menos importante, meu muito obrigado a todos os colegas de curso que interagiram no discord possibilitando a interação, ajuda e referência no decorrer do curso.


# Referência e documentação:
[Diferença de SVM para Logistic Regression](https://medium.com/axum-labs/logistic-regression-vs-support-vector-machines-svm-c335610a3d16)

[AUC: A Better Measure than Accuracy in Comparing Learning Algorithms](https://link.springer.com/chapter/10.1007/3-540-44886-1_25)

Bibliotecas:
[FeatureWiz](https://github.com/AutoViML/featurewiz)

[LogisticRegression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html)

[XGBoost](https://xgboost.readthedocs.io/en/latest/get_started.html)

[ExtraTreesClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.ExtraTreesClassifier.html)

[Pandas](https://pandas.pydata.org/docs/index.html)

[matplotlib](https://matplotlib.org/stable/contents.html)

[Seaborn](https://seaborn.pydata.org/)

[LazyPredict](https://lazypredict.readthedocs.io/en/latest/)
