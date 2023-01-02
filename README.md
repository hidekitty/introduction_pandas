# introduction_pandas

[Link](https://colab.research.google.com/drive/1v8FzWGB74wwSBpIGaTCe67yvkA3dIx1q?usp=sharing) to google colab.

Import pandas and matplot lib:
```python
import pandas as pd
import matplotlib.pyplot as plt
plt.style.use('seaborn')
```

Upload file on google colab:
```python
from google.colab import files
arq = files.upload()
```

Create dataframe:
```python
df = pd.read_excel('AdventureWorks.xlsx')
df.sample(5)
df.shape
df.dtypes
```

Create new columns on dataframe:
```python
df['Custo'] = df['Custo Unitário'].mul(df['Quantidade'])
df['Lucro'] = df['Valor Venda'] - df['Custo']
df['Tempo Envio'] = (df['Data Envio'] - df['Data Venda']).dt.days
df.head(1)
```

Verify null values:
```python
df.isnull().sum()
```

Generating graphics:
```python
df.groupby('Produto')['Quantidade'].sum().sort_values(ascending=False).plot.barh(title='Lucro x Produto')
plt.xlabel('Receita')
plt.ylabel('Produto');
```

```python
df.groupby(df['Data Venda'].dt.year)['Lucro'].sum().plot.bar(title='Lucro x Ano')
plt.xlabel('Ano')
plt.ylabel('Lucro');
```

Insights filtering specific year:
```python
df_2009 = df.loc[df['Data Venda'].dt.year == 2009]
 
df_2009.groupby(df['Data Venda'].dt.month)['Lucro'].sum().plot(title='Lucro x Mês')
plt.xlabel('Mês')
plt.ylabel('Lucro');

df_2009.groupby('Marca')['Lucro'].sum().plot.bar(title='Lucro x Marca')
plt.xlabel('Lucro')
plt.ylabel('Marca')
plt.xticks(rotation='horizontal');

df_2009.groupby('Classe')['Lucro'].sum().plot.bar(title='Lucro x Classe')
plt.xlabel('Classe')
plt.ylabel('Lucro')
plt.xticks(rotation='horizontal');
```

Insights at delivery time column:
```python
df['Tempo Envio'].describe()
plt.boxplot(df['Tempo Envio']);
plt.hist(df['Tempo Envio'])
df['Tempo Envio'].min()
df['Tempo Envio'].max()
df[df['Tempo Envio'] == 20]
```

Saving dataframe to file:
```python
df.to_csv('df_vendas_novo.csv', index=False)
```
