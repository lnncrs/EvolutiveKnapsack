# EvolutiveKnapsack

**Problema da mochila evolutiva**

![UFABC Logo](assets/logotipo-ufabc-extenso.png)

Universidade Federal do ABC - Bacharelado em Ciência e Tecnologia Sistemas Inteligentes 2024/Q3

Lenin Cristi

lenin.cristi@aluno.ufabc.edu.br

## Resumo

**Resumo. Experimento de resolução do problema da mochila usando algoritmos genéticos**

**Abstract. Experiment of Solving the Knapsack Problem Using Genetic Algorithms**

## Objetivos

O objetivo principal deste estudo é investigar a aplicação de algoritmos genéticos (AG) para resolver o problema da mochila, um problema clássico de otimização combinatória.

### O que é o problema da mochila

Para o estudo atual, o problema foi enunciado da seguinte maneira

    Você fará uma viagem a um acampamento durante o final de semana e precisa decidir quais itens levar. Como você só dispõe de uma mochila com capacidade para 15 kg, decidiu incluir somente os itens que maximizem a soma do valor em R$ dos itens, sem ultrapassar o limite de peso

Itens possíveis na mochila

| Nº  | Item                        | Valor (R$) | Peso (kg) |
|-----|-----------------------------|------------|-----------|
| 1   | Barraca                    | 150,00     | 3,5       |
| 2   | Saco de dormir             | 100,00     | 2,0       |
| 3   | Isolante térmico           | 50,00      | 0,5       |
| 4   | Colchão inflável           | 80,00      | 1,0       |
| 5   | Lanterna                   | 30,00      | 0,2       |
| 6   | Kit de primeiros socorros  | 20,00      | 0,5       |
| 7   | Repelente de insetos       | 15,00      | 0,1       |
| 8   | Protetor solar             | 20,00      | 0,2       |
| 9   | Canivete                   | 10,00      | 0,1       |
| 10  | Mapa e bússola             | 25,00      | 0,3       |
| 11  | Garrafa de água            | 15,00      | 1,8       |
| 12  | Filtro de água             | 50,00      | 0,5       |
| 13  | Comida (ração liofilizada) | 50,00      | 3,0       |
| 14  | Fogão de camping           | 70,00      | 1,5       |
| 15  | Botijão de gás             | 30,00      | 1,2       |
| 16  | Prato, talheres e caneca   | 20,00      | 0,5       |
| 17  | Roupas (conjunto)          | 80,00      | 1,5       |
| 18  | Calçados (botas)           | 120,00     | 2,0       |
| 19  | Toalha                     | 20,00      | 0,5       |
| 20  | Kit de higiene pessoal     | 30,00      | 0,5       |

### Requisitos para a solução

- O problema deve ser resolvido implementando um algoritmo genético.

- A representação do problema em cromossomos, a função de ajuste (fitness) e os operadores genéticos (mutação, crossover e o mecanismo de seleção) são parte da solução.

## Metodologia

### Framework utilizado

Neste estudo, utilizamos o **DEAP (Distributed Evolutionary Algorithms in Python)** como framework para implementar o algoritmo genético destinado a resolver o problema da mochila. O DEAP é uma biblioteca de código aberto amplamente utilizada para desenvolvimento de algoritmos evolutivos e heurísticas, fornecendo uma interface robusta e flexível para criar e avaliar populações, realizar seleção, cruzamento e mutação, e monitorar a evolução de soluções.

O DEAP permite a fácil visualização e coleta dos resultados durante a execução do algoritmo, fornecendo ferramentas para monitorar o progresso da evolução e analisar a qualidade das soluções geradas ao longo das gerações.

O seu uso para implementar o algoritmo no contexto deste estudo foi devido a:

- **Facilidade de implementação** A estrutura do DEAP permite uma rápida prototipagem e implementação de algoritmos genéticos com uma interface simples.

- **Flexibilidade** O DEAP oferece diversos operadores genéticos prontos para uso, mas também permite a criação de novos operadores, adaptando o algoritmo a necessidades específicas.

