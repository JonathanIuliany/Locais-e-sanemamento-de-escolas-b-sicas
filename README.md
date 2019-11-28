# Locais-e-sanemamento-de-escolas-de-ensino-básico
analisar quantas escolas de ensino básico estão em região rural e urbana.
Analiar quantas escolas queimam , enterram ou recicla seu lixo e os impactos.
Desenvolvido por Thiago e Jonathan



Descrição breve (localização):

	Este é um trabalho de raspagem de dados, em que foi contado e montado um gráfico de barras duplas de escolas rurais e urbanas ao longo de cinco anos, entre 1995 e 1999. A linguagem de programação utilizada foi o python. Os arquivos lidos estavam na extenção "csv".



Origem dos Dados usados:

	Os dados foram coletados do site <http://inep.gov.br/microdados> na guia "Censo Escolar". Lembrando que foram pegos os anos de 1995 a 1999.



Resultados obtidos (localização):

import pandas as pd
censo= pd.read_csv('CENSOESC_1995.csv', usecols=['LOC'], squeeze=True)


#conta quantas escolas rurais e urbanas tem no arquivo CENSOESC_1995.csv.
censo95 = censo.value_counts()
censo95

>>>Rural     154723
>>>Urbana     88913
>>>Name: LOC, dtype: int64


DadosDesp95= pd.read_csv('DADOS_DESP_1995.csv', usecols=['LOC'], squeeze=True)

#conta quantas escolas rurais e urbanas tem no arquivo DADOS_DESP_1995.csv.
DadosDesp95 = DadosDesp95.value_counts()
DadosDesp95

>>>Urbana    46254
>>>Rural      3388
>>>Name: LOC, dtype: int64

DadosCurso95 = pd.read_csv('DADOSCURSO_1995.csv', usecols=['LOC'], squeeze=True)

#conta quantas escolas rurais e urbanas tem no arquivo DADOSCURSO_1995.csv.
DadosCurso95 = DadosCurso95.value_counts()
DadosCurso95

>>>Urbana    25002
>>>Rural       570
>>>Name: LOC, dtype: int64


#Total de escolas Rurais
rural95 = censo95['Rural'] + b['Rural'] + DadosCurso95['Rural']
rural95

>>>158681

#Total de escolas Urbanas
urbana95 = censo95['Urbana'] + DadosDesp95['Urbana'] + DadosCurso95['Urbana']
urbana95

>>>160169



urbana95 = '%.1f' %(urbana95/1000)
urbana95

>>>160.2

rural95 = '%.1f' %(rural95/1000)
rural95

>>>158.7


import matplotlib.pyplot as plt
import numpy as np

labels = ['1995', '1996', '1997', '1998', '1999']
urbana = [urbana95, urbana96, urbana97, urbana98, urbana99]
rural = [rural95, rural96, rural97, rural98, rural99]

x = np.arange(len(labels))  # localização do labels
width = 0.4# espessura da barra

fig, ax = plt.subplots()
rects1 = ax.bar(x - width/2, urbana, width, label='Urbana')
rects2 = ax.bar(x + width/2, rural, width, label='Rural')

# Adiciona texto aos rótulos
ax.set_ylabel('Valores dividido por 1,000')
ax.set_title('Localização das escolas de ensino básico')
ax.set_xticks(x)
ax.set_xticklabels(labels)
ax.legend()


def autolabel(rects):
    # Anexa um valor acima de cada barra, exibindo sua altura
    for rect in rects:
        height = rect.get_height()
        ax.annotate('{}'.format(height),
                    xy=(rect.get_x() + rect.get_width() / 2, height),
                    xytext=(0, 3), # Alinhamento dos valores das alturas das barras
                    textcoords="offset points",
                    ha='center', va='bottom')


autolabel(rects1)
autolabel(rects2)

fig.tight_layout()

plt.show()
