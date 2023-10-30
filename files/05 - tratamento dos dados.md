**Python -  Limpeza e Tratamento de Dados** 
>**Tratamento dos Dados**    
> Repositório: python - Fundamentos  
> GitHub: @gastaldoguilherme
&nbsp;


## Tratamento dos Dados
&nbsp;

| ID | Score | Estado |  Genero  | Idade | Patrimonio |     Saldo     | Produtos | TemCartCredito | Ativo |    Salario   | Saiu |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 619 | RS | Feminino | 42 | 2 | 0.0 | 1 | 1 | 1 | 10134888.0 | 1 |
| 2 | 608 | SC | Feminino | 41 | 1 | 8380786.0 | 1 | 0 | 1 | 11254258.0 | 0 |
| 3 | 502 | RS | Feminino | 42 | 8 | 1596608.0 | 3 | 1 | 0 | 11393157.0 | 1 |
| 4 | 699 | RS | Feminino | 39 | 1 | 0.0 | 2 | 0 | 0 | 9382663.0 | 0 |
| 5 | 850 | SC | Feminino | 43 | 2 | 12551082.0 | 1 | 1 | 1 | 790841.0 | 0 |

&nbsp;




### Tratamento de Dados e Análise Exploratória

Nesta seção, realizaremos o tratamento de dados e análise exploratória no conjunto de dados.

#### Contagem de Valores NaN

Vamos começar contando quantos valores ausentes (NaN) existem no conjunto de dados.

```python
dataset.isnull().sum()
```

**Resultado**:
Isso mostrará a contagem de valores NaN em cada coluna do conjunto de dados.

#### Tratamento da Coluna "Salario"

Vamos lidar com a coluna "Salario". Primeiro, calculamos estatísticas descritivas.

```python
dataset['Salario'].describe()
```

**Resultado**:
Isso exibirá estatísticas descritivas, incluindo a mediana dos salários.

Agora, calculamos a mediana dos salários.

```python
mediana = sts.median(dataset['Salario'])
mediana
```

**Resultado**:
Isso mostrará o valor da mediana calculada dos salários.

Substituímos os valores ausentes (NaN) na coluna "Salario" pela mediana.

```python
dataset['Salario'].fillna(mediana, inplace=True)
```

Verificamos novamente se não há mais valores ausentes na coluna "Salario".

```python
dataset['Salario'].isnull().sum()
```

**Resultado**:
Isso deve retornar 0, indicando que não há mais valores ausentes na coluna "Salario".

#### Tratamento da Coluna "Genero"

Agora, vamos lidar com a coluna "Genero". Primeiro, agrupamos os valores e contamos suas ocorrências.

```python
agrupado = dataset.groupby(['Genero']).size()
agrupado
```

**Resultado**:
Isso exibirá a contagem de valores únicos na coluna "Genero".

Em seguida, verificamos o total de valores ausentes (NaN) na coluna "Genero".

```python
dataset['Genero'].isnull().sum()
```

**Resultado**:
Isso mostrará a contagem de valores ausentes na coluna "Genero".

Preenchemos os valores ausentes na coluna "Genero" com "Masculino" (a moda).

```python
dataset['Genero'].fillna('Masculino', inplace=True)
```

Verificamos novamente se não há mais valores ausentes na coluna "Genero".

```python
dataset['Genero'].isnull().sum()
```

**Resultado**:
Isso deve retornar 0, indicando que não há mais valores ausentes na coluna "Genero".

Em seguida, padronizamos os valores da coluna "Genero" de acordo com o domínio, substituindo "M" por "Masculino" e "Fem" ou "F" por "Feminino".

```python
dataset.loc[dataset['Genero'] == 'M', 'Genero'] = "Masculino"
dataset.loc[dataset['Genero'].isin(['Fem', 'F']), 'Genero'] = "Feminino"
```

Visualizamos o resultado do agrupamento da coluna "Genero novamente.

```python
agrupado = dataset.groupby(['Genero']).size()
agrupado
```

#### Tratamento de Idades Fora do Domínio

Agora, focamos na coluna "Idade". Começamos calculando estatísticas descritivas.

```python
dataset['Idade'].describe()
```

**Resultado**:
Isso exibirá estatísticas descritivas da coluna "Idade".

Em seguida, identificamos as idades que estão fora do domínio (menos de 0 ou mais de 120).

```python
dataset.loc[(dataset['Idade'] < 0) | (dataset['Idade'] > 120)]
```

**Resultado**:
Isso retornará as linhas do conjunto de dados em que as idades estão fora do domínio.

Calculamos a mediana das idades.

```python
mediana = sts.median(dataset['Idade'])
mediana
```

**Resultado**:
Isso mostrará o valor da mediana calculada das idades.

Substituímos as idades fora do domínio pela mediana.

```python
dataset.loc[(dataset['Idade'] < 0) | (dataset['Idade'] > 120), 'Idade'] = mediana
```

Verificamos se ainda existem idades fora do domínio.

```python
dataset.loc[(dataset['Idade'] < 0) | (dataset['Idade'] > 120)]
```

#### Tratamento de Dados Duplicados