- **Desempenho** O DEAP é otimizado para desempenho, com implementações eficientes de operadores genéticos.

Foi utilizado o repositório do GitHub https://github.com/lnncrs/EvolutiveKnapsack para implementar a solução.

A criação do ambiente para reproduzir o experimento está no **Anexo 1** e pode ser encontrada no README do repositório.

Um primeiro contato com o framework foi feito para solucionar um problema mais simples de OneMax, o código usado é quase integral da documentação do DEAP e foi usado para experimentos iniciais com o framework e validação de ambiente, está no **Anexo 2** e no repositório corresponde ao notebook [OneMax](notebooks/OneMax.ipynb).

### Definições iniciais

#### Lista de itens

A lista de itens possiveis foi modelada contendo ID (ordem do item na lista original), Nome do item, Valor (R$), Peso (kg).

#### Cromossomos

O cromossomo foi criado como uma lista apontando para um tipo de fitness de peso positivo (para maximizar).

#### Função de ajuste (fitness)

A função de avaliação da mochila é relativamente simples, ela soma os pesos dos itens e os valores na mochila e retorna uma penalidade de -1 se o peso for excedido, caso contrário retorna o valor somado como ganho.

#### Operadores genéticos (mutação, crossover e o mecanismo de seleção)

Inicialmente foram definidos os seguintes operadores para a implementação do código

| Parâmetro                    | Nome do parâmetro               | Valor        | Descrição                                                                |
|------------------------------|----------------------------------|--------------|--------------------------------------------------------------------------|
| População inicial             | `population_size`               | 300          | Número de indivíduos na população inicial                                |
| Probabilidade individual de mutação | `individual_probability` | 0.05         | Probabilidade de mutação de cada gene em um indivíduo (bit flip)          |
| Tamanho do torneio            | `tournament_size`               | 3            | Tamanho do torneio, ou número de indivíduos selecionados para reprodução |
| Número de Gerações           | `num_generations`               | 40           | Número de iterações que o algoritmo genético realizará                   |
| Taxa de Crossover            | `crossover_probability`         | 0.5          | Define a probabilidade de que dois indivíduos (pais) se cruzem           |
| Taxa de Mutação              | `mutation_probability`          | 0.2          | Define a probabilidade de que um indivíduo sofra uma mutação             |
| Melhores indivíduos          | `best_individuals`              | 5            | Número de indivíduos selecionados ao final                               |

### Primeira solução

A primeira solução usando os valores determinados foi implementada no código do **Anexo 3** e corresponde ao notebook [KnapSack](notebooks/KnapSack.ipynb).

O melhor indivíduo encontrado nesta solução foi:

| Nome do item                      | Valor (R$) | Peso (kg) |
|------------------------------------|------------|-----------|
| Barraca                            | 150.0      | 3.5       |
| Saco de dormir                     | 100.0      | 2.0       |
| Isolante térmico                   | 50.0       | 0.5       |
| Colchão inflável                   | 80.0       | 1.0       |
| Lanterna                           | 30.0       | 0.2       |
| Kit de primeiros socorros          | 20.0       | 0.5       |
| Repelente de insetos               | 15.0       | 0.1       |
| Protetor solar                     | 20.0       | 0.2       |
| Canivete                           | 10.0       | 0.1       |
| Mapa e bússola                     | 25.0       | 0.3       |
| Filtro de água                     | 50.0       | 0.5       |
| Fogão de camping                   | 70.0       | 1.5       |
| Prato, talheres e caneca           | 20.0       | 0.5       |
| Roupas (conjunto)                  | 80.0       | 1.5       |
| Calçados (botas)                   | 120.0      | 2.0       |
| Kit de higiene pessoal             | 30.0       | 0.5       |

Valor total: R$870.00<br/>
Peso total: 14.90kg<br/>
Tempo de execução (evolução somente): 0.2194 segundos

### Busca de outras soluções

