
# Carregando as bibliotecas


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

# Configurações adicionais


```python
plt.style.use("seaborn-muted")
%matplotlib inline
pd.set_option('display.max_columns', None)


from google.colab import drive
drive.mount("/content/drive", force_remount = True)
```

    Mounted at /content/drive


# Carregando o banco de dados


```python
banco = pd.read_csv("/content/drive/My Drive/Training_Dataset_v2.csv", low_memory = False)
```


```python
banco.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1687861 entries, 0 to 1687860
    Data columns (total 23 columns):
     #   Column             Non-Null Count    Dtype  
    ---  ------             --------------    -----  
     0   sku                1687861 non-null  object 
     1   national_inv       1687860 non-null  float64
     2   lead_time          1586967 non-null  float64
     3   in_transit_qty     1687860 non-null  float64
     4   forecast_3_month   1687860 non-null  float64
     5   forecast_6_month   1687860 non-null  float64
     6   forecast_9_month   1687860 non-null  float64
     7   sales_1_month      1687860 non-null  float64
     8   sales_3_month      1687860 non-null  float64
     9   sales_6_month      1687860 non-null  float64
     10  sales_9_month      1687860 non-null  float64
     11  min_bank           1687860 non-null  float64
     12  potential_issue    1687860 non-null  object 
     13  pieces_past_due    1687860 non-null  float64
     14  perf_6_month_avg   1687860 non-null  float64
     15  perf_12_month_avg  1687860 non-null  float64
     16  local_bo_qty       1687860 non-null  float64
     17  deck_risk          1687860 non-null  object 
     18  oe_constraint      1687860 non-null  object 
     19  ppap_risk          1687860 non-null  object 
     20  stop_auto_buy      1687860 non-null  object 
     21  rev_stop           1687860 non-null  object 
     22  went_on_backorder  1687860 non-null  object 
    dtypes: float64(15), object(8)
    memory usage: 296.2+ MB


# Transformações nas variáveis

## Retirando a variável sku


```python
banco = banco.drop("sku", axis = 1)

banco.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>national_inv</th>
      <th>lead_time</th>
      <th>in_transit_qty</th>
      <th>forecast_3_month</th>
      <th>forecast_6_month</th>
      <th>forecast_9_month</th>
      <th>sales_1_month</th>
      <th>sales_3_month</th>
      <th>sales_6_month</th>
      <th>sales_9_month</th>
      <th>min_bank</th>
      <th>potential_issue</th>
      <th>pieces_past_due</th>
      <th>perf_6_month_avg</th>
      <th>perf_12_month_avg</th>
      <th>local_bo_qty</th>
      <th>deck_risk</th>
      <th>oe_constraint</th>
      <th>ppap_risk</th>
      <th>stop_auto_buy</th>
      <th>rev_stop</th>
      <th>went_on_backorder</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>No</td>
      <td>0.0</td>
      <td>-99.00</td>
      <td>-99.00</td>
      <td>0.0</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>9.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>No</td>
      <td>0.0</td>
      <td>0.99</td>
      <td>0.99</td>
      <td>0.0</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>No</td>
      <td>0.0</td>
      <td>-99.00</td>
      <td>-99.00</td>
      <td>0.0</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7.0</td>
      <td>8.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>No</td>
      <td>0.0</td>
      <td>0.10</td>
      <td>0.13</td>
      <td>0.0</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>No</td>
      <td>0.0</td>
      <td>-99.00</td>
      <td>-99.00</td>
      <td>0.0</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
    </tr>
  </tbody>
</table>
</div>



## Lidando com os valores NaN

- Nenhum ganho absurdo de diferença inputando a média, mediana ou moda (a mesma nos dá score parecidos);
- O melhor ganho, foi dropando os NAs e utilizando a estratégia de colocar o 999 no lugar deles.
    - A variável lead_time teve uma maior importância (0.03466);
    - O **recall** (nos dá informações sobre falsos negativos, de todos os exemplos que realmente são verdadeiros, o quanto meu modelo meu modelo previu corretamente), métrica que queremos maximizar, teve o valor de 0.51


```python
banco.isnull().sum()
```




    national_inv              1
    lead_time            100894
    in_transit_qty            1
    forecast_3_month          1
    forecast_6_month          1
    forecast_9_month          1
    sales_1_month             1
    sales_3_month             1
    sales_6_month             1
    sales_9_month             1
    min_bank                  1
    potential_issue           1
    pieces_past_due           1
    perf_6_month_avg          1
    perf_12_month_avg         1
    local_bo_qty              1
    deck_risk                 1
    oe_constraint             1
    ppap_risk                 1
    stop_auto_buy             1
    rev_stop                  1
    went_on_backorder         1
    dtype: int64




