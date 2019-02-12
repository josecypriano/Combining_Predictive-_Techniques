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