Foi implementado um código separado que simula um GridSearch para encontrar melhores parâmetros para o algoritmo evolutivo, o código está no **Anexo 4** e corresponde ao notebook [KnapSackGrid](notebooks/KnapSackGrid.ipynb).

Este mecanismo de busca por melhores parâmetros utilizou as seguintes variações de busca

| Parâmetro             | Valores utilizados             |
|-----------------------|--------------------------------|
| population_size       | 50, 100, 200                   |
| num_generations       | 50, 100, 200                   |
| crossover_probability | 0.5, 0.7, 0.9                  |
| mutation_probability  | 0.1, 0.2, 0.3                  |
| tournament_size       | 2, 5, 10                       |
| select_method         | "selTournament", "selRoulette" |

E encontrou os seguintes parâmetros

```text
Melhores parâmetros encontrados: {'population_size': 50, 'num_generations': 50, 'crossover_probability': 0.5, 'mutation_probability': 0.2, 'tournament_size': 10, 'select_method': 'selTournament'}
```

Tempo de execução (evolução somente): 207.2722 segundos

### Implementação da solução alternativa

Os parâmetros encontrados na busca foram utilizados num código identico ao da solução original, o código está no **Anexo 5** e corresponde ao notebook [KnapSackGridBest](notebooks/KnapSackGridBest.ipynb).

Com o seguinte indivíduo encontrado:

| Nome do item                     | Valor (R$) | Peso (kg) |
|-----------------------------------|------------|-----------|
| Barraca                           | 150.0      | 3.5       |
| Saco de dormir                    | 100.0      | 2.0       |
| Isolante térmico                  | 50.0       | 0.5       |
| Colchão inflável                  | 80.0       | 1.0       |
| Lanterna                          | 30.0       | 0.2       |
| Kit de primeiros socorros         | 20.0       | 0.5       |
| Repelente de insetos              | 15.0       | 0.1       |
| Protetor solar                    | 20.0       | 0.2       |
| Canivete                          | 10.0       | 0.1       |
| Mapa e bússola                    | 25.0       | 0.3       |
| Filtro de água                    | 50.0       | 0.5       |
| Fogão de camping                  | 70.0       | 1.5       |
| Prato, talheres e caneca          | 20.0       | 0.5       |
| Roupas (conjunto)                 | 80.0       | 1.5       |
| Calçados (botas)                  | 120.0      | 2.0       |
| Kit de higiene pessoal            | 30.0       | 0.5       |

Valor total: R$870.00<br/>
Peso total: 14.90kg<br/>
Tempo de execução (evolução somente): 0.0477 segundos

## Discussão

A primeira solução com os valores iniciais de disparo encontrou um indivíduo com características e lista de itens idênticas ao do individuo encontrado pela busca de parâmetros, **Valor total: R$870.00 / Peso total: 14.90kg**.

A diferença ficou pelo tempo de busca, na solução inicial foram **0.2194 segundos** e na solução alternativa encontrada por busca foram **0.0477 segundos**, mas é importante notar que o tempo de busca por parâmetros ótimos em si foi de **207.2722 segundos** o que não justifica a sua utilização, mas reforça que parâmetros ponderados de disparo podem ser capazes de gerar resultados ótimos neste tipo de algoritmo.

A busca de parâmetros parece ter encontrado um caminho de convergência ótimo, pois a solução ótima em si foi encontrada já com parâmetros iniciais mais abrangentes.

Mais testes são necessários para sacramentar que técnicas semelhantes ao GridSearch bem caras computacionalmente e bem comum em determinados algoritmos de aprendizado são desnecessárias aqui.

## Anexo 1: Como gerar o ambiente para reproduzir os experimentos

Vamos mostrar a seguir um exemplo de como criar o ambiente necessário usando o gerenciador de ambientes e pacotes Anaconda como base com o arquivo environments.yml neste repositório.

### Instalando o conda

Utilize a referência oficial Anaconda para instalar o miniconda no seu ambiente https://docs.anaconda.com/miniconda/install/