```python
#--- Para comentar as linhas: Ctrl + "/" (teclado numérico)

#--- Dropando todas


# banco = banco.dropna()

#--------------------------------------------------------------------

#--- Excluindo a última linha e imputando média na variável lead_time

# banco = banco[: -1] 

# banco["lead_time"] = banco["lead_time"].fillna(banco["lead_time"].mean())

#--------------------------------------------------------------------

#--- Excluindo a última linha e imputando média na variável lead_time

# banco = banco[: -1] 

# banco["lead_time"] = banco["lead_time"].fillna(banco["lead_time"].median())

#--------------------------------------------------------------------

#--- Excluindo a última linha e imputando a moda na variável lead_time

# banco = banco[: -1] 

# banco["lead_time"] = banco["lead_time"].fillna(banco["lead_time"].mode()[0])

#--------------------------------------------------------------------

#--- Excluindo a última linha e imputando o 0 na variável lead_time

banco = banco[: -1] 

banco["lead_time"] = banco["lead_time"].fillna(999)

banco.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>national_inv</th>
      <th>lead_time</th>
      <th>in_transit_qty</th>
      <th>forecast_3_month</th>
      <th>forecast_6_month</th>
      <th>forecast_9_month</th>
      <th>sales_1_month</th>
      <th>sales_3_month</th>
      <th>sales_6_month</th>
      <th>sales_9_month</th>
      <th>min_bank</th>
      <th>potential_issue</th>
      <th>pieces_past_due</th>
      <th>perf_6_month_avg</th>
      <th>perf_12_month_avg</th>
      <th>local_bo_qty</th>
      <th>deck_risk</th>
      <th>oe_constraint</th>
      <th>ppap_risk</th>
      <th>stop_auto_buy</th>
      <th>rev_stop</th>
      <th>went_on_backorder</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1687855</th>
      <td>0.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>10.0</td>
      <td>10.0</td>
      <td>10.0</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>7.0</td>
      <td>7.0</td>
      <td>0.0</td>
      <td>No</td>
      <td>0.0</td>
      <td>0.69</td>
      <td>0.69</td>
      <td>5.0</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1687856</th>
      <td>-1.0</td>
      <td>999.0</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>7.0</td>
      <td>9.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>8.0</td>
      <td>0.0</td>
      <td>No</td>
      <td>0.0</td>
      <td>-99.00</td>
      <td>-99.00</td>
      <td>1.0</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1687857</th>
      <td>-1.0</td>
      <td>9.0</td>
      <td>0.0</td>
      <td>7.0</td>
      <td>9.0</td>
      <td>11.0</td>
      <td>0.0</td>
      <td>8.0</td>
      <td>11.0</td>
      <td>12.0</td>
      <td>0.0</td>
      <td>No</td>
      <td>0.0</td>
      <td>0.86</td>
      <td>0.84</td>
      <td>1.0</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>1687858</th>
      <td>62.0</td>
      <td>9.0</td>
      <td>16.0</td>
      <td>39.0</td>
      <td>87.0</td>
      <td>126.0</td>
      <td>35.0</td>
      <td>63.0</td>
      <td>153.0</td>
      <td>205.0</td>
      <td>12.0</td>
      <td>No</td>
      <td>0.0</td>
      <td>0.86</td>
      <td>0.84</td>
      <td>6.0</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1687859</th>
      <td>19.0</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>7.0</td>
      <td>12.0</td>
      <td>20.0</td>
      <td>1.0</td>
      <td>No</td>
      <td>0.0</td>
      <td>0.73</td>
      <td>0.78</td>
      <td>1.0</td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td>Yes</td>
      <td>No</td>
      <td>No</td>
    </tr>
  </tbody>
</table>
</div>



## Recodificando variáveis qualitativas para quantitativas


```python
columns_yesno = ["potential_issue", "deck_risk", "oe_constraint", "ppap_risk", "stop_auto_buy", "rev_stop", "went_on_backorder"]

banco[columns_yesno] = banco[columns_yesno].replace({"No" : 0, "Yes": 1})

banco.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>national_inv</th>
      <th>lead_time</th>
      <th>in_transit_qty</th>
      <th>forecast_3_month</th>
      <th>forecast_6_month</th>
      <th>forecast_9_month</th>
      <th>sales_1_month</th>
      <th>sales_3_month</th>
      <th>sales_6_month</th>
      <th>sales_9_month</th>
      <th>min_bank</th>
      <th>potential_issue</th>
      <th>pieces_past_due</th>
      <th>perf_6_month_avg</th>
      <th>perf_12_month_avg</th>
      <th>local_bo_qty</th>
      <th>deck_risk</th>
      <th>oe_constraint</th>
      <th>ppap_risk</th>
      <th>stop_auto_buy</th>
      <th>rev_stop</th>
      <th>went_on_backorder</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>999.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>-99.00</td>
      <td>-99.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>9.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.99</td>
      <td>0.99</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.0</td>
      <td>999.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>-99.00</td>
      <td>-99.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7.0</td>
      <td>8.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.10</td>
      <td>0.13</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8.0</td>
      <td>999.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>-99.00</td>
      <td>-99.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

