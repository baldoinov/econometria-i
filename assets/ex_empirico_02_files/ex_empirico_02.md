---
"lang": "pt-br",
"title": "Exercício Empírico II",
"subtitle": "Econometria I - EAE0324",
"authors": ["Vitor Baldoino"],
"date": "Junho 2022"
---

***

## Descrição e Tratamento dos Dados


O objetivo deste exercício é estimar o efeito dos hábitos e características diversas de um indivíduo em seu peso em gramas. Para isto, usaremos os dados da PNS (Pesquisa Nacional de Saúde) de 2013. Nesta base, possuímos informações sobre os hábitos, peso, altura, sexo, estado conjugal, alfabetização e idade dos indivíduos participantes, mas antes de estimarmos o primeiro modelo de regressão, é necessário tratar os dados e conhecer mais sobre a base.

Em primeiro lugar, utilizaremos o dicionário de variáveis fornecido com a base para lembrarmos os valores que serão utilizados ao longo de todo o exercício.


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
      <th>Código</th>
      <th>Significado</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c008</td>
      <td>Idade</td>
    </tr>
    <tr>
      <th>1</th>
      <td>p020</td>
      <td>Quantidade de Dias que Consome Refrigerante</td>
    </tr>
    <tr>
      <th>2</th>
      <td>p022</td>
      <td>Quantidade de Refrigerante Consumida</td>
    </tr>
    <tr>
      <th>3</th>
      <td>p045</td>
      <td>Horas assistindo TV</td>
    </tr>
    <tr>
      <th>4</th>
      <td>p05402</td>
      <td>Quantidad de Cigarro/Dia</td>
    </tr>
    <tr>
      <th>5</th>
      <td>w00103</td>
      <td>Peso (kg)</td>
    </tr>
    <tr>
      <th>6</th>
      <td>w00203</td>
      <td>Altura (cm)</td>
    </tr>
  </tbody>
</table>
</div>


</br>