### Criando o ambiente

Para criar o ambiente com os pacotes base a partir do arquivo

```bash
conda env create -f environment.yml
```

### Ativando o ambiente

Após a instalação do ambiente base, ative ele com

```bash
conda activate evol
```

### DEAP

Abaixo um comando de como instalar a biblioteca

```bash
pip install deap
```

## Anexo 2 - OneMax

Código somente, para a versão integral visite o notebook

```python
import random
from deap import creator, base, tools, algorithms

creator.create("FitnessMax", base.Fitness, weights=(1.0,))
creator.create("Individual", list, fitness=creator.FitnessMax)

toolbox = base.Toolbox()

toolbox.register("attr_bool", random.randint, 0, 1)
toolbox.register("individual", tools.initRepeat, creator.Individual, toolbox.attr_bool, n=10)
toolbox.register("population", tools.initRepeat, list, toolbox.individual)

def evalOneMax(individual):
    return sum(individual),

toolbox.register("evaluate", evalOneMax)
toolbox.register("mate", tools.cxTwoPoint)
toolbox.register("mutate", tools.mutFlipBit, indpb=0.05)
toolbox.register("select", tools.selTournament, tournsize=3)

population = toolbox.population(n=300)

NGEN=40
for gen in range(NGEN):
    offspring = algorithms.varAnd(population, toolbox, cxpb=0.5, mutpb=0.1)
    fits = toolbox.map(toolbox.evaluate, offspring)
    for fit, ind in zip(fits, offspring):
        ind.fitness.values = fit
    population = toolbox.select(offspring, k=len(population))

top10 = tools.selBest(population, k=10)

top10
```

## Anexo 3 - KnapSack

Código somente, para a versão integral visite o notebook