## Criando novas features


```python
#--- national_inv quadrado (Boa variável)

banco["national_inv_poly2"] = banco["national_inv"] ** 2


#--- 0 se national_inv < 0, 1 se >= 0 (Variável ruim)

banco["national_inv_qual"] = banco["national_inv"].map(lambda x: 0 if x <= 0 else 1)

# 0: Se x <= 0
# 1: Se x > 0


#--- Feature verificando se a lead_time (O tempo de trânsito do produto) é nulo ou não:

banco["lead_time_isnull"] = banco["lead_time"].map(lambda x: 1 if x == 999 else 0)


# Resultado: é uma boa variável para aumentar o Recall em 0.02 (0.54), apesar de aumentar um pouco os falsos positivos


#--- Tentativa de retirar variáveis que não foram importantes para o primeiro modelo:

# banco = banco.drop(["potential_issue", "rev_stop", "oe_constraint"], axis = 1)

# Resultado: O modelo diminui em 0.01 o Recall, coisa que não queremos


#--- Criando uma média para cada variável de meses

# banco["forecast_month_avg"] = banco[["forecast_3_month", "forecast_6_month", "forecast_9_month"]].mean(axis = 1)

# banco["sales_month_avg"] = banco[["sales_1_month", "sales_3_month", "sales_6_month", "sales_9_month"]].mean(axis = 1)

# banco["perf_month_avg"] = banco[["perf_6_month_avg", "perf_12_month_avg"]].mean(axis = 1)


# Resultado: São boas variáveis para diminuir os falsos positivos, entretanto aumenta os falsos negativos


#--- Verificamos através da correlação que quanto maior o nível de estoque atual da peça, maior a quantidade mínima do produto 
# recomendada para ficar em estoque, podemos criar uma razão entre elas:


banco["relat_minbank_nationalinv"] = banco["min_bank"]/banco["national_inv"]

banco["relat_minbank_nationalinv"] = banco["relat_minbank_nationalinv"].map(lambda x: 0 if x < 0 else 1)

# 0: Indica que a relação foi negativa
# 1: Indica que a relação foi positiva


# Resultado: Aumenta o recall em 0.01 mas também aumenta os falsos positivos (não tanto quanto a variável lead_time_isnull)
# Portanto, essa é a melhor feature para ganhar recall.


#--- Quanto maior a quantidade mínima do produto recomendada também são maiores os desempenhos do produto/loja nos períodos de meses 
# indicados.

# 0: Indica que a relação foi negativa
# 1: Indica que a relação foi positiva


# banco["new"] = banco["min_bank"]/banco["perf_6_month_avg"]

# banco["new"] = banco["new"].map(lambda x: 0 if x < 0 else 1)

# Resultados: não foi importante para o modelo


#--- Relacionar alguma variável com as features de desempenho por mês


#--- Criando uma feature baseada nos quartis das variáveis que possuem alta variação:

colunas = ["national_inv", "in_transit_qty", "min_bank", "national_inv_poly2"]
novas_colunas = [i + "_new" for i in colunas]

banco[novas_colunas] = banco[colunas].apply(lambda x: pd.qcut(x, 4, duplicates = "drop"), axis = 0)

# Resultado: Aumentaram o recall e a F1 em 0.1


#--- Criando um loop para verificar se cada valor para uma lista variáveis é maior que o percentil 95

# 1- Pegar o quartil 90 da coluna
# 2- Verificar se aquele valor é maior que o quartil 85

# for column in colunas:

#   novas_colunas1 = column + '_isabove85'

#   # print(novas_colunas1)

#   quart85 = banco[column].quantile(q = 0.85)

#   banco[novas_colunas1] = banco[column].map(lambda x: 1 if x >= quart85 else 0)

#   print(banco[novas_colunas1].value_counts())
#   print()


#--- Resultados: Mais ou menos útil, não melhorou em nada, somente os falsos positivos em um número bem pequeno, então vamos 
# ao princípio da parcimônia


# def isabovequant(df, quantile):

#   df1 = pd.DataFrame()

#   for column in df:

#     novas_colunas1 = column + "_isabove85"

#     selec_quantile = banco[column].quantile(q = quantile)

#     df1[novas_colunas1] = banco[column].map(lambda x: 1 if x >= selec_quantile else 0)

#   return(df1)


# isabovequant(df = banco[colunas], quantile = 0.85) 


ideia1 = ["national_inv", "in_transit_qty", "min_bank", "forecast_3_month", "forecast_6_month", "forecast_9_month",
          "sales_1_month", "sales_3_month", "sales_6_month", "sales_9_month"]


def isabovequant(df, quantile):

  for column in df:

    novas_colunas1 = column + '_isabove_quantile'

    selec_quantile = banco[column].quantile(q = quantile)

    banco[novas_colunas1] = banco[column].map(lambda x: 1 if x >= selec_quantile else 0)

    # print(banco[novas_colunas1].value_counts())
    # print()


isabovequant(df = banco[ideia1], quantile = 0.85) 


#--- Quadrado das ideias1

# novas_ideias1 = [i + "_2poly" for i in ideia1]

# banco[novas_ideias1] = banco[ideia1] ** 2

# Resultado: Não foram boas, somente as primeira


#--- Relacionar as variáveis de meses com as demais variávies

# 1. nível de estoque atual da peça x previsão de vendas para os próximos X meses


#--- Verificando se o valor é 0 para as variáveis forecast_3_month

def isequal0var(x):
  if x == 0:
    return(1)
  else:
    return(0)


banco["forecast_3_month_isequal0"] = banco["forecast_3_month"].apply(lambda x: isequal0var(x))

banco["sales_1_month_isequal0"] = banco["sales_1_month"].apply(lambda x: isequal0var(x))

banco["perf_6_month_avg_isbelow0"] = banco["perf_6_month_avg"].apply(lambda x: 1 if x <= 0 else 0)


# Resultado: boas variável
# Nota: Melhorar o script utilizando o applymap nos dados e não precisaria criar a função isequal0var. Exemplo:

# var1 = ["forecast_3_month", "sales_1_month", "perf_6_month_avg"]
# banco[var1].applymap(lambda x: isequal0var(x))

banco0 = banco[banco["went_on_backorder"] == 0]
banco1 = banco[banco["went_on_backorder"] == 1]


#--- national_inv_qual * forecast_3_month

# banco["relat_nationalinvqual_forecast3"] = banco["national_inv_qual"] * banco["forecast_3_month"]

#--- (1-NivelEstoque)*Previsão Vendas

banco["1relat_nationalinvqual_forecast3"] = (1 - banco["national_inv_qual"]) * banco["forecast_3_month"]

#--- 

banco.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>national_inv</th>
      <th>lead_time</th>
      <th>in_transit_qty</th>
      <th>forecast_3_month</th>
      <th>forecast_6_month</th>
      <th>forecast_9_month</th>
      <th>sales_1_month</th>
      <th>sales_3_month</th>
      <th>sales_6_month</th>
      <th>sales_9_month</th>
      <th>min_bank</th>
      <th>potential_issue</th>
      <th>pieces_past_due</th>
      <th>perf_6_month_avg</th>
      <th>perf_12_month_avg</th>
      <th>local_bo_qty</th>
      <th>deck_risk</th>
      <th>oe_constraint</th>
      <th>ppap_risk</th>
      <th>stop_auto_buy</th>
      <th>rev_stop</th>
      <th>went_on_backorder</th>
      <th>national_inv_poly2</th>
      <th>national_inv_qual</th>
      <th>lead_time_isnull</th>
      <th>relat_minbank_nationalinv</th>
      <th>national_inv_new</th>
      <th>in_transit_qty_new</th>
      <th>min_bank_new</th>
      <th>national_inv_poly2_new</th>
      <th>national_inv_isabove_quantile</th>
      <th>in_transit_qty_isabove_quantile</th>
      <th>min_bank_isabove_quantile</th>
      <th>forecast_3_month_isabove_quantile</th>
      <th>forecast_6_month_isabove_quantile</th>
      <th>forecast_9_month_isabove_quantile</th>
      <th>sales_1_month_isabove_quantile</th>
      <th>sales_3_month_isabove_quantile</th>
      <th>sales_6_month_isabove_quantile</th>
      <th>sales_9_month_isabove_quantile</th>
      <th>forecast_3_month_isequal0</th>
      <th>sales_1_month_isequal0</th>
      <th>perf_6_month_avg_isbelow0</th>
      <th>1relat_nationalinvqual_forecast3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>999.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>-99.00</td>
      <td>-99.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>(-27256.001, 4.0]</td>
      <td>(-0.001, 489408.0]</td>
      <td>(-0.001, 3.0]</td>
      <td>(-0.001, 16.0]</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>9.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.99</td>
      <td>0.99</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>4.0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>(-27256.001, 4.0]</td>
      <td>(-0.001, 489408.0]</td>
      <td>(-0.001, 3.0]</td>
      <td>(-0.001, 16.0]</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.0</td>
      <td>999.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>-99.00</td>
      <td>-99.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>4.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>(-27256.001, 4.0]</td>
      <td>(-0.001, 489408.0]</td>
      <td>(-0.001, 3.0]</td>
      <td>(-0.001, 16.0]</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7.0</td>
      <td>8.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.10</td>
      <td>0.13</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>49.0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>(4.0, 15.0]</td>
      <td>(-0.001, 489408.0]</td>
      <td>(-0.001, 3.0]</td>
      <td>(16.0, 225.0]</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8.0</td>
      <td>999.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>-99.00</td>
      <td>-99.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>64.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>(4.0, 15.0]</td>
      <td>(-0.001, 489408.0]</td>
      <td>(-0.001, 3.0]</td>
      <td>(16.0, 225.0]</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# # 1. nível de estoque atual da peça x previsão de vendas para os próximos X meses

# # 0: Se x <= 0
# # 1: Se x > 0

# banco_quant1 = banco1.select_dtypes(exclude = [object]).drop(['potential_issue', 'pieces_past_due', 'deck_risk', 'oe_constraint',
# 'ppap_risk', 'stop_auto_buy', 'rev_stop', 'went_on_backorder', 'national_inv_qual', 'lead_time_isnull', 'relat_minbank_nationalinv', 'national_inv_new', 'in_transit_qty_new',
# 'min_bank_new', 'national_inv_isabove_quantile', 'in_transit_qty_isabove_quantile', 'min_bank_isabove_quantile', 'forecast_3_month_isabove_quantile',
# 'forecast_6_month_isabove_quantile', 'forecast_9_month_isabove_quantile', 'sales_1_month_isabove_quantile', 'sales_3_month_isabove_quantile', 'sales_6_month_isabove_quantile',
# 'sales_9_month_isabove_quantile', 'forecast_3_month_isequal0', 'sales_1_month_isequal0', 'perf_6_month_avg_isbelow0'], axis = 1)


# f, axes = plt.subplots(5, 3, figsize = (20, 20), sharex = False)

# for ax, feature in zip(axes.flat, banco_quant1.columns):
#     sns.distplot(banco_quant1[feature] , color = "orangered", hist = False, ax = ax)
```


