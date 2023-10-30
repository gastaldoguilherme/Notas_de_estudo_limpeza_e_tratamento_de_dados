**Python -  Limpeza e Tratamento de Dados** 
>**Análise Exploratória**    
> Repositório: python - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;

## Análise de Dados com Python, Statistics, Pandas e Seaborn

Neste documento, vamos analisar um conjunto de dados usando Python e as bibliotecas statistics, Pandas e Seaborn. O conjunto de dados usado é denominado "Churn.csv".


### Importar Bibliotecas

Vamos começar importando as bibliotecas necessárias.

```python
import pandas as pd
import seaborn as sns
import statistics as sts
```

### Importar Dados

Agora, importaremos o conjunto de dados "Churn.csv" e visualizaremos suas primeiras linhas.

```python
dataset = pd.read_csv("Churn.csv", sep=";")
dataset.head()
```

Resultado:

&nbsp;

| X0 |   X1  |  X2  |    X3   |  X4  | X4.1 |   X6  |  X7  | X8  | X9 |       X10       | X11 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 619 | RS | Feminino | 42 |  2  |  0 |  1 |  1 |  1 | 10134888.0 |  1  |
| 2 | 608 | SC | Feminino | 41 |  1  | 8380786 |  1 |  0 |  1 | 11254258.0 |  0  |
| 3 | 502 | RS | Feminino | 42 |  8  | 1596608 |  3 |  1 |  0 | 11393157.0 |  1  |
| 4 | 699 | RS | Feminino | 39 |  1  |  0 |  2 |  0 |  0 |  9382663.0 |  0  |
| 5 | 850 | SC | Feminino | 43 |  2  | 12551082 |  1 |  1 |  1 |   790841.0 |  0  |

&nbsp;


### Renomear Colunas

Vamos dar nomes mais descritivos às colunas do conjunto de dados.

```python
dataset.columns = ["ID", "Score", "Estado", "Genero", "Idade", "Patrimonio", "Saldo", "Produtos", "TemCartCredito", "Ativo", "Salario", "Saiu"]

dataset.head()
```

Resultado:
&nbsp;

| ID | Score | Estado |  Genero  | Idade | Patrimonio |     Saldo     | Produtos | TemCartCredito | Ativo |    Salario   | Saiu |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 619 | RS | Feminino | 42 | 2 | 0.0 | 1 | 1 | 1 | 10134888.0 | 1 |
| 2 | 608 | SC | Feminino | 41 | 1 | 8380786.0 | 1 | 0 | 1 | 11254258.0 | 0 |
| 3 | 502 | RS | Feminino | 42 | 8 | 1596608.0 | 3 | 1 | 0 | 11393157.0 | 1 |
| 4 | 699 | RS | Feminino | 39 | 1 | 0.0 | 2 | 0 | 0 | 9382663.0 | 0 |
| 5 | 850 | SC | Feminino | 43 | 2 | 12551082.0 | 1 | 1 | 1 | 790841.0 | 0 |

&nbsp;
## Explorar Dados Categóricos
&nbsp;


### Explorar a coluna "Estado"

Vamos explorar algumas das colunas categóricas do conjunto de dados, começando pelo "Estado".

```python
estado_agrupado = dataset.groupby(['Estado']).size()
estado_agrupado
```

Resultado:
```
Estado
PR    2575
RS    4849
SC    2576
dtype: int64
```

### Gráfico de barras para o Estado
```
estado_agrupado.plot.bar(color='gray')
```

### Explorar a coluna "Genero"

```python
genero_agrupado = dataset.groupby(['Genero']).size()
genero_agrupado
```

Resultado:
```
Genero
Feminino    4543
Masculino   5457
dtype: int64
```

### Gráfico de barras para o Gênero
```
genero_agrupado.plot.bar(color='gray')
```

&nbsp;

## Explorar Dados Numéricos


### Explorar a coluna "Score"


Vamos agora explorar algumas das colunas numéricas, começando pelo "Score".

```python
score_descricao = dataset['Score'].describe()
score_descricao
```

Resultado:
```
count   10000.0
mean      650.53
std        96.65
min       350.0
25%       584.0
50%       652.0
75%       718.0
max       850.0
Name: Score, dtype: float64
```

### Boxplot e distribuição para o Score
```
sns.boxplot(dataset['Score']).set_title('Score')
sns.distplot(dataset['Score']).set_title('Score')
```

### Explorar a coluna "Idade"

```python
idade_descricao = dataset['Idade'].describe()
idade_descricao
```

Resultado:
```
count   10000.0
mean       38.92
std        10.49
min        18.0
25%        32.0
50%        37.0
75%        44.0
max        92.0
Name: Idade, dtype: float64

```
### Boxplot e distribuição para a Idade

```
sns.boxplot(dataset['Idade']).set_title('Idade')
sns.distplot(dataset['Idade']).set_title('Idade')
```

### Explorar a coluna "Saldo"

```python
saldo_descricao = dataset['Saldo'].describe()
saldo_descricao
```

Resultado:
```
count      10000.0
mean       76485.9
std        62397.4
min            0.0
25%            0.0
50%        97198.5
75%       127644.2
max       250898.1
Name: Saldo, dtype: float64
```

### Boxplot e distribuição para o Saldo
```
sns.boxplot(dataset['Saldo']).set_title('Saldo')
sns.distplot(dataset['Saldo']).set_title('Saldo')
```

### Explorar a coluna "Salario"

```python
salario_descricao = dataset['Salario'].describe()
salario_descricao
```

Resultado:
```
count     10000.0
mean    100090.24
std      57510.49
min         11.58
25%      51002.11
50%     100193.92
75%     149388.25
max     199992.48
Name: Salario, dtype: float64
```


### Boxplot e distribuição para o Salario
```
sns.boxplot(dataset['Salario']).set_title('Salario')
sns.distplot(dataset['Salario']).set_title('Salario')
```


&nbsp;

<div align="center">
   
[Retornar ao índice](/README.md)

</div>