O segundo passo de preparação deste exercício foi a conversão do peso em quilogramas (como foi passado na base original) para gramas e o preenchimento dos dados categóricos originais pela sua versão explicita. Ao final desse processo (cujo o código pode ser visto [aqui](https://github.com/baldoinov/econometria-i/blob/main/ex_empirico_02.ipynb)), terminamos com a seguinte base:



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
      <th>w00103</th>
      <th>c008</th>
      <th>p020</th>
      <th>p022</th>
      <th>p045</th>
      <th>p05402</th>
      <th>w00203</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>59500.0</td>
      <td>35</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>2.5</td>
      <td>0.0</td>
      <td>162.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>37</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>16</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>81200.0</td>
      <td>42</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>2.5</td>
      <td>0.0</td>
      <td>169.0</td>
    </tr>
  </tbody>
</table>
</div>



</br>

Com os dados tratados, podemos ver algumas estatísticas descritivas:


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
      <th>w00103</th>
      <th>c008</th>
      <th>p020</th>
      <th>p022</th>
      <th>p045</th>
      <th>p05402</th>
      <th>w00203</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>59402.00</td>
      <td>205546.00</td>
      <td>205546.00</td>
      <td>205546.00</td>
      <td>205546.00</td>
      <td>205546.00</td>
      <td>59402.00</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>70403.97</td>
      <td>32.28</td>
      <td>0.69</td>
      <td>0.35</td>
      <td>0.69</td>
      <td>0.38</td>
      <td>163.04</td>
    </tr>
    <tr>
      <th>std</th>
      <td>15215.30</td>
      <td>20.65</td>
      <td>1.70</td>
      <td>0.76</td>
      <td>1.41</td>
      <td>2.78</td>
      <td>9.74</td>
    </tr>
    <tr>
      <th>min</th>
      <td>30000.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>125.00</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>59700.00</td>
      <td>15.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>156.00</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>68600.00</td>
      <td>30.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>162.80</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>79200.00</td>
      <td>47.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.50</td>
      <td>0.00</td>
      <td>170.00</td>
    </tr>
    <tr>
      <th>max</th>
      <td>179000.00</td>
      <td>109.00</td>
      <td>7.00</td>
      <td>3.00</td>
      <td>6.50</td>
      <td>80.00</td>
      <td>203.00</td>
    </tr>
  </tbody>
</table>
</div>



</br>

Como indicado na tabela acima, nem todas as observações da nossa base estão completas. Por exemplo, a variável de interesse, peso (w00103), só possui 59402 observações de um total de 205546 entradas. Apesar desse fato, ainda possuímos dados o suficiente para estimarmos modelos com muitos graus de liberdade. 

## Modelos de Regressão

### Modelo 01

$$peso_g = \beta_0 + \beta_1 refrigerante_i + \beta_2 TV_i + \beta_3 cigarro_i + u_i$$

<center>

                          Modelo 01 - OLS Regression Results                      
    ==============================================================================
    Dep. Variable:                 w00103   R-squared:                       0.005
    Model:                            OLS   Adj. R-squared:                  0.005
    Method:                 Least Squares   F-statistic:                     91.56
    Date:                Thu, 16 Jun 2022   Prob (F-statistic):           4.08e-59
    Time:                        18:44:03   Log-Likelihood:            -6.5619e+05
    No. Observations:               59402   AIC:                         1.312e+06
    Df Residuals:                   59398   BIC:                         1.312e+06
    Df Model:                           3                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [0.025      0.975]
    ------------------------------------------------------------------------------
    const       6.898e+04    120.429    572.791      0.000    6.87e+04    6.92e+04
    p020         382.0815     25.664     14.888      0.000     331.779     432.384
    p045         227.6570     37.515      6.068      0.000     154.128     301.186
    p05402        -9.2446     12.417     -0.745      0.457     -33.581      15.092
    ==============================================================================
    Omnibus:                     6734.827   Durbin-Watson:                   1.921
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):            11124.096
    Skew:                           0.799   Prob(JB):                         0.00
    Kurtosis:                       4.394   Cond. No.                         10.8
    ==============================================================================

</center>    

    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    


    
![png](ex_empirico_02_files/ex_empirico_02_15_0.png)
    


O resultado da regressão acima nos diz que existe uma associação positiva entre o peso em gramas do indivíduo, a quantidade de dias que ele consome refrigerante ($\text{p020}$) e a quantidade de horas assistindo televisão. Isto é, *ceteris paribus*, consumir refrigerante um dia a mais na semana pode levar a um aumento do peso do indivíduo em cerca de 380 gramas, essa análise de estática comparativa pode ser extrapolada para as outras variáveis do modelo para demonstrar que uma hora a mais assistindo TV ($\text{p045}$) está associada a um ganho de 227 gramas e que o consumo de um cigarro a mais ($\text{p05402}$) está associado a uma diminuição de 9 gramas no peso do indivíduo. Segundo a tabela de resumo, o $R^2$ de $0.005$ indica que a regressão explica 0.5% da variação do peso do indivíduo em gramas. Dada a simplicidade do modelo inicial, é compreensível esse baixo poder explicativo.

Adicionalmente, para testarmos a hipótese de que cada parâmetro individual é igual a zero, isto é, $\beta_i = 0$, nós precisamos garantir que os resíduos do nosso modelo são distribuídos normalmente. É possível ver através das ferramentas gráficas acima que a distribuição do termo de erro do nosso modelo não se aproxima perfeitamente de uma distribuição normal, mas, apesar disso, prosseguiremos com o teste de hipóteses.

Os valores estimados para os nossos $\hat{\beta_i}$ são, respectivamente, $382.0815$, $227.6570$ e $-9.2446$. Através dos p-valores informados no tabela de resumo, podemos rejeitar a hipótese nula para os dois primeiros coeficientes ($\beta_1 \ne 0$ e $\beta_2 \ne 0$), mas não para o terceiro ($\beta_3$). Em suma, os resultados da nossa regressão são estatisticamente significantes ao nível de 5% para os dois primeiros coeficientes, mas não para o terceiro. Além disso, o p-valor da estatística $F$ nos mostra que os coeficientes da regressão, de forma conjunta, são estatisticamente significantes ao nível de 5%.

### Modelo 02

$$log(peso_g) = \beta_0 + \beta_1 refrigerante_i + \beta_2 TV_i + \beta_3 log(cigarro_i) + u_i$$

<center>

                          Modelo 02 - OLS Regression Results                      
    ==============================================================================
    Dep. Variable:             log_w00103   R-squared:                       0.004
    Model:                            OLS   Adj. R-squared:                  0.004
    Method:                 Least Squares   F-statistic:                     86.61
    Date:                Thu, 16 Jun 2022   Prob (F-statistic):           6.52e-56
    Time:                        18:44:04   Log-Likelihood:                 8194.7
    No. Observations:               59402   AIC:                        -1.638e+04
    Df Residuals:                   59398   BIC:                        -1.635e+04
    Df Model:                           3                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [0.025      0.975]
    ------------------------------------------------------------------------------
    const         11.1216      0.002   6636.866      0.000      11.118      11.125
    p020           0.0052      0.000     14.639      0.000       0.005       0.006
    p045           0.0028      0.001      5.356      0.000       0.002       0.004
    log_p05402    -0.0036      0.001     -3.148      0.002      -0.006      -0.001
    ==============================================================================
    Omnibus:                      106.804   Durbin-Watson:                   1.915
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):              112.630
    Skew:                           0.081   Prob(JB):                     3.49e-25
    Kurtosis:                       3.138   Cond. No.                         8.17
    ==============================================================================