```python
# banco_quant2 = banco0.select_dtypes(exclude = [object]).drop(['potential_issue', 'pieces_past_due', 'deck_risk', 'oe_constraint',
# 'ppap_risk', 'stop_auto_buy', 'rev_stop', 'went_on_backorder', 'national_inv_qual', 'lead_time_isnull', 'relat_minbank_nationalinv', 'national_inv_new', 'in_transit_qty_new',
#        'min_bank_new', 'national_inv_isabove_quantile',
#        'in_transit_qty_isabove_quantile', 'min_bank_isabove_quantile',
#        'forecast_3_month_isabove_quantile',
#        'forecast_6_month_isabove_quantile',
#        'forecast_9_month_isabove_quantile', 'sales_1_month_isabove_quantile',
#        'sales_3_month_isabove_quantile', 'sales_6_month_isabove_quantile',
#        'sales_9_month_isabove_quantile', 'forecast_3_month_isequal0',
#        'sales_1_month_isequal0', 'perf_6_month_avg_isbelow0'], axis = 1)


# # len(banco_quant1.columns)

# f, axes = plt.subplots(5, 3, figsize = (20, 20), sharex = False)

# for ax, feature in zip(axes.flat, banco_quant2.columns):
#     sns.distplot(banco_quant2[feature] , color = "orangered", hist = False, ax = ax)
```