```python
import random
import time
import pandas as pd
from deap import creator, base, tools, algorithms

# Lista de itens: ID, Nome do item, Valor (R$), Peso (kg)
items = [
    (1, "Barraca", 150.0, 3.5),
    (2, "Saco de dormir", 100.0, 2.0),
    (3, "Isolante térmico", 50.0, 0.5),
    (4, "Colchão inflável", 80.0, 1.0),
    (5, "Lanterna", 30.0, 0.2),
    (6, "Kit de primeiros socorros", 20.0, 0.5),
    (7, "Repelente de insetos", 15.0, 0.1),
    (8, "Protetor solar", 20.0, 0.2),
    (9, "Canivete", 10.0, 0.1),
    (10, "Mapa e bússola", 25.0, 0.3),
    (11, "Garrafa de água", 15.0, 1.8),
    (12, "Filtro de água", 50.0, 0.5),
    (13, "Comida (ração liofilizada)", 50.0, 3.0),
    (14, "Fogão de camping", 70.0, 1.5),
    (15, "Botijão de gás", 30.0, 1.2),
    (16, "Prato, talheres e caneca", 20.0, 0.5),
    (17, "Roupas (conjunto)", 80.0, 1.5),
    (18, "Calçados (botas)", 120.0, 2.0),
    (19, "Toalha", 20.0, 0.5),
    (20, "Kit de higiene pessoal", 30.0, 0.5)
]

# Capacidade máxima da mochila em kg
max_weight = 15.0

population_size = 300
individual_probability = 0.05
tournament_size = 3
num_generations = 40
crossover_probability = 0.5
mutation_probability = 0.2
best_individuals = 5

def evalKnapsack(individual):
    total_value = 0.0  # Valor total da mochila
    total_weight = 0.0  # Peso total da mochila

    for i, selected in enumerate(individual):
        if selected:  # Se o item foi selecionado
            total_value += items[i][2]  # Soma o valor do item ao total
            total_weight += items[i][3]  # Soma o peso do item ao total

    # Penaliza soluções que ultrapassam o peso máximo
    if total_weight > max_weight:
        return -1,  # Penalidade
    return total_value, # Retorna o valor total como fitness para soluções válidas

# Cria um tipo de "fitness" para maximizar um único valor (peso positivo indica maximização).
creator.create("FitnessMax", base.Fitness, weights=(1.0,))

# Define um indivíduo como uma lista que possui um fitness do tipo "FitnessMax".
creator.create("Individual", list, fitness=creator.FitnessMax)

# Caixa de ferramentas para registrar funções que geram e operam sobre os indivíduos.
toolbox = base.Toolbox()

# Representação binária dos itens (0 ou 1 para incluir ou não incluir)
toolbox.register("attr_bool", random.randint, 0, 1)

# Registra um indivíduo como uma lista de genes de comprimento igual ao número de itens.
toolbox.register("individual", tools.initRepeat, creator.Individual, toolbox.attr_bool, n=len(items))

# Registra uma população como uma lista de indivíduos.
toolbox.register("population", tools.initRepeat, list, toolbox.individual)

# Registra a função de avaliação no toolbox.
toolbox.register("evaluate", evalKnapsack)

# Registra o operador de crossover de dois pontos no toolbox.
toolbox.register("mate", tools.cxTwoPoint)

# Registra o operador de mutação.
toolbox.register("mutate", tools.mutFlipBit, indpb=individual_probability)

# Registra o operador de seleção por torneio.
toolbox.register("select", tools.selTournament, tournsize=tournament_size)

# Gera a população inicial
population = toolbox.population(n=population_size)

# Registra o tempo de início
start_time = time.time()

# Execução do algoritmo
for gen in range(num_generations):

    # Gera novos indivíduos (offspring) a partir da população atual aplicando crossover e mutação.
    offspring = algorithms.varAnd(population, toolbox, cxpb=crossover_probability, mutpb=mutation_probability)

    # Calcula os valores de fitness para cada indivíduo da nova geração.
    fits = toolbox.map(toolbox.evaluate, offspring)
    for fit, ind in zip(fits, offspring):
        ind.fitness.values = fit  # Atribui o fitness calculado aos indivíduos.

    population = toolbox.select(offspring, k=len(population))

# Seleciona n melhores indivíduos.
top_individuals = tools.selBest(population, k=best_individuals)

# Registra o tempo de término
end_time = time.time()

# Calcula o tempo total de execução
execution_time = end_time - start_time

# Seleciona o melhor indivíduo.
best_individual = top_individuals[0]

# Identifica os itens selecionados no melhor indivíduo.
selected_items = [items[i] for i in range(len(best_individual)) if best_individual[i] == 1]

# Criação do DataFrame com os itens selecionados pelo melhor indivíduo
selected_items_data = [{
    'Nome do item': item[1],
    'Valor (R$)': item[2],
    'Peso (kg)': item[3]
} for item in selected_items]

df_selected_items = pd.DataFrame(selected_items_data)

print("Itens selecionados:")
df_selected_items.head(len(items))

# Imprime o valor total dos itens na mochila.
print(f"Valor total: R${sum(item[2] for item in selected_items):.2f}")

# Imprime o peso total dos itens na mochila.
print(f"Peso total: {sum(item[3] for item in selected_items):.2f}kg")

# Imprime o tempo de execução
print(f"Tempo de execução (evolução somente): {execution_time:.4f} segundos")
```

## Anexo 4 - KnapSackGrid

Código somente, para a versão integral visite o notebook