</center>

    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    


    
![png](ex_empirico_02_files/ex_empirico_02_19_0.png)
    


Neste segundo modelo, o uso de $logs$ na variável dependente ( $log(\text{w00103})$ ) e na variável de consumo de cigarro ( $log(\text{p05402})$ ) modifica a interpretação dos coeficientes. Para o consumo de cigarro por dia, o coeficiente de estimado nos diz que o aumento de 1% no consumo de cigarro está associado a uma diminuição de 0.0036% no peso em gramas do indivíduo. De forma *semelhante*, podemos ver que um dia a mais consumindo refrigerante leva a um aumento de 0.52% no peso em gramas da pessoa e uma hora a mais assistindo teve está associada a um aumento de 0.28% no peso do indivíduo. Semelhantemente ao primeiro modelo, o $R^2$ de $0.004$ indica que a regressão explica 0,4% da variação do $log$ do peso do indivíduo em gramas, além disso, é interessante notar que o $\overline{R^2}$ não impôs nenhuma penalidade à conversão das variáveis $\text{w00103}$ e $\text{p05402}$ para $log$.

Como podemos ver pelos p-valores informados na tabela de resumo, todos os coeficientes estimados são estatisticamente significantes ao nível de 5%, o que nos leva a rejeitar a hipótese nula de que $\beta_i = 0$ e a hipótese conjunta de que todos os parâmetros são iguais a zero. Além disso, diferentemente do primeiro modelo, podemos ver pelos gráficos acima que o termo de erro da regressão tem uma distribuição bem próxima a uma normal, o que descarta considerações extras sobre a validade do nosso teste de hipóteses.

### Modelo 03

