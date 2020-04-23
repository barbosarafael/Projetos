# Apresentação, introdução, iniciação ao problema...

---

Esse é um famoso banco de dados que provém de uma competição do [Kaggle](https://www.kaggle.com/c/house-prices-advanced-regression-techniques). Ele está disponível neste [link](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data) e tem a seguinte descrição

**Comece aqui se**:

1. Você tem experiência com R ou Python; e
2. Conhece um pouco sobre aprendizado de máquina;

Ideal para uma pessoa que está aprendendo análise de dados em Python (em R eu já estou em um nível relativamente intermediário) e também aprendizado de máquina (igual eu, neste momento). 

## Descrição da competição 

---

Esse é um banco de dados *playground*, justamente para aplicarmos tudo aquilo que aprendemos em análise de dados e previsão. Também menciona a parte que muitas coisas, como o número de banheiros, influencia no valor de uma casa.

O banco de dados possui 79 variáveis explicativas, estas referem aos aspectos residenciais de casas da cidade de Ames em Iowa.

## Objetivo

---

A partir destas 79 variáveis explicativas, isto é, as características das casas, prever o valor de casa. 

## Habilidades que serão praticadas (segundo o Kaggle)

---

1. Criatividade na criação da *feature engineering* (recomendo pesquisar no Google caso não saiba o que é isso); e
2. Para a parte de previsão (aprendizado de máquina): utilização de regressão, random forest, gradient boosting, etc.

## Métrica para verificação dos resultados

---

Será utilizado o Root-Mean-Squared-Error (RMSE), para os mais intimos, a raiz do erro quadrático médio, entre o *log* do valor que o nosso modelo preveu, ou estimou, ($ \hat{y_i} $) e o real valor da casa ($ y $). A fórmula para o RMSE é dada por

$$ RMSE = \sqrt{\frac{1}{n}\sum_{i = 1}^{n} (\hat{y_i} - y_i)^2} $$ 

# Análise Exploratória dos Dados
