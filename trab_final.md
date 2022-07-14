---
"lang": "pt-br",
"title": "Trabalho Final",
"subtitle": "Econometria I - EAE0324",
"authors": ["Vitor Baldoino - 11766857"],
"date": "Julho 2022"
---

***

O objetivo deste trabalho é entender como algumas variáveis econômicas impactam o número de óbitos de cidades brasileiras. Para tal, fazemos o uso de uma *cross-section* de municípios que contém a nossa variável explicada, o número de óbitos, e algumas possíveis variáveis explicativas, como a despesa orçamentária do município, população total, região geográfica, indicadores educacionais, entre outras. Esse trabalho foi inspirado pelo artigo [*US mortality by economic, demographic, and social characteristics: the National Longitudinal Mortality Study*](https://ajph.aphapublications.org/doi/epdf/10.2105/AJPH.85.7.949) de Sorlie, Backlund e Keller, publicado no *American Journal of Public Health* em 1995.

## Descrição dos Dados

***

A base utilizada neste trabalho é de elaboração própria, as bases de brutas para aquisição dos dados presentes aqui podem ser obtidas através do portal [*Base dos Dados*](https://basedosdados.org/) (a lista completa das bases utilizadas se encontra nas referências). Adicionalmente, os *scripts* utilizados para o tratamento, agregação e modelagem dos dados pode ser encontrado no [meu perfil do *GitHub*](https://github.com/baldoinov/econometria-i).


<style type="text/css">
  .column {
  float: left;
  width: 48.25%;
  padding: 5px;
}

.row::after {
  content: "";
  clear: both;
  display: table;
}
</style>
    
<center>  
  <div class="row">
    <div class="column">
      <img src="trab_final_files/trab_final_8_0.png" style="width:100%">
    </div>
    <div class="column">
      <img src="trab_final_files/trab_final_9_0.png" style="width:100%">
    </div>
  </div>
</center>


## Modelos de Regressão

***

A nossa abordagem para estimar o impacto de variáveis econômicas no número de óbitos de um município consiste em estimar três modelos:

$$log(\text{mortes}) = \beta_0 + \beta_1 log(\text{Pop}) + \beta_2 \text{Emprego} + \beta_3 log(\text{Despesa}) + \beta_4 \text{Evasão-EM} + \beta_5 \text{Nordeste} + u_i$$

$$log(\text{mortes}) = \beta_0 + \beta_1 log(\text{Pop}) + \beta_2\text{Emprego} + \beta_3 log(\text{Seg}) + \beta_4\text{Evasão-EM} + \beta_5\text{Nordeste} + u_i$$

$$log(\text{mortes}) = \beta_0 + \beta_1 log(\text{Pop}) + \beta_2 \text{Emprego} + \beta_{i, i = \{3, 4, 5\} } log(\text{Despesas}) + \beta_6\text{Evasão-EM} + \beta_7\text{(Alu/Turma)} + \beta_8\text{Nordeste} + u_i$$

Nestes modelos, as variáveis "``log(Pop)``", "``Emprego``", "``Evasão-EM``" representam o *log* da população, o tempo médio que um trabalhador permance empregado e a taxa de evasão do ensino médio de cada observação, respectivamente. A variável "``Nordeste``" é uma *dummy* que assume o valor 1 se o município observado é na região nordeste do país e 0 caso contrário. Espera-se que as variáveis "``log(Pop)``" e "``Evasão-EM``" possuam um sinal positivo, a primeira porque é natural que municípios maiores apresentem um maior número de óbitos e a última para refletir a intuição de que uma maior evasão escolar está relacionada à um baixo nível de instrução e, consequentemente, a uma vida mais curta. O sinal esperado da variável "``Emprego``" é positivo, relefetindo a ideia de que uma permanência maior em um emprego, na média, tende a aumentar a qualidade de vida de um trabalhador e, portanto, diminuir as chances de óbito.

No primeiro e segundo modelo, as variáveis "``log(Despesa)``" e "``log(Seg)``" são o *log* da despesa orçamentária total do município e o *log* do gasto em segurança público do município, respectivamente. Para o terceiro modelo, a variável representada como "``log(Despesas)``" contém o *log* da despesa orçamentária do município com segurança, assistência social e previdência. Esses gastos foram isolados e representados separadamente por se pensar que eles sejam mais importante para explicar o número de óbitos da cidade. Adicionalmente, espera-se que o sinal das variáveis de despesas orçamentárias seja negativo em todos os modelos, intuitivamente, esse sinal captaria a ideia que um gasto público maior tem a capacidade de aumentar o bem-estar geral e diminuir o número de óbitos do município.

No terceiro e último modelo, a variável "``Alu/Turma``" 

<center>

    ====================================================
                        Modelo 01  Modelo 02  Modelo 03 
    ----------------------------------------------------
    const               -4.5198*** -4.4103*** -4.5053***
                        (0.0849)   (0.0370)   (0.0552)  
    nordeste            -0.0515*** -0.0321*** -0.0049   
                        (0.0086)   (0.0095)   (0.0102)  
    log_populacao       0.9482***  0.9399***  0.9269*** 
                        (0.0035)   (0.0039)   (0.0056)  
    taxa_abandono_em    -0.0143*** -0.0138*** -0.0126***
                        (0.0011)   (0.0011)   (0.0011)  
    tempo_medio_emprego 0.0010***  0.0011***  0.0010*** 
                        (0.0002)   (0.0002)   (0.0002)  
    log_seguranca                  0.0039***  0.0037*** 
                                   (0.0007)   (0.0007)  
    log_assistencia                           0.0144*** 
                                              (0.0048)  
    log_previdencia                           0.0041*** 
                                              (0.0005)  
    log_despesa         0.0032                          
                        (0.0040)                        
    atu_em                                    -0.0023***
                                              (0.0009)  
    R-squared           0.9405     0.9409     0.9419    
    R-squared Adj.      0.9405     0.9409     0.9418    
    N                   4685.0000  4685.0000  4685.0000 
    Prob(F-statistic):  0.0000     0.0000     0.0000    
    Prob(JB):           0.0000     0.0000     0.0000    
    Covariance type:    HC1        HC1        HC1       
    ====================================================
    Standard errors in parentheses.
    * p<.1, ** p<.05, ***p<.01
    
</center>