<center>

                          Modelo 03 - OLS Regression Results                      
    ==============================================================================
    Dep. Variable:             log_w00103   R-squared:                       0.295
    Model:                            OLS   Adj. R-squared:                  0.295
    Method:                 Least Squares   F-statistic:                     4138.
    Date:                Thu, 16 Jun 2022   Prob (F-statistic):               0.00
    Time:                        18:44:05   Log-Likelihood:                 18439.
    No. Observations:               59402   AIC:                        -3.686e+04
    Df Residuals:                   59395   BIC:                        -3.680e+04
    Df Model:                           6                                         
    Covariance Type:            nonrobust                                         
    ==============================================================================
                     coef    std err          t      P>|t|      [0.025      0.975]
    ------------------------------------------------------------------------------
    const          8.9629      0.014    635.219      0.000       8.935       8.991
    c008           0.0134      0.000     58.471      0.000       0.013       0.014
    c008_2        -0.0001   2.34e-06    -53.029      0.000      -0.000      -0.000
    p020_p022      0.0012      0.000      8.416      0.000       0.001       0.001
    p045           0.0072      0.000     16.422      0.000       0.006       0.008
    log_p05402    -0.0190      0.001    -19.552      0.000      -0.021      -0.017
    w00203         0.0113   7.83e-05    144.542      0.000       0.011       0.011
    ==============================================================================
    Omnibus:                      955.306   Durbin-Watson:                   1.964
    Prob(Omnibus):                  0.000   Jarque-Bera (JB):             1080.792
    Skew:                           0.271   Prob(JB):                    2.04e-235
    Kurtosis:                       3.378   Cond. No.                     5.27e+04
    ==============================================================================

</center>

    Notes:
    [1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
    [2] The condition number is large, 5.27e+04. This might indicate that there are
    strong multicollinearity or other numerical problems.
    


    
![png](ex_empirico_02_files/ex_empirico_02_23_0.png)
    

Neste terceiro e último modelo, estimamos a regressão:

$$log(\text{peso}) = \beta_0 + \beta_1 \text{idade}_i + \beta_2 \text{idade}^2 + \beta_3 (\text{p020} \times \text{p022}) + \beta_4 \text{TV}_i + \beta_5 log(\text{cigarro}_i) + \beta_6 \text{altura}_i + u_i$$

Neste modelo, a interação entre as variáveis $\text{p020}$ e $\text{p022}$ nos dá o consumo total de refrigerante pelo indivíduo na semana, e a idade ao quadrado nos mostra o efeito decrescente da idade no aumento percentual do peso.

Posto isso, esse terceiro modelo nos informa que a cada ano mais velho, um indivíduo tende a ganhar 1.34% gramas a mais. Entretanto, esse efeito atinge seu pico aos 67 anos de idade, onde os efeitos decrescentes da idade sobre o peso começam a aparecer. Analogamente, um aumento no consumo total de refrigerante do indivíduo, isto é, quantidade de refrigerantes tomados *vezes* a frequência desse consumo, está associado a um aumento de 0.12% no peso em gramas do indivíduo. O mesmo raciocinio pode ser aplicado aos coeficientes das variáveis de consumo de cigarro ($log(\text{p05402})$) e de altura ($log(\text{w00203})$).

Um ponto de notável diferença em relação aos modelos anteriores é grau de ajuste. O $R^2$ passou a explicar cerca de 30% da variação no peso em gramas dos indivíduos da amostra, isso sem sermos penalizados pela medida ajustada $\overline{R}^2$. Entretanto, cabe notar que ao incluír a variável altura podemos incorrer em um problema de multicolinearidade, dada a forte correlação entre a altura do indivíduo e seu peso.

Apesar do provável problema com multicolinearidade, o histograma de resíduos e o gráfico de distribuição de probabilidade normal expostos acima demonstram que o termo de erro do nosso modelo se aproxima bem o suficiente de uma distribuição normal. Tendo isso em mente, podemos testar sob cada parâmetro estimado a hipótese de que $\beta_i = 0$. O resultado desses testes, como é possível ver pelos p-valores da tabela de resumo, nos leva a rejeitar a hipótese nula ao nível de 5% de significância. Adicionalmente, como podemos ver pelo p-valor da estatística $F$, também podemos rejeitar a hipótese conjunta de que todos os parâmetros são iguais a zero.
