---
"lang": "pt-br",
"title": "Exercício Empírico III",
"subtitle": "Econometria I - EAE0324",
"authors": ["Vitor Baldoino - 11766857"],
"date": "Julho 2022"
---

***

## Descrição dos Dados

O objetivo deste exercício é estimar quais fatores influenciam o desempenho das escolas no SAEB em Matemática e Português. Para isto, usaremos os Dados da Educação Básica de 2013. Nesta base, possuímos informações sobre as notas das escolas, número de matrículas, número de professores, localização, entre outras.

Antes de partir para a estimação dos modelos, seguem a quantidade de escolas por região e sua oferta dos níveis de ensino. Através do último gráfico, vemos que as escolas que oferecem todos os níveis de ensino não minoria.

<p align="center">
  <img src="ex_empirico_03_files/estats_descritivas_ex_empirico_03_01.png"/>
</p>

<p align="center">
  <img src="ex_empirico_03_files/estats_descritivas_ex_empirico_03_02.png"/>
</p>

## Modelos de Regressão


### Modelo 01

Como abordagem inicial, estimaremos o modelo:

$$\text{final-mat} = \beta_0 + \beta_1 \text{salas} + \beta_2 \text{professores} + \beta_3 \text{funcionarios} + \beta_4 \text{rural} + u_i$$

Onde as variáveis "``salas``", "``professores``" e "``funcionários``" indicam as quantidades respectivias para cada escola e a variável "rural" é uma *dummy* que assume o valor $1$ quando a escola está situada na área rural e $0$ caso a escola esteja na região urbana. Além disso, é esperado que os sinais das variáveis "``salas``", "``professores``" e "``funcionários``" sejam positivos, indicando que mais recursos à disposição dos alunos - tanto físicos quanto humanos - impactem positivamente o seu desempenho escolar. Já para a variável "``rural``", é esperado que seu sinal seja negativo, seguindo a percepção difundida no senso comum de que moradores de áreas rurais tendem a ter mais dificuldade no acesso à educação.

<center>

                                    Modelo 01                                   
    ==============================================================================
    Dep. Variable:              final_mat   R-squared:                       0.074
    Model:                            OLS   Adj. R-squared:                  0.074
    No. Observations:               24425   Prob (F-statistic):               0.00
    Covariance Type:                  HC1   Prob(JB):                    1.11e-306
    =======================================================================================
                            coef    std err          z      P>|z|      [0.025      0.975]
    ---------------------------------------------------------------------------------------
    const                 250.4236      0.469    533.926      0.000     249.504     251.343
    nu_salas_utilizadas     0.3304      0.048      6.914      0.000       0.237       0.424
    num_proffundamental     0.0126      0.004      3.036      0.002       0.004       0.021
    nu_funcionarios        -0.0060      0.013     -0.463      0.644      -0.031       0.019
    rural                 -11.9353      0.418    -28.521      0.000     -12.756     -11.115
    =======================================================================================

    Notes: Standard Errors are heteroscedasticity robust (HC1)

</center>

Começando pelo termo de erro, o p-valor do teste de Jarque-Bera indica sucesso ao rejeitar a hipótese nula de que os erros do modelo seguem uma distribuição normal. Apesar disso, seguiremos com a interpretação geral do modelo e o teste de hipóteses.

Os resultados do primeiro modelo confirmam, em grande parte, as nossas suposições feitas *a priori*. Para este modelo, uma sala a mais na escola está relacionada, em média, com $0,3304$ pontos adicionados à nota na seção de matemática do SAEB de um aluno do ensino fundamental II. De forma análoga, um professor a mais dedicado ao ensino fundamental está relacionado com um aumento de $0,0126$ pontos na mesma nota. Os resultados para ambas as variáveis são estatisticamente significantes ao nível de 5%.

Uma ressalva deve ser feita ao efeito do número de funcionários da escola: os resultados dizem que um membro a mais no *staff* da escola diminui a nota dos alunos na seção de matemática do SAEB em $0,006$, entretanto, esse resultado não é estatisticamente diferente de zero com uma significância de 5%.

Adicionalmente, é possível ver que escolas em áreas rurais realmente possuem uma desvantagem grande em relação às escolas em zonas urbanas. Segundo os resultados da regressão, os alunos de escolas em zonas rurais tem uma nota, em média, $11,9$ pontos menor.

