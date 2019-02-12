# Combining_Predictive_Techniques
Final Project - ND Predictive Analysis for Business


## Tarefa 1: Determine formatos de loja para as lojas existentes

1.	Qual é o número ideal de formatos de loja? Como você chegou a esse número?

O número ideal de formatos de loja foi baseado nos dados de 2015 e utilizamos a média de vendas por categoria e loja para cada agrupamento. A algoritmo de clusterização utilizado foi o K-Means e os gráficos e tabela abaixo mostram que o número ideal de clusters é de 3, isso por conta que ambos gráficos (Adjusted Rand Indices e Calinski-Harabasz Indices) mostram uma mediana maior dentro do cluster 3.


![image](https://user-images.githubusercontent.com/34245933/52661432-300e1e00-2ee9-11e9-9b94-b48a5a3aff5a.png)  
*Figura 1: K-Means Cluster Assessment Report*

![image](https://user-images.githubusercontent.com/34245933/52661468-46b47500-2ee9-11e9-9ee8-2575a9516171.png)  
*Figura 2: Adjusted Rand Indices e Calinski-Harabasz Indices*



2.	Quantas lojas enquadram-se em cada formato?

Com base nos números gerados pela ferramenta K-Centroids Cluster Analysis, temos um total de **23 lojas** para o **Cluster 1**, **29 lojas** para o **Cluster 2** e **33 lojas** para o **Cluster 3**.


![image](https://user-images.githubusercontent.com/34245933/52661555-795e6d80-2ee9-11e9-9e79-7e0b2faf921e.png)  
*Figura 3: Cluster Information*



3.	Com base nos resultados do modelo de agrupamento, de que forma os clusters diferem um do outro?

Analisando os resultados do total de vendas e das categorias com maior representatividade dentro dos nossos dados (Grocery, Merchandise & Produce) percebemos, conforme gráficos abaixo, que o Cluster 1 tem maior representatividade no Total Sales, Grocery & Merchandise, enquanto o Cluster 2 se mostra maior para a categoria Produce. O Cluster 3 se mostra mais flat sem muita variação dentro do próprio range, ou seja, as lojas são muito parecidas em questões de vendas.



![image](https://user-images.githubusercontent.com/34245933/52661591-8bd8a700-2ee9-11e9-969b-fe00f06c130a.png)  
*Figura 4: Sales Category Plot in Tableau*


![image](https://user-images.githubusercontent.com/34245933/52661679-b165b080-2ee9-11e9-967d-7398986182f5.png)  
*Figura 5: Sales Map by Store & Cluster in Tableau*



https://public.tableau.com/profile/jose.cypriano.de.oliveira.junior#!/


## Tarefa 2: Formato das lojas novas

1.	Qual metodologia você usou para prever o melhor formato para as lojas novas?

Após aplicar os modelos de Decision Tree, Random Forest e Boosted e analisar os resultados de acurácia de cada metodologia, percebemos que o modelo Boosted tem mais aderência aos nossos dados. Por mais que o modelo Boosted tenha a mesma acurácia do modelo Random Forest, a variável F1 tem mais precisão no modelo escolhido, conforme podemos ver na tabela abaixo.


![image](https://user-images.githubusercontent.com/34245933/52661825-0275a480-2eea-11e9-8b96-a6fa3580e15b.png)  
*Figura 6: Model Comparison Report*


2.	Quais são as três variáveis mais importantes que ajudam a explicar a relação entre os indicadores demográficos e o formato das lojas?

De acordo com o gráfico de importância das variáveis, percebemos que as variáveis que mais explicam a relação entre os indicadores demográficos e o formato das lojas são: Age0to9, HVal750kPlus e EdHsGrad.


![image](https://user-images.githubusercontent.com/34245933/52661848-0f929380-2eea-11e9-85d5-6f5d05062300.png)  
*Figura 7: Importance Plot*


3.	Em que formato cada uma das 10 lojas novas se enquadra? Preencha a tabela abaixo:

Id da Loja	   Segmento
S0086	            3
S0087	            2
S0088	            1
S0089	            2
S0090	            2
S0091	            1
S0092	            2
S0093	            1
S0094	            2
S0095	            2


## Tarefa 3: Prevendo a vendas de produtos

1.	Qual tipo de modelo, ETS ou ARIMA, você usou para cada previsão? Use a notação ETS (a, m, n) ou ARIMA (ar, i, ma). Como você chegou a essa decisão?

Ambos os modelos ETS não amortecido e ARIMA foram utilizados para a previsão do nosso problema.
Para o modelo ETS (Erro, Trend & Seasonality) percebemos uma sazonalidade dentro dos anos, portanto utilizamos o modelo multiplicativamente. Em relação à tendência, não foi observado nenhum tipo de tendência nos dados, portanto não utilizamos essa variável. O indicador de erro, demonstrado no gráfico Remainder, demonstra claramente uma variação ao longo do tempo, portanto consideramos o modelo como multiplicativamente. Podemos ver todos os pontos descritos nos gráficos abaixo.


![image](https://user-images.githubusercontent.com/34245933/52661945-4b2d5d80-2eea-11e9-9b60-1774bddb93ed.png)  
*Figura 8: Error, Trend & Seasonality*

Para o modelo ARIMA, por conta dos nossos dados conterem sazonalidade e o modelo de trabalhar com dados estacionários, precisamos ajustar a séria temporal para estacionária, utilizando a metodologia de diferença sazonal. Nos gráficos abaixo vemos uma alta variabilidade dos dados e alta correlação nos números, devido a sazonalidade.

![image](https://user-images.githubusercontent.com/34245933/52661959-57b1b600-2eea-11e9-8686-4b0b543d4082.png)  
*Figura 9: ACF & PACF sem diferenciação*

Após fazermos a primeira transformação pela diferenciação, percebemos que os dados ficaram estacionários, ou seja, podemos considerar que a primeira diferença sazonal ajusta os nossos dados para a aplicação do modelo.

![image](https://user-images.githubusercontent.com/34245933/52661978-64cea500-2eea-11e9-9eb9-97219f40e9ec.png)  
*Figura 10: ACF & PACF primeira diferença sazonal*


Como os dados estão estacionários, podemos fazer a definição dos termos de AR e/ou MA para aplicação do modelo. Para as séries não sazonais, como lag-1 é positivo e pouco correlacionado, podemos considerar os termos: AR = 1, I = 0 e MA = 1. Enquanto as séries sazonais, percebemos que há mais picos nos intervalos à cada 6 meses, portanto podemos assumir que os termos são: AR = 0, I = 1 e MA = 0. Por fim, nosso modelo fica da seguinte forma: ARIMA (1,0,1) (0,1,0) [12].
Por fim, ao analisar os resultados de ambos os modelos, percebemos que o ETS tem melhor aderência aos nossos dados, portanto é o que devemos usar para realizar nossa previsão. Percebemos isso, pois os indicadores de RMSE e MASE são menores para ETS (RMSE: 1,020,596 | MASE: 0.45), em relação ao modelo de ARIMA (RMSE: 1,352,529 | MASE: 4.28), conforme podemos ver na tabela abaixo. 

![image](https://user-images.githubusercontent.com/34245933/52662010-74e68480-2eea-11e9-97a9-c28047694c85.png)  
*Figura 11 - Model Comparison*


Além dos indicadores de erro mostrarem que o modelo ETS tem mais acurácia nos nossos dados, o indicador AIC é maior para ETS (1,283) em relação ao ARIMA (1,073).

Abaixo segue conceitos dos indicadores de RMSE, MASE e AIC:

Root Mean Squared Error (RMSE): representa o desvio padrão das diferenças entre os valores previstos e realizados. Esta é uma ótima medida para ser usado quando se deseja comparar modelos porque ela mostra quantos desvios padrão o valor previsto está da média.
Mean Absolute Scaled Error (MASE): é outra medida relativa de erro que é aplicável somente a dados de séries temporais. É definida como o erro médio absoluto do modelo dividido pelo valor médio absoluto da primeira diferença da série. Como a medida de erro é relativa e pode ser aplicado entre os vários modelos, é considerado uma das melhores métricas para a medição do erro.
Akaike Information Criterion (AIC): Mede a qualidade relativa de um modelo estatístico. Esse cálculo equilibra a qualidade do fit do modelo e a complexidade do modelo. Podemos falar que esse é o melhor indicador para definir se um modelo é melhor que outro.

Abaixo os dados gerados para a previsão dos nossos números, utilizando a metodologia de ETS non dempened.


![image](https://user-images.githubusercontent.com/34245933/52662041-829c0a00-2eea-11e9-9a7c-38f6ebd35bad.png)  
*Figura 12 – Forecast Results using ETS Model*


![image](https://user-images.githubusercontent.com/34245933/52662050-8a5bae80-2eea-11e9-8e02-64bca60e0268.png)  
*Figura 13 – Forecast Results Table*


2.	Envie um dashboard do Tableau (salvo como um arquivo público do Tableau) que inclua uma tabela e um gráfico das três previsões mensais; um para as existentes, um para as novas e um para todas as lojas. Nomeie a aba no arquivo "Tarefa 3” do Tableau.

Abaixo tabela de previsão de vendas para as novas e existentes lojas.

![image](https://user-images.githubusercontent.com/34245933/52662080-9ba4bb00-2eea-11e9-820c-d4edb33779b5.png)  
*Figura 14: Tabela Forecast de Vendas para Novas e Existentes lojas*


![image](https://user-images.githubusercontent.com/34245933/52662105-a4958c80-2eea-11e9-9e12-aef0d2f48b52.png)  
*Figura 15: Dados históricos e Forecast de Vendas para Novas e Existentes lojas*

https://public.tableau.com/profile/jose.cypriano.de.oliveira.junior#!/