```python
import random
import time
import pandas as pd
from deap import creator, base, tools, algorithms

# Lista de itens: ID, Nome do item, Valor (R$), Peso (kg)
items = [
    (1, "Barraca", 150.0, 3.5),
    (2, "Saco de dormir", 100.0, 2.0),
    (3, "Isolante térmico", 50.0, 0.5),
    (4, "Colchão inflável", 80.0, 1.0),
    (5, "Lanterna", 30.0, 0.2),
    (6, "Kit de primeiros socorros", 20.0, 0.5),
    (7, "Repelente de insetos", 15.0, 0.1),
    (8, "Protetor solar", 20.0, 0.2),
    (9, "Canivete", 10.0, 0.1),
    (10, "Mapa e bússola", 25.0, 0.3),
    (11, "Garrafa de água", 15.0, 1.8),
    (12, "Filtro de água", 50.0, 0.5),
    (13, "Comida (ração liofilizada)", 50.0, 3.0),
    (14, "Fogão de camping", 70.0, 1.5),
    (15, "Botijão de gás", 30.0, 1.2),
    (16, "Prato, talheres e caneca", 20.0, 0.5),
    (17, "Roupas (conjunto)", 80.0, 1.5),
    (18, "Calçados (botas)", 120.0, 2.0),
    (19, "Toalha", 20.0, 0.5),
    (20, "Kit de higiene pessoal", 30.0, 0.5),
]

# Capacidade máxima da mochila em kg
max_weight = 15.0

# Definir os parâmetros para o grid search
param_grid = {
    "population_size": [50, 100, 200],
    "num_generations": [50, 100, 200],
    "crossover_probability": [0.5, 0.7, 0.9],
    "mutation_probability": [0.1, 0.2, 0.3],
    "tournament_size": [2, 5, 10],
    "select_method": ["selTournament", "selRoulette"],
}


# Função para rodar o algoritmo genético com uma combinação de parâmetros
def run_genetic_algorithm(params):

    population_size = params["population_size"]
    num_generations = params["num_generations"]
    crossover_probability = params["crossover_probability"]
    mutation_probability = params["mutation_probability"]
    tournament_size = params["tournament_size"]
    select_method = params["select_method"]

    creator.create("FitnessMax", base.Fitness, weights=(1.0,))
    creator.create("Individual", list, fitness=creator.FitnessMax)

    toolbox = base.Toolbox()
    toolbox.register("attr_bool", random.randint, 0, 1)
    toolbox.register(
        "individual",
        tools.initRepeat,
        creator.Individual,
        toolbox.attr_bool,
        n=len(items),
    )
    toolbox.register("population", tools.initRepeat, list, toolbox.individual)

    def eval_knapsack(individual):
        # Cálculo do valor e peso total dos itens selecionados
        value = sum(items[i][2] for i in range(len(individual)) if individual[i] == 1)
        weight = sum(items[i][3] for i in range(len(individual)) if individual[i] == 1)
        if weight > 15:  # Respeitar o limite de peso
            return (0,)
        return (value,)

    toolbox.register("evaluate", eval_knapsack)
    toolbox.register("mate", tools.cxTwoPoint)
    toolbox.register("mutate", tools.mutFlipBit, indpb=mutation_probability)

    # toolbox.register("select", getattr(tools, select_method), tournsize=tournsize)

    # Escolher a função de seleção com base no método escolhido
    if select_method == "selTournament":
        toolbox.register("select", tools.selTournament, tournsize=tournament_size)
    elif select_method == "selRoulette":
        toolbox.register("select", tools.selRoulette)
    else:
        raise ValueError("Método de seleção desconhecido!")

    population = toolbox.population(n=population_size)

    for gen in range(num_generations):
        offspring = algorithms.varAnd(population, toolbox, cxpb=crossover_probability, mutpb=mutation_probability)
        fits = toolbox.map(toolbox.evaluate, offspring)
        for fit, ind in zip(fits, offspring):
            ind.fitness.values = fit
        population = toolbox.select(offspring, k=len(population))

    top_individual = tools.selBest(population, 1)[0]
    return top_individual.fitness.values[0]


# Rodar o grid search manualmente
best_score = -1
best_params = {}

# Registra o tempo de início
start_time = time.time()

for population_size in param_grid["population_size"]:
    for NGEN in param_grid["num_generations"]:
        for CXPB in param_grid["crossover_probability"]:
            for MUTPB in param_grid["mutation_probability"]:
                for tournsize in param_grid["tournament_size"]:
                    for select_method in param_grid["select_method"]:
                        params = {
                            "population_size": population_size,
                            "num_generations": NGEN,
                            "crossover_probability": CXPB,
                            "mutation_probability": MUTPB,
                            "tournament_size": tournsize,
                            "select_method": select_method,
                        }
                        score = run_genetic_algorithm(params)
                        print(f"Parâmetros: {params} => Melhor valor: {score}")

                        if score > best_score:
                            best_score = score
                            best_params = params

# Registra o tempo de término
end_time = time.time()

# Calcula o tempo total de execução
execution_time = end_time - start_time

# Imprime os melhores parâmetros encontrados
print("Melhores parâmetros encontrados:", best_params)

# Imprime o tempo de execução
print(f"Tempo de execução (evolução somente): {execution_time:.4f} segundos")
```