Por fim, conforme a medida de ajuste $R^2$, este primeiro modelo explica 7,4% da variação dos dados e, conforme a estatística F, as variáveis da regressão são estatisticamente diferentes de zero quando consideradas de forma conjunta. Além disso, é importante notar que os desvios padrão do modelo foram ajustados para heterocedasticidade seguindo o proposto por White.

### Modelo 02

Tendo em vista os resultados acima, iremos estimar o próximo modelo:

$$\text{inicial-mat} = \beta_0 + \beta_1 \text{salas} + \beta_2 \text{professores} + \beta_3 \text{matriculas} + \beta_4 \text{rural} + \beta_5 \text{espaço-escola} + u_i$$

Onde a variável "``matrículas``" indica o número de alunos matriculados naquela escola da 1º à 4º série do ensino fundamental. Já a variável "``espaço-escola``" indica a completude do espaço escolar, isto é, se ele oferece laboratórios (informática e ciências), quadra, cozinha, biblioteca, sala de leitura, Internet e alimentação, sendo o número 8 atribuído para a escola que oferece todos esses recursos e 0 para a escola que não oferece nenhum deles. As variáveis trazidas do modelo anterior mantêm seus significados.

É esperado que a variável "``matrículas``" apresente um sinal negativo, indicando que escolas super-lotadas diminuem o desempenho acadêmico dos alunos. Já para a variável "``espaço-escola``", espera-se que seu sinal seja positivo, sinalizando que espaços mais completos influenciam positivamente o desempenho dos alunos. O sinal esperado das outras variáveis permanece o mesmo.

<center>

                                    Modelo 02                                   
    ==============================================================================
    Dep. Variable:            inicial_mat   R-squared:                       0.171
    Model:                            OLS   Adj. R-squared:                  0.171
    No. Observations:               39944   Prob (F-statistic):               0.00
    Covariance Type:                  HC1   Prob(JB):                         0.00
    =======================================================================================
                            coef    std err          z      P>|z|      [0.025      0.975]
    ---------------------------------------------------------------------------------------
    const                 191.9743      0.507    378.428      0.000     190.980     192.969
    nu_salas_utilizadas     0.0393      0.025      1.600      0.110      -0.009       0.087
    num_proffundamental    -0.0115      0.003     -3.909      0.000      -0.017      -0.006
    num_matri_fund_1a4     -0.1789      0.163     -1.096      0.273      -0.499       0.141
    rural                 -10.9903      0.331    -33.217      0.000     -11.639     -10.342
    com_escola_1            5.9185      0.101     58.313      0.000       5.720       6.117
    =======================================================================================

    Notes: Standard Errors are heteroscedasticity robust (HC1)

</center>

Os resultados acima indicam algumas diferenças com o primeiro modelo estimado. Notavelmente, a variável "``num_proffundamental``" mudou de sinal, divergindo da intuição delineada *à priori*, e a variável "``nu_salas_utilizadas``" deixou de ser estatisticamente significante ao nível de 5%. De forma geral, este segundo modelo apresenta um ajuste melhor aos dados, explicando 17% da variação da variável dependente, mas continua desrespeitando a hipótese da normalidade do termo de erro, da mesma forma que o modelo anterior.

Quanto aos outros resultados e às novas variáveis, pode-se ver que uma escola mais completa impacta positivamente a nota na seção de matemática do SAEB de um aluno do ensino fundamental I. Mas, apesar do resultado estatisticamente significante, devemos notar que essa variável atribui o mesmo peso relativo a todos os sub-indicadores que entram em seu cálculo ("``in_laboratorio_informatica``", "``in_laboratorio_ciencias``", "``in_quadra_esportes``", etc), o que pode não ser verdade em todas as situações. Por exemplo, é razoável presumir que a presença de uma biblioteca no espaço escolar contribua mais para o desempenho de um aluno do que a presença de uma quadra de esportes.

Adicionalmente, os resultados da regressão indicam que uma matrícula a mais nas turmas do ensino fundamental I diminui, em média, $0,17$ ponto no resultado do SAEB de um aluno. Entretanto, esse resultado não é estatisticamente significante ao nível de 5%.

Por fim, os comentários para os erros padrões robustos, a estatística F e para a variável "``rural``" permanecem os mesmos, salvo a mudança de magnitude no coeficiente da variável.

