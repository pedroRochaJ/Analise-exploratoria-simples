# Analise-exploratoria-simples
Para fazer essa pequena análise, eu utilizei um dataset do cálculo que contém 3 espécies de flores e seus respectivos dados acerca da largura e 
comprimento das pétalas e sépalas. Basicamente, eu busquei entender a variação desses dados em cada espécie com a utilização de gráficos e também
visualizei a correlação entre esses dados.

#Primeiro iremos importar nossas bibliotecas
import pandas as pd
import numpy as np
import sweetviz as sv
import matplotlib.pyplot as plt
from collections import Counter
import seaborn as sns

iris = pd.read_csv("iris.csv")
iris.head()
	Id	SepalLengthCm	SepalWidthCm	PetalLengthCm	PetalWidthCm	Species
0	 1	       5.1	          3.5	         1.4	      0.2	     Iris-setosa
1	 2	       4.9	          3.0	         1.4	      0.2	     Iris-setosa
2  3	       4.7	          3.2	         1.3	      0.2	     Iris-setosa
3	 4	       4.6	          3.1	         1.5	      0.2	     Iris-setosa
4	 5	       5.0	          3.6	         1.4	      0.2	     Iris-setosa

#Descrição dos principais dados estatísticos do dataset
iris.describe()

df = pd.read_csv(r'iris.csv')
#Dessa maneira podemos ter uma visão mais geral dos dados
df

#Formado por 150 linhas e 6 colunas 
df.shape

#Visualização dos tipos de dados e nome das colunas
df.info()

#Verificando a presença de valores nulos no dataset
df.isnull()
df.isnull().sum()
Id               0
SepalLengthCm    0
SepalWidthCm     0
PetalLengthCm    0
PetalWidthCm     0
Species          0
#É bom saber que não há valores nulos 

#Verificando a quantidade de espécies de flores no dataset
list_species= Counter(df.Species).keys()
#Quantidade de dados para a mesma espécie
print(Counter(df.Species).values())
num = len(list_species)
print("Há %s espécies presentes" %(num))
Resultados: 
dict_values([50, 50, 50])
Há 3 espécies presentes

#Fazer um gráfico pegando uma espécie e o comprimento de sua pétala e verificar sua variação
flowers=df.Species[:50]
petal=df.PetalLengthCm[:50]
plt.title("Comparação entre a mesma espécie do comprimento da pétala (iris-setosa)")
plt.ylabel("Tamanho da pétala em (cm)")
plt.xlabel("Iris-setosa")
plt.bar(range(len(flowers)), petal)
plt.show()
![image](https://user-images.githubusercontent.com/113612805/205777950-04301db5-a857-4ae9-9fb2-b62e56f5fc99.png)

flowersIV=df.Species[51:100]
petalIV=df.PetalLengthCm[51:100]
plt.title("Comparação entre a mesma espécie do comprimento de pétala (iris-versicola)")
plt.ylabel("Tamanho da pétala em (cm)")
plt.xlabel("Iris-Versicola")
plt.bar(range(len(flowersIV)), petalIV)
![image](https://user-images.githubusercontent.com/113612805/205777984-00b1cfa3-322c-4f09-9974-2344085f83a1.png)


flowers2=df.Species[101:151]
petal2=df.PetalLengthCm[101:151]
plt.title("Comparação entre a mesma espécie do comprimento de pétala (iris-versicola)")
plt.ylabel("Tamanho da pétala em (cm)")
plt.xlabel("Iris-")
plt.bar(range(len(flowers2)), petal2)
![image](https://user-images.githubusercontent.com/113612805/205778007-62909843-6db5-448e-b6fa-97926b34fe73.png)

#Iremos criar um gráfico para visualizar a comparação entre as espécies. (Eu entendo que estatísticamente não há para que isso ser feito, no entanto, antes de tudo
esse projeto é para fixação das minhas habilidades.)
md1=df.PetalLengthCm.loc[0:50].mean()
md2=df.PetalLengthCm.loc[51:100].mean()
md3=df.PetalLengthCm.loc[101:150].mean()
lista_media=[]
lista_media.extend((md1,md2,md3))

nome_especies = Counter(df.Species).keys()
plt.xticks(range(len(nome_especies)), nome_especies)
plt.ylabel("Comprimento da pétala em cm")
plt.bar(range(len(nome_especies)), lista_media)
![image](https://user-images.githubusercontent.com/113612805/205778247-2cf5d7b2-c981-48d7-845f-21d96b532b2d.png)

import seaborn as sns
_ = sns.boxplot(x="Species", y="PetalLengthCm", data=df)
![image](https://user-images.githubusercontent.com/113612805/205778319-3df35a8d-f18f-46f6-8e6e-408d6100f2d2.png)
#Com base na visualização do gráfico podemos notar que a variância da iris-setosa é bem menor se comparado ao restante

df.corr()
	        Id	SepalLengthCm	SepalWidthCm	PetalLengthCm	PetalWidthCm
          Id	1.000000	0.716676	-0.397729	0.882747	0.899759
SepalLengthCm	0.716676	1.000000	-0.109369	0.871754	0.817954
SepalWidthCm	-0.397729	-0.109369	1.000000	-0.420516	-0.356544
PetalLengthCm	0.882747	0.871754	-0.420516	1.000000	0.962757
PetalWidthCm	0.899759	0.817954	-0.356544	0.962757	1.000000
#Correlação entre as variáveis
#Correlação menor que zero:Se a correlação é menor que zero, significa que é negativo, 
#isto é, que as variáveis são inversamente relacionadas.
#Correlação maior que zero: Se a correlação for igual a +1, significa que é perfeito positivo. 
#Neste caso, significa que a correlação é positiva, isto é, que as variáveis estão diretamente correlacionadas.


lim_varx = df.SepalLengthCm.loc[0:50]
lim_vary = df.PetalLengthCm.loc[0:50]
_ = sns.displot(lim_varx, kde=True) #displot faz a distribuição normal
_ = sns.displot(lim_vary, kde=True) #displot faz a distribuição normal
#_ = sns.boxplot(x="lim_varx", y="lim_vary", data=df)
#Quanto maior o comprimento da sépala menor é a largura dela 
#Quanto maior o comprimento da sépala maior é o comprimento da pétala
![image](https://user-images.githubusercontent.com/113612805/205778501-85f0c553-5d3b-4e2f-9637-f10b00d3b7a1.png)
![image](https://user-images.githubusercontent.com/113612805/205778517-d9c95e07-2bc7-4516-b4ba-d98d3f44530b.png)
#Podemos afirmar que os dados são bem dispersos em torno da nossa medida central.


df.plot(kind='box', figsize=(10,6), subplots=True)
#De maneira geral esse gráfico corresponde as informações visuais descritas em df.describe()
Id                  AxesSubplot(0.125,0.11;0.133621x0.77)
SepalLengthCm    AxesSubplot(0.285345,0.11;0.133621x0.77)
SepalWidthCm      AxesSubplot(0.44569,0.11;0.133621x0.77)
PetalLengthCm    AxesSubplot(0.606034,0.11;0.133621x0.77)
PetalWidthCm     AxesSubplot(0.766379,0.11;0.133621x0.77)
dtype: object
![image](https://user-images.githubusercontent.com/113612805/205778865-a02319a8-6afc-4eac-8c41-14632692e274.png)


my_report = sv.analyze(iris)
my_report.show_html()
#Irá gerar uma página com as principais medidas estatísticas, nos possibilitando analisar os dados de uma forma mais rápida. Com essa biblioteca
é possível também comparar dados e ver graficamente e de forma interativa.