## Anexo 5 - KnapSackGridBest

Código somente, para a versão integral visite o notebook

```python
import random
import time
import pandas as pd
from deap import creator, base, tools, algorithms

# Lista de itens: ID, Nome do item, Valor (R$), Peso (kg)
items = [
    (1, "Barraca", 150.0, 3.5),
    (2, "Saco de dormir", 100.0, 2.0),
    (3, "Isolante térmico", 50.0, 0.5),
    (4, "Colchão inflável", 80.0, 1.0),
    (5, "Lanterna", 30.0, 0.2),
    (6, "Kit de primeiros socorros", 20.0, 0.5),
    (7, "Repelente de insetos", 15.0, 0.1),
    (8, "Protetor solar", 20.0, 0.2),
    (9, "Canivete", 10.0, 0.1),
    (10, "Mapa e bússola", 25.0, 0.3),
    (11, "Garrafa de água", 15.0, 1.8),
    (12, "Filtro de água", 50.0, 0.5),
    (13, "Comida (ração liofilizada)", 50.0, 3.0),
    (14, "Fogão de camping", 70.0, 1.5),
    (15, "Botijão de gás", 30.0, 1.2),
    (16, "Prato, talheres e caneca", 20.0, 0.5),
    (17, "Roupas (conjunto)", 80.0, 1.5),
    (18, "Calçados (botas)", 120.0, 2.0),
    (19, "Toalha", 20.0, 0.5),
    (20, "Kit de higiene pessoal", 30.0, 0.5)
]

# Capacidade máxima da mochila em kg
max_weight = 15.0

population_size = 50
individual_probability = 0.05
tournament_size = 10
num_generations = 50
crossover_probability = 0.5
mutation_probability = 0.2
best_individuals = 5

def evalKnapsack(individual):
    total_value = 0.0  # Valor total da mochila
    total_weight = 0.0  # Peso total da mochila

    for i, selected in enumerate(individual):
        if selected:  # Se o item foi selecionado
            total_value += items[i][2]  # Soma o valor do item ao total
            total_weight += items[i][3]  # Soma o peso do item ao total

    # Penaliza soluções que ultrapassam o peso máximo
    if total_weight > max_weight:
        return -1,  # Penalidade
    return total_value, # Retorna o valor total como fitness para soluções válidas

# Cria um tipo de "fitness" para maximizar um único valor (peso positivo indica maximização).
creator.create("FitnessMax", base.Fitness, weights=(1.0,))

# Define um indivíduo como uma lista que possui um fitness do tipo "FitnessMax".
creator.create("Individual", list, fitness=creator.FitnessMax)

# Caixa de ferramentas para registrar funções que geram e operam sobre os indivíduos.
toolbox = base.Toolbox()

# Representação binária dos itens (0 ou 1 para incluir ou não incluir)
toolbox.register("attr_bool", random.randint, 0, 1)

# Registra um indivíduo como uma lista de genes de comprimento igual ao número de itens.
toolbox.register("individual", tools.initRepeat, creator.Individual, toolbox.attr_bool, n=len(items))

# Registra uma população como uma lista de indivíduos.
toolbox.register("population", tools.initRepeat, list, toolbox.individual)

# Registra a função de avaliação no toolbox.
toolbox.register("evaluate", evalKnapsack)

# Registra o operador de crossover de dois pontos no toolbox.
toolbox.register("mate", tools.cxTwoPoint)

# Registra o operador de mutação.
toolbox.register("mutate", tools.mutFlipBit, indpb=individual_probability)

# Registra o operador de seleção por torneio.
toolbox.register("select", tools.selTournament, tournsize=tournament_size)

# Gera a população inicial
population = toolbox.population(n=population_size)

# Registra o tempo de início
start_time = time.time()

# Execução do algoritmo
for gen in range(num_generations):

    # Gera novos indivíduos (offspring) a partir da população atual aplicando crossover e mutação.
    offspring = algorithms.varAnd(population, toolbox, cxpb=crossover_probability, mutpb=mutation_probability)

    # Calcula os valores de fitness para cada indivíduo da nova geração.
    fits = toolbox.map(toolbox.evaluate, offspring)
    for fit, ind in zip(fits, offspring):
        ind.fitness.values = fit  # Atribui o fitness calculado aos indivíduos.

    population = toolbox.select(offspring, k=len(population))

# Seleciona n melhores indivíduos.
top_individuals = tools.selBest(population, k=best_individuals)

# Registra o tempo de término
end_time = time.time()

# Calcula o tempo total de execução
execution_time = end_time - start_time

# Seleciona o melhor indivíduo.
best_individual = top_individuals[0]

# Identifica os itens selecionados no melhor indivíduo.
selected_items = [items[i] for i in range(len(best_individual)) if best_individual[i] == 1]

# Criação do DataFrame com os itens selecionados pelo melhor indivíduo
selected_items_data = [{
    'Nome do item': item[1],
    'Valor (R$)': item[2],
    'Peso (kg)': item[3]
} for item in selected_items]

df_selected_items = pd.DataFrame(selected_items_data)

print("Itens selecionados:")
df_selected_items.head(len(items))

# Imprime o valor total dos itens na mochila.
print(f"Valor total: R${sum(item[2] for item in selected_items):.2f}")

# Imprime o peso total dos itens na mochila.
print(f"Peso total: {sum(item[3] for item in selected_items):.2f}kg")

# Imprime o tempo de execução
print(f"Tempo de execução (evolução somente): {execution_time:.4f} segundos")
```