```python
# x = banco0["national_inv_poly2"]

# y = banco1["national_inv_poly2"]

# df = pd.concat([x, y], axis = 1)

# df.columns = ["N_houve_atraso", 'Houve_atraso']

# df = pd.melt(df, var_name='Category')

# g = sns.FacetGrid(df, col='Category', col_wrap=2, sharex=False, sharey=False, aspect=1.5)
# g = g.map(sns.distplot, "value", color="r", hist = 0)
# g.axes[0].set_xscale('log')
# g.axes[1].set_xscale('log')
```

## OneHotEncoding nas variáveis categóricas


```python
banco = pd.get_dummies(data = banco, columns = novas_colunas,  drop_first = True)

banco.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>national_inv</th>
      <th>lead_time</th>
      <th>in_transit_qty</th>
      <th>forecast_3_month</th>
      <th>forecast_6_month</th>
      <th>forecast_9_month</th>
      <th>sales_1_month</th>
      <th>sales_3_month</th>
      <th>sales_6_month</th>
      <th>sales_9_month</th>
      <th>min_bank</th>
      <th>potential_issue</th>
      <th>pieces_past_due</th>
      <th>perf_6_month_avg</th>
      <th>perf_12_month_avg</th>
      <th>local_bo_qty</th>
      <th>deck_risk</th>
      <th>oe_constraint</th>
      <th>ppap_risk</th>
      <th>stop_auto_buy</th>
      <th>rev_stop</th>
      <th>went_on_backorder</th>
      <th>national_inv_poly2</th>
      <th>national_inv_qual</th>
      <th>lead_time_isnull</th>
      <th>relat_minbank_nationalinv</th>
      <th>national_inv_isabove_quantile</th>
      <th>in_transit_qty_isabove_quantile</th>
      <th>min_bank_isabove_quantile</th>
      <th>forecast_3_month_isabove_quantile</th>
      <th>forecast_6_month_isabove_quantile</th>
      <th>forecast_9_month_isabove_quantile</th>
      <th>sales_1_month_isabove_quantile</th>
      <th>sales_3_month_isabove_quantile</th>
      <th>sales_6_month_isabove_quantile</th>
      <th>sales_9_month_isabove_quantile</th>
      <th>forecast_3_month_isequal0</th>
      <th>sales_1_month_isequal0</th>
      <th>perf_6_month_avg_isbelow0</th>
      <th>1relat_nationalinvqual_forecast3</th>
      <th>national_inv_new_(4.0, 15.0]</th>
      <th>national_inv_new_(15.0, 80.0]</th>
      <th>national_inv_new_(80.0, 12334404.0]</th>
      <th>min_bank_new_(3.0, 313319.0]</th>
      <th>national_inv_poly2_new_(16.0, 225.0]</th>
      <th>national_inv_poly2_new_(225.0, 6400.0]</th>
      <th>national_inv_poly2_new_(6400.0, 152137522035216.0]</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>999.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>-99.00</td>
      <td>-99.00</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>9.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.99</td>
      <td>0.99</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>4.0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.0</td>
      <td>999.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>-99.00</td>
      <td>-99.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>4.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7.0</td>
      <td>8.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.10</td>
      <td>0.13</td>
      <td>0.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>49.0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8.0</td>
      <td>999.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>0</td>
      <td>0.0</td>
      <td>-99.00</td>
      <td>-99.00</td>
      <td>0.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>64.0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



## Separando em treino e teste


```python
from sklearn.model_selection import train_test_split