### Modelo 03 

Por último, iremos estimar o modelo:

$$\text{inicial-pt} = \beta_0 + \beta_1 \text{matri/prof} + \beta_2 \text{matri/sala} + \beta_3 \text{rural} + \beta_4 \text{espaço-escola} + \beta_5 \text{biblioteca} + \beta_6 \text{leitura} + u_i$$

Diferentemente dos anteriores, a lógica dessa forma funcional não parte da observação em nível do capital físico e humano das escolas, mas sim da sua situação relativa ao número de alunos da escola e como ela impacta o desempenho acadêmico dos alunos do ensino fundamental I. Posto isso, as variáveis "``matri/prof``" e "``matri/sala``" indicam o número de alunos para cada professor e o número de alunos em cada sala, respectivamente. As variáveis "``biblioteca``" e "``leitura``" são *dummies* que indicam, respectivamente, a presença de uma biblioteca e uma sala de leitura na escola. É importante notar, entretanto, que as variáveis "``biblioteca``" e "``leitura``" foram retiradas do cálculo da variável "``espaço-escola``" para que não incorrêssemos em multicolineariedade. Com isso, o valor atribuído às escolas mais completas passa a ser 6.

Também em contraste aos modelos anteriores, o sinal esperado das variáveis deste modelo é negativo, exceção feita as variáveis "``biblioteca``", "``leitura``" e "``espaço-escola``". Esperar que o sinal das outras variáveis do modelo seja negativo reflete a intuição de que um maior número de alunos para cada professor e sala indica uma sobrecarga dos docentes e, talvez, a precariedade do espaço escolar. Esses fatores, em última instância, teriam efeito negativo no desempenho acadêmico dos alunos.

<center>

                                    Modelo 03                                   
    ==============================================================================
    Dep. Variable:             inicial_pt   R-squared:                       0.204
    Model:                            OLS   Adj. R-squared:                  0.204
    No. Observations:               39944   Prob (F-statistic):               0.00
    Covariance Type:                  HC1   Prob(JB):                     8.74e-21
    ===================================================================================
                        coef    std err          z      P>|z|      [0.025      0.975]
    -----------------------------------------------------------------------------------
    const             187.1190      0.413    453.426      0.000     186.310     187.928
    matri/prof         -2.8782      2.321     -1.240      0.215      -7.428       1.671
    matri/salas        -0.0922      1.172     -0.079      0.937      -2.390       2.205
    rural             -12.4252      0.313    -39.662      0.000     -13.039     -11.811
    com_escola_2        7.0949      0.123     57.646      0.000       6.854       7.336
    in_biblioteca       2.6456      0.258     10.256      0.000       2.140       3.151
    in_sala_leitura     2.1871      0.266      8.229      0.000       1.666       2.708
    ===================================================================================

    Notes: Standard Errors are heteroscedasticity robust (HC1)

</center>

Os resultados do terceiro e último modelo, repetem os resultados para o teste de Jarque-Bera e para a estatistica F obtidos no primeiro modelo. Observando a tabela de resumo, é possível ver que o ajuste deste modelo ($R^2$) é ligeiramente maior do que o do modelo anterior, entretanto, é possível que isso reflita a característica não decrescente do $R^2$, e não a efetividade do modelo proposto em explicar as mudanças da variável dependente.

Posto isso, os coeficientes das variáveis "``matri/prof``" e "``matri/sala``" seguem a intuição definida anteriormente, entretanto, esses mesmos coeficientes falham em rejeitar a hipótese nula ao nível de 5% de significância. Um dos fatores por trás desse resultado pode residir em uma limitação da base de dados, que não discrimina o número de professores e salas dedicadas ao ensino fundamental I. Com isso, o cálculo dessas variáveis foi feito utilizando a quantidade total de professores e salas destinada às duas etapas do ensino fundamental, o que, provavelmente, leva a subestimação das razões "``matri/prof``" e "``matri/sala``". Em contrapartida, as variáveis "``biblioteca``" e "``leitura``" seguem a intuição proposta anteriormente e são estatisticamente significativas, indicando que a presença desses ambientes nas escolas leva a um aumento de cerca de 2 pontos na nota da seção de português do SAEB dos alunos do ensino fundamental I.