## Referências

DEAP - Distributed Evolutionary Algorithms in Python<br>
https://github.com/DEAP/deap

François-Michel De Rainville, Félix-Antoine Fortin, Marc-André Gardner, Marc Parizeau and Christian Gagné, "DEAP -- Enabling Nimbler Evolutions", SIGEVOlution, vol. 6, no 2, pp. 17-26, February 2014.<br>
http://vision.gel.ulaval.ca/~cgagne/pubs/sigevolution2014.pdf

Félix-Antoine Fortin, François-Michel De Rainville, Marc-André Gardner, Marc Parizeau and Christian Gagné, "DEAP: Evolutionary Algorithms Made Easy", Journal of Machine Learning Research, vol. 13, pp. 2171-2175, jul 2012.<br>
https://jmlr.csail.mit.edu/papers/v13/fortin12a.html

François-Michel De Rainville, Félix-Antoine Fortin, Marc-André Gardner, Marc Parizeau and Christian Gagné, "DEAP: A Python Framework for Evolutionary Algorithms", in !EvoSoft Workshop, Companion proc. of the Genetic and Evolutionary Computation Conference (GECCO 2012), July 07-11 2012.<br>
http://vision.gel.ulaval.ca/~cgagne/pubs/deap-gecco-2012.pdf

DEAP 1.4.1 documentation » Examples » One Max Problem<br>
https://deap.readthedocs.io/en/master/examples/ga_onemax.html

DEAP 1.4.1 documentation » Examples » Knapsack Problem: Inheriting from Set<br>
https://deap.readthedocs.io/en/master/examples/ga_knapsack.html

___

CMCC - Universidade Federal do ABC (UFABC) - Santo André - SP - Brasil