x_treino, x_teste, y_treino, y_teste = train_test_split(banco.drop("went_on_backorder", axis = 1), banco["went_on_backorder"], train_size = 0.7, random_state = 1234, stratify = banco["went_on_backorder"])
```


```python
print(x_treino.shape, y_treino.shape, x_teste.shape, y_teste.shape)
```

    (1181502, 46) (1181502,) (506358, 46) (506358,)



```python
print(15*"---")

print("Proporção da variável target nos dados de treino:\n", y_treino.value_counts(normalize = True))

print(15*"---")

print("Proporção da variável target nos dados de treino:\n", y_teste.value_counts(normalize = True))
```

    ---------------------------------------------
    Proporção da variável target nos dados de treino:
     0    0.993309
    1    0.006691
    Name: went_on_backorder, dtype: float64
    ---------------------------------------------
    Proporção da variável target nos dados de treino:
     0    0.993309
    1    0.006691
    Name: went_on_backorder, dtype: float64


# Random forest


```python
from sklearn.utils import class_weight

class_weights1 = class_weight.compute_class_weight('balanced',
                                                 np.unique(y_treino),
                                                 y_treino)

class_weights1
```




    array([ 0.50336785, 74.7313093 ])



## Cross-Validation


```python
from sklearn.ensemble import RandomForestClassifier


rfc = RandomForestClassifier(n_estimators = 100, 
                             class_weight = {0: 0.5034, 1: 74.7370}, 
                             random_state = 1234, 
                             min_samples_leaf = 5, 
                             min_samples_split = 5,
                             max_depth = None,
                             n_jobs = -1)
```


```python
%%time

from sklearn.model_selection import cross_validate 

scoring1 = [
    "accuracy", 
    "f1", 
    'f1_macro',
    'recall',
    'recall_macro',
    'precision',
    'precision_macro',          
    'roc_auc']

scores = cross_validate(rfc, x_treino, y_treino, cv = 5, scoring = scoring1, n_jobs = -1)
```

    /usr/local/lib/python3.6/dist-packages/joblib/externals/loky/process_executor.py:691: UserWarning: A worker stopped while some jobs were given to the executor. This can be caused by a too short worker timeout or by a memory leak.
      "timeout or by a memory leak.", UserWarning


    CPU times: user 410 ms, sys: 642 ms, total: 1.05 s
    Wall time: 11min 29s



```python
scores


# import sklearn

# sorted(sklearn.metrics.SCORERS.keys())
```




    {'fit_time': array([307.60833406, 285.16906571, 246.58286929, 238.33629751,
            118.50701761]),
     'score_time': array([14.79028034, 14.62633419, 14.24836302, 13.83162761,  6.84228396]),
     'test_accuracy': array([0.98522647, 0.98495563, 0.98482438, 0.98500635, 0.98527719]),
     'test_f1': array([0.34119645, 0.33687745, 0.3302204 , 0.33364679, 0.35442568]),
     'test_f1_macro': array([0.66686296, 0.66463448, 0.66127282, 0.66303233, 0.67348968]),
     'test_precision': array([0.24314147, 0.23888889, 0.23429632, 0.2374197 , 0.25078782]),
     'test_precision_macro': array([0.62011534, 0.61798651, 0.61564941, 0.61721779, 0.62404762]),
     'test_recall': array([0.57179001, 0.5711575 , 0.55913978, 0.56103732, 0.60404807]),
     'test_recall_macro': array([0.77990063, 0.77945017, 0.77341573, 0.7744497 , 0.79594656]),
     'test_roc_auc': array([0.9680942 , 0.96150484, 0.96191622, 0.96053337, 0.96472544])}



## Aplicando a RF nos dados de teste


```python
%%time