Agora, lidamos com dados duplicados. Começamos identificando duplicatas com base na coluna "Id".

```python
dataset[dataset.duplicated(['Id'], keep=False)]
```

**Resultado**:
Isso retornará as linhas duplicadas com base no valor da coluna "Id".

Em seguida, excluímos as duplicatas, mantendo apenas a primeira ocorrência.

```python
dataset.drop_duplicates(subset="Id", keep='first', inplace=True)
```

Verificamos se ainda existem duplicatas.

```python
dataset[dataset.duplicated(['Id'], keep=False)]
```

**Resultado**:
Isso deve retornar um DataFrame vazio, indicando que não há mais duplicatas com base na coluna "Id".

#### Tratamento de Estados Fora do Domínio

Por fim, lidamos com a coluna "Estado". Começamos agrupando os valores e contando suas ocorrências.

```python
agrupado = dataset.groupby(['Estado']).size()
agrupado
```

**Resultado**:
Isso exibirá a contagem de valores únicos na coluna "Estado".

A seguir, atribuímos "RS" aos estados "RP", "SP" e "TD".

```python
dataset.loc[dataset['Estado'].isin(['RP', 'SP', 'TD']), 'Estado'] = "RS"
```

Verificamos o resultado novamente.

```python
agrupado = dataset.groupby(['Estado']).size()
agrupado
```

#### Tratamento de Outliers em Salários

Por fim, identificamos outliers na coluna "Salario" com base em 2 desvios padrão.

```python
desv = sts.stdev(dataset['Salario'])
desv
```

**Resultado**:
Isso mostrará o valor do desvio padrão dos salários.

Definimos um padrão de que os valores maiores ou iguais a 2 desvios padrão são considerados outliers.

```python
dataset.loc[dataset['Salario'] >= 2 * desv]
```

A seguir, calculamos a mediana dos salários.

```python
mediana = sts.median(dataset['Salario'])
mediana
```

**Resultado**:
Isso exibirá o valor da mediana calculada dos salários.

Substituímos os outliers pela mediana.

```python


dataset.loc[dataset['Salario'] >= 2 * desv, 'Salario'] = mediana
```

Verificamos se ainda existem outliers.

```python
dataset.loc[dataset['Salario'] >= 2 * desv]
```

### Visualização dos Dados

Por fim, exibimos as primeiras linhas do conjunto de dados.

```python
dataset.head()
```

**Resultado**:
Isso mostrará as primeiras linhas do conjunto de dados após todas as transformações e tratamentos realizados.


## Observação sobre os dados faltantes:

Substituir dados faltantes categóricos pela moda e dados faltantes numéricos pela mediana é uma prática comum no tratamento de dados, mas a escolha entre essas estratégias pode variar dependendo do contexto do problema e dos dados em questão. Aqui estão algumas razões pelas quais essas estratégias são frequentemente usadas:

**Substituir Dados Faltantes Categóricos Pela Moda:**

1. **Preservação da Tendência Central:** A moda representa o valor mais frequente em um conjunto de dados categóricos. Substituir dados faltantes pela moda ajuda a preservar a tendência central dos dados, ou seja, mantém a distribuição de valores categóricos o mais próxima possível da distribuição original.

2. **Categorias Dominantes:** Em muitos casos, a moda é uma categoria dominante que reflete a preferência da maioria. Substituir dados faltantes pela moda tende a atribuir valores que são mais representativos da maioria dos casos.

3. **Simplicidade:** A moda é fácil de calcular e entender. Ela não requer cálculos complexos e é uma abordagem simples e direta para lidar com dados categóricos ausentes.

**Substituir Dados Faltantes Numéricos Pela Mediana:**

1. **Robustez a Outliers:** A mediana é uma medida de tendência central robusta que não é sensível a valores extremos (outliers). Substituir dados numéricos faltantes pela mediana ajuda a minimizar o impacto de valores atípicos na imputação dos dados.

2. **Preservação da Ordem dos Dados:** A mediana é o valor que divide os dados ordenados ao meio. Ela preserva a ordem dos dados, o que é importante quando se trata de dados numéricos. Substituir dados faltantes pela mediana ajuda a manter a estrutura da distribuição dos dados.

3. **Adequação para Distribuições Não Normais:** Enquanto a média é sensível a distribuições não normais, a mediana é uma escolha adequada, independentemente da distribuição dos dados. Isso a torna uma escolha robusta para dados numéricos.

4. **Minimização de Viés:** A mediana não é afetada por valores extremos, ao contrário da média. Isso ajuda a minimizar o viés introduzido pela imputação de dados faltantes em distribuições com valores atípicos.

É importante notar que a escolha entre moda e mediana para substituir dados faltantes depende da natureza dos dados e das suposições que fazemos sobre o problema em questão. Em alguns casos, pode ser apropriado explorar outras estratégias de imputação de dados, como regressão, imputação por valor mais próximo, ou até mesmo métodos mais avançados, como k-vizinhos mais próximos ou modelos de aprendizado de máquina. A escolha da estratégia de imputação deve ser guiada pela compreensão dos dados e dos objetivos da análise.


&nbsp;

<div align="center">
   
[Retornar ao índice](/README.md)

</div>