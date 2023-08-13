# Código para traçar as linhas de tendência no gráfico
import matplotlib.pyplot as plt
import numpy as np

# Carregar os dados do gráfico
data = np.loadtxt('chart_data.csv', delimiter=',')

# Separar os dados em abertura, máxima, mínima e fechamento
open = data[:,0]
high = data[:,1]
low = data[:,2]
close = data[:,3]

# Criar uma figura e um eixo
fig, ax = plt.subplots(figsize=(10,6))

# Plotar os candles usando a função candlestick_ohlc do módulo mplfinance
from mplfinance.original_flavor import candlestick_ohlc
import matplotlib.dates as mdates

# Converter os índices em datas
dates = mdates.datestr2num(['2023-08-07 22:00', '2023-08-07 22:05', '2023-08-07 22:10', '2023-08-07 22:15', '2023-08-07 22:20', '2023-08-07 22:25', '2023-08-07 22:30', '2023-08-07 22:35', '2023-08-07 22:40', '2023-08-07 22:45'])

# Criar um array com as datas e os dados dos candles
ohlc = np.column_stack((dates, open, high, low, close))

# Plotar os candles no eixo
candlestick_ohlc(ax, ohlc, width=0.003, colorup='green', colordown='red')

# Formatar o eixo x com as datas
ax.xaxis.set_major_formatter(mdates.DateFormatter('%H:%M'))

# Traçar as linhas de tendência em vermelho
ax.plot(dates[[0, -1]], [165.5, 162], color='red', linestyle='solid')
ax.plot(dates[[0, -1]], [164.5, 161], color='red', linestyle='solid')

# Adicionar os títulos e legendas
ax.set_title('Gráfico de Monero/Tether Perpetual')
ax.set_xlabel('Hora')
ax.set_ylabel('Preço (USDT)')
ax.legend(['Linha de Tendência'])

# Mostrar o gráfico
plt.show()