rfc.fit(x_treino, y_treino)

y_pred = rfc.predict(x_teste)
```

    CPU times: user 6min 51s, sys: 521 ms, total: 6min 52s
    Wall time: 3min 29s


# Métricas a serem avaliadas



```python
from sklearn.metrics import accuracy_score

acc = accuracy_score(y_teste, y_pred)

print("Accuracy:", acc)
```

    Accuracy: 0.9852416669628997



```python
from sklearn.metrics import confusion_matrix

print(confusion_matrix(y_teste, y_pred))
```

    [[496849   6121]
     [  1352   2036]]



```python
pd.crosstab(y_teste, y_pred, rownames = ["True"], colnames = ["Predicted"], margins = True)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Predicted</th>
      <th>0</th>
      <th>1</th>
      <th>All</th>
    </tr>
    <tr>
      <th>True</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>496849</td>
      <td>6121</td>
      <td>502970</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1352</td>
      <td>2036</td>
      <td>3388</td>
    </tr>
    <tr>
      <th>All</th>
      <td>498201</td>
      <td>8157</td>
      <td>506358</td>
    </tr>
  </tbody>
</table>
</div>




```python
from sklearn.metrics import classification_report

print(classification_report(y_teste, y_pred))
```

                  precision    recall  f1-score   support
    
               0       1.00      0.99      0.99    502970
               1       0.25      0.60      0.35      3388
    
        accuracy                           0.99    506358
       macro avg       0.62      0.79      0.67    506358
    weighted avg       0.99      0.99      0.99    506358
    



```python
from sklearn.metrics import cohen_kappa_score

cohen_kappa_score(y_teste, y_pred)
```




    0.3465283572144585




```python
from sklearn.metrics import fbeta_score

fbeta_score(y_teste, y_pred, beta = 2)
```




    0.4689299368925331




```python
#--- Adaptado de: https://stackoverflow.com/questions/25009284/how-to-plot-roc-curve-in-python

import sklearn.metrics as metrics

probs = rfc.predict_proba(x_teste)
preds = probs[:,1]
fpr, vpr, threshold = metrics.roc_curve(y_teste, preds)
roc_auc = metrics.auc(fpr, vpr)

#--- Curva

plt.figure(figsize = [10, 6])
plt.title("Curva ROC")
plt.plot(fpr, vpr, "blue", label = "AUC = %0.2f" % roc_auc)
plt.legend(loc = "lower right")
plt.plot([0, 1], [0, 1], "r--")
plt.ylabel("Taxa de Verdadeiros Positivos", fontsize = 14, color = "black")
plt.xlabel("Taxa de Falsos Positivos", fontsize = 14, color = "black")
plt.tick_params(axis = "x", labelsize = 12, labelcolor = "black")
plt.tick_params(axis = "y", labelsize = 12, labelcolor = "black")
plt.show()
```


![png](2classweight_randomforest_files/2classweight_randomforest_42_0.png)


# Importância das variáveis para o modelo de Random Forest


