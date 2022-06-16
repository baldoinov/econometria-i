---
"lang": "pt-br",
"title": "Exercício Empírico I",
"subtitle": "Econometria I - EAE0324",
"authors": ["Vitor Baldoino - 11766857"],
"date": "Maio 2022"
---

***

## Descrição dos Dados

Os dados para este exercício são uma *cross-section* de alunos do curso de Economia da Universidade de São Paulo. Na nossa base de dados, nós temos acesso as seguintes variáveis:


<center>

     #   Column            Non-Null Count  Dtype  
    ---  ------            --------------  -----  
     0   genero            45 non-null     object 
     1   idade             45 non-null     int64  
     2   nota1             45 non-null     float64
     3   nota2             45 non-null     float64
     4   fuvest            44 non-null     float64
     5   gosta_curso       45 non-null     object 
     6   frequencia        45 non-null     object 
     7   gosta_estudo      45 non-null     object 
     8   ensino_medio      45 non-null     object 
     9   trabalho          45 non-null     object 
     10  nasceu_sp         45 non-null     object 
     11  pretende_estudar  45 non-null     object 

</center>

Como indicado na tabela acima, nós possuímos uma observação faltante na variável que apresenta a nota da Fuvest. Essa ausência será tratada posteriormente no código que gera os modelos de regressão. Adicionalmente, como não iremos usar variáveis categóricas neste primeiro momento, eu optei por manter na base apenas as variáveis relevantes para o exercício.


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
      <th>genero</th>
      <th>idade</th>
      <th>nota1</th>
      <th>nota2</th>
      <th>fuvest</th>
      <th>gosta_curso</th>
      <th>frequencia</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M</td>
      <td>23</td>
      <td>8.5</td>
      <td>8.5</td>
      <td>67.0</td>
      <td>S</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M</td>
      <td>21</td>
      <td>10.0</td>
      <td>10.0</td>
      <td>71.0</td>
      <td>S</td>
      <td>S</td>
    </tr>
    <tr>
      <th>2</th>
      <td>F</td>
      <td>21</td>
      <td>8.6</td>
      <td>8.3</td>
      <td>66.0</td>
      <td>S</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M</td>
      <td>23</td>
      <td>9.0</td>
      <td>6.8</td>
      <td>62.0</td>
      <td>S</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M</td>
      <td>22</td>
      <td>9.5</td>
      <td>8.6</td>
      <td>68.0</td>
      <td>S</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>



Abaixo, temos uma breve descrição das variáveis contínuas presentes na base. Como é possível ver, a nota em MAE0229 dos alunos é bem distribuída, assemelhando-se a uma normal. Entretanto, a variável de idade possui uma assimetria à direita, algo esperado dado as características dos indivíduos da amostra (estudantes universitários). E as notas de MAE0219 e as notas da Fuvest possuem uma assimetria à esquerda.

![png](ex_empirico_01_files/ex_empirico_01_9_0.png)
    

***

## Modelos de Regressão

Antes de passar para a estimação dos modelos, é necessário retirar o efeito das diferentes escalas de medidas dos dados. Isto é, como as notas das matérias da Universidade de São Paulo são medidas numa escala de 0 a 10 e a prova da Fuvest é medida em uma escala de 0 a 90, precisamos normalizar (trazer para um intervalo entre 0 e 1) os valores dessas variáveis. Terminado o procedimento descrito, a nova base de dados ficará assim:

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
      <th>genero</th>
      <th>idade</th>
      <th>nota1</th>
      <th>nota2</th>
      <th>fuvest</th>
      <th>gosta_curso</th>
      <th>frequencia</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M</td>
      <td>23</td>
      <td>0.625</td>
      <td>0.625</td>
      <td>0.68750</td>
      <td>S</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M</td>
      <td>21</td>
      <td>1.000</td>
      <td>1.000</td>
      <td>0.81250</td>
      <td>S</td>
      <td>S</td>
    </tr>
    <tr>
      <th>2</th>
      <td>F</td>
      <td>21</td>
      <td>0.650</td>
      <td>0.575</td>
      <td>0.65625</td>
      <td>S</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M</td>
      <td>23</td>
      <td>0.750</td>
      <td>0.200</td>
      <td>0.53125</td>
      <td>S</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M</td>
      <td>22</td>
      <td>0.875</td>
      <td>0.650</td>
      <td>0.71875</td>
      <td>S</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>