```python
pd.DataFrame(rfc.feature_importances_, x_teste.columns).reset_index().rename(columns = {0: "Valor", "index": "Variável"}).sort_values("Valor", ascending = False).round(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Variável</th>
      <th>Valor</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>national_inv</td>
      <td>0.10581</td>
    </tr>
    <tr>
      <th>3</th>
      <td>forecast_3_month</td>
      <td>0.10388</td>
    </tr>
    <tr>
      <th>5</th>
      <td>forecast_9_month</td>
      <td>0.08497</td>
    </tr>
    <tr>
      <th>4</th>
      <td>forecast_6_month</td>
      <td>0.08361</td>
    </tr>
    <tr>
      <th>21</th>
      <td>national_inv_poly2</td>
      <td>0.08065</td>
    </tr>
    <tr>
      <th>35</th>
      <td>forecast_3_month_isequal0</td>
      <td>0.04819</td>
    </tr>
    <tr>
      <th>9</th>
      <td>sales_9_month</td>
      <td>0.04272</td>
    </tr>
    <tr>
      <th>7</th>
      <td>sales_3_month</td>
      <td>0.04153</td>
    </tr>
    <tr>
      <th>8</th>
      <td>sales_6_month</td>
      <td>0.04048</td>
    </tr>
    <tr>
      <th>14</th>
      <td>perf_12_month_avg</td>
      <td>0.03905</td>
    </tr>
    <tr>
      <th>13</th>
      <td>perf_6_month_avg</td>
      <td>0.03770</td>
    </tr>
    <tr>
      <th>6</th>
      <td>sales_1_month</td>
      <td>0.03660</td>
    </tr>
    <tr>
      <th>38</th>
      <td>1relat_nationalinvqual_forecast3</td>
      <td>0.02940</td>
    </tr>
    <tr>
      <th>1</th>
      <td>lead_time</td>
      <td>0.02689</td>
    </tr>
    <tr>
      <th>10</th>
      <td>min_bank</td>
      <td>0.02107</td>
    </tr>
    <tr>
      <th>2</th>
      <td>in_transit_qty</td>
      <td>0.02048</td>
    </tr>
    <tr>
      <th>45</th>
      <td>national_inv_poly2_new_(6400.0, 15213752203521...</td>
      <td>0.01923</td>
    </tr>
    <tr>
      <th>22</th>
      <td>national_inv_qual</td>
      <td>0.01777</td>
    </tr>
    <tr>
      <th>41</th>
      <td>national_inv_new_(80.0, 12334404.0]</td>
      <td>0.01703</td>
    </tr>
    <tr>
      <th>36</th>
      <td>sales_1_month_isequal0</td>
      <td>0.01469</td>
    </tr>
    <tr>
      <th>40</th>
      <td>national_inv_new_(15.0, 80.0]</td>
      <td>0.00953</td>
    </tr>
    <tr>
      <th>26</th>
      <td>in_transit_qty_isabove_quantile</td>
      <td>0.00768</td>
    </tr>
    <tr>
      <th>44</th>
      <td>national_inv_poly2_new_(225.0, 6400.0]</td>
      <td>0.00748</td>
    </tr>
    <tr>
      <th>25</th>
      <td>national_inv_isabove_quantile</td>
      <td>0.00736</td>
    </tr>
    <tr>
      <th>16</th>
      <td>deck_risk</td>
      <td>0.00650</td>
    </tr>
    <tr>
      <th>15</th>
      <td>local_bo_qty</td>
      <td>0.00567</td>
    </tr>
    <tr>
      <th>43</th>
      <td>national_inv_poly2_new_(16.0, 225.0]</td>
      <td>0.00560</td>
    </tr>
    <tr>
      <th>18</th>
      <td>ppap_risk</td>
      <td>0.00515</td>
    </tr>
    <tr>
      <th>39</th>
      <td>national_inv_new_(4.0, 15.0]</td>
      <td>0.00457</td>
    </tr>
    <tr>
      <th>12</th>
      <td>pieces_past_due</td>
      <td>0.00421</td>
    </tr>
    <tr>
      <th>28</th>
      <td>forecast_3_month_isabove_quantile</td>
      <td>0.00309</td>
    </tr>
    <tr>
      <th>42</th>
      <td>min_bank_new_(3.0, 313319.0]</td>
      <td>0.00274</td>
    </tr>
    <tr>
      <th>31</th>
      <td>sales_1_month_isabove_quantile</td>
      <td>0.00268</td>
    </tr>
    <tr>
      <th>19</th>
      <td>stop_auto_buy</td>
      <td>0.00216</td>
    </tr>
    <tr>
      <th>30</th>
      <td>forecast_9_month_isabove_quantile</td>
      <td>0.00211</td>
    </tr>
    <tr>
      <th>24</th>
      <td>relat_minbank_nationalinv</td>
      <td>0.00211</td>
    </tr>
    <tr>
      <th>29</th>
      <td>forecast_6_month_isabove_quantile</td>
      <td>0.00170</td>
    </tr>
    <tr>
      <th>37</th>
      <td>perf_6_month_avg_isbelow0</td>
      <td>0.00167</td>
    </tr>
    <tr>
      <th>27</th>
      <td>min_bank_isabove_quantile</td>
      <td>0.00160</td>
    </tr>
    <tr>
      <th>34</th>
      <td>sales_9_month_isabove_quantile</td>
      <td>0.00143</td>
    </tr>
    <tr>
      <th>32</th>
      <td>sales_3_month_isabove_quantile</td>
      <td>0.00141</td>
    </tr>
    <tr>
      <th>23</th>
      <td>lead_time_isnull</td>
      <td>0.00096</td>
    </tr>
    <tr>
      <th>33</th>
      <td>sales_6_month_isabove_quantile</td>
      <td>0.00075</td>
    </tr>
    <tr>
      <th>11</th>
      <td>potential_issue</td>
      <td>0.00005</td>
    </tr>
    <tr>
      <th>20</th>
      <td>rev_stop</td>
      <td>0.00004</td>
    </tr>
    <tr>
      <th>17</th>
      <td>oe_constraint</td>
      <td>0.00000</td>
    </tr>
  </tbody>
</table>
</div>



# Próximos passos:

1. Criar novas features;
    - Relacionar a forecast_3_month com alguma variável;
2. Verificar a relação das variáveis (esqueci hoje);
3. Observar as variáveis national_inv e lead_time;
4. Testar o método de oversampling e undersampling.


Falso positivo: o modelo previu que era um pedido em atraso, quando não era 
um pedido em atraso

Falso negativo (*): o modelo disse que não era um pedido em atraso, quando na verdade ele era

- Focar na métrica Recall