Posto isso, podemos estimar o modelo:

$$nMAE0229 = \hat{\beta_0} + \hat{\beta_1}nMAE0219 + \hat{u}_i$$ 

Onde $nMAE0229$ é a nota dos alunos em Introdução à Probabilidade e Estatística I e $nMAE0229$ é a nota dos alunos em Introdução à Probabilidade e Estatística II.  

<center>

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                  nota2   R-squared:                       0.198
    Model:                            OLS   Adj. R-squared:                  0.179
    Method:                 Least Squares   F-statistic:                     10.62
    Date:                Mon, 23 May 2022   Prob (F-statistic):            0.00219
    Time:                        22:50:40   Log-Likelihood:                 15.114
    No. Observations:                  45   AIC:                            -26.23
    Df Residuals:                      43   BIC:                            -22.61
    Df Model:                           1                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [0.025      0.975]
    ------------------------------------------------------------------------------
    const          0.1507      0.113      1.339      0.188      -0.076       0.378
    nota1          0.4599      0.141      3.259      0.002       0.175       0.745
    ==============================================================================

</center>

<center>

![png](ex_empirico_01_files/ex_empirico_01_14_0.png)
    
</center>


Os resultados da regressão acima dizem que um ponto a mais na nota de Introdução à Probabilidade e Estatística I (MAE0219), está associado a um aumento de $0.4599$ décimos na nota de Introdução à Probabilidade e Estatística II (MAE0229). Esse resultado faz algum sentido lógico, pois é esperado que alunos com mais base se saiam melhores nas matérias que presumem conhecimento prévio.

Entretanto, é necessário notar que o $R^2$ da regressão é de $0.1981$, o que significa que o modelo especificado explica apenas 19% da varição da nota em MAE0229. De fato, houve a omissão de variáveis que podem impactar significativamente o grau de ajuste do modelo, tais como a idade dos alunos e o seu nível de preparação ao sair do ensino médio - medido pela nota da Fuvest. 

Para corrigir o erro de omissão de variável do modelo anterior, estimaremos um novo modelo, dado por:

$$nMAE0229 = \hat{\beta_0} + \hat{\beta_1}nMAE0219 + \hat{\beta_2}nFUVEST + \hat{u}_i$$

Onde as varáveis anteriores mantém seu significado e $nFUVEST$ é a nota dos alunos na última prova da FUVEST que prestaram. 

<center>

                                OLS Regression Results                            
    ==============================================================================
    Dep. Variable:                  nota2   R-squared:                       0.224
    Model:                            OLS   Adj. R-squared:                  0.186
    Method:                 Least Squares   F-statistic:                     5.912
    Date:                Mon, 23 May 2022   Prob (F-statistic):            0.00555
    Time:                        22:50:40   Log-Likelihood:                 15.094
    No. Observations:                  44   AIC:                            -24.19
    Df Residuals:                      41   BIC:                            -18.83
    Df Model:                           2                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [0.025      0.975]
    ------------------------------------------------------------------------------
    const          0.0846      0.139      0.611      0.545      -0.195       0.364
    nota1          0.4714      0.147      3.213      0.003       0.175       0.768
    fuvest         0.0879      0.141      0.622      0.538      -0.198       0.373
    ==============================================================================
    
</center>

Os resultados da regressão acima indicam que, mantendo a nota em MAE0219 constante, um ponto a mais na prova da Fuvest está associado a um aumento de 8,79% na média de MAE0229. Em outras palavras, dados dois estudantes com a mesma nota em MAE0219, a previsão é que o estudante que tiver obtido a maior nota na Fuvest terá uma nota 8,79% maior em MAE0229.

Analogamente, mantendo a nota da Fuvest constante, um aumento na nota de MAE0219 está associado a um aumento de 47% da média de MAE0229.

Entretanto, vale notar que o $R^2$ da regressão ainda é baixo - somente 22% da variação da nota em MAE0229 é explicada pelas variáveis da regressão. Isto é um indicativo de que temos outras variáveis no termo de erro $u_i$ que ajudam a explicar melhor a variação da nota de Introdução à Probabilidade e Estatística II. Em última instância, a omissão dessas variáveis (por exemplo, as variáveis categóricas que possuímos nas bases) podem causar um problema de viés dos estimadores da nossa regressão.
