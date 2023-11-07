# Atividade Estrutura de Dados - Algoritmos de ordenação
## Aluno: Thiago Rodrigues Cruz Justino (20220007276)
## Professor: Gilberto Farias de Sousa Filho

A atividade consiste em fazer os seguintes algoritmos de ordenação: 
- Selection sort
- Insertion sort
- MergeSort

Além disso, deve-se observar e comparar o tempo de execução de cada algoritmo.

## Adaptação para abrir os arquivos e o usuário selecionar o arquivo que deseja testar:
Bom, para fazer um aplicação que possa ser executável a qualquer momento sem precisar baixar nada, optei por armazenar as instâncias de teste no Github. Como apresentado no seguinte código:

```python
import requests
# Solicita ao usuário o número de instâncias e o exemplo desejado
n = input("Digite o número de instâncias desejado (Opções: 1000, 10000, 100000): ")
p = input("Selecione um dos exemplos (Opções: 1, 2, 3 ou 4): ")
array = []
# Verifique se as entradas são válidas
opcoes_n = ['1000', '10000', '100000']
opcoes_p = ['1', '2', '3', '4']

if n not in opcoes_n or p not in opcoes_p:
    print("Entrada inválida. Certifique-se de escolher opções válidas.")

else:
  # URL direta do arquivo no GitHub
  url = f'https://raw.githubusercontent.com/Thiagorcj/Atividade_ED3/main/instancias-num/num.{n}.{p}.in'

  # Faz uma solicitação para obter o conteúdo do arquivo
  response = requests.get(url)

  # Verifica se a solicitação foi bem-sucedida
  if response.status_code == 200:
      # O conteúdo do arquivo estará em response.text
      conteudo = response.text

      # Divida o conteúdo em linhas
      linhas = conteudo.splitlines()

      # Itera sobre as linhas
      for linha in linhas:
          array.append(int(linha))
  else:
      print('Falha ao obter o arquivo do GitHub. Código de status:', response.status_code)
```
```bash
Digite o número de instâncias desejado (Opções: 1000, 10000, 100000): 1000
Selecione um dos exemplos (Opções: 1, 2, 3 ou 4): 1
```
## Algoritmos de Ordenação:
### Selection Sort:
#### Explicação do código
O código começa com um loop "for" que percorre todos os elementos do array, exceto o último, pois não há necessidade de compará-lo, já que não há elementos à direita. Neste primeiro "for", é armazenado o valor inicial e, em seguida, todos os valores à esquerda são comparados através de outro loop, com o objetivo de identificar o menor valor à direita. Após percorrer todos os valores à direita do valor inicial, o valor inicial é trocado pelo menor valor encontrado. Desta forma, os elementos da posição 0 até n-1 são gradualmente substituídos pelos valores menores à direita, resultando na ordenação crescente do array com um algoritmo de complexidade O(N²).
#### Tempo de execução do código:
- Executando 1000 elementos: Em média aproximadamente 0,05 segundos.
- Executando 10000 elementos: Em média aproximadamente 5,7 segundos.
- Executando 100000 elementos: Em média aproximadamente 537 segundos.
```python
import time
import copy

def SelectionSort(arr):
  array = copy.copy(arr)   # Prefiri não modificar diretamente o array, mas criar uma cópia
  # Registra o tempo de início
  start_time = time.time()
  # Algoritmo
  for i in range(len(array)-1):
    inicial = array[i]
    indice_menor = i

    for j in range(i+1,len(array)):
      if array[j]<array[indice_menor]:
        indice_menor = j

    array[i] = array[indice_menor]
    array[indice_menor] = inicial
  # Registra o tempo de término
  end_time = time.time()
  # Calcula o tempo de execução
  execution_time = end_time - start_time
  print(f"Tempo de execução: {execution_time:.6f} segundos")

  return array
# Optei por resumir para apenas 8 iniciais e finais no print
# Printando o array antes da ordenação:
print(f"Antes:{(array[:8] + ['...'] + array[-8:])}")
# Printando o array depois da ordenação:
lista = SelectionSort(array)
print(f"Depois:{(lista[:8] + ['...'] + lista[-8:])}")
```
```bash
Antes:[1000, 93287, -2, 94656, -29, -14, 24, -48, '...', -39, -46, 67711, 14, 42, 65284, 26, 58119]
Tempo de execução: 0.057317 segundos
Depois:[-50, -50, -50, -49, -49, -49, -49, -49, '...', 99199, 99242, 99311, 99638, 99659, 99716, 99877, 99911]
```
### Insertion Sort:

#### Explicação do código:
Iniciamos o algoritmo com um loop 'for' que começa a partir da segunda posição, uma vez que iremos observar e comparar esses elementos com os elementos à esquerda, que não existem na primeira posição. Neste algoritmo, selecionamos um elemento representado pela variável "atual", armazenamos o seu valor e o comparamos com os elementos à esquerda. Ao fazer isso, arrastamos os elementos com valores maiores para a direita até encontrar um que seja menor ou até atingirmos a posição 0. Quando isso ocorre, deslocamos o elemento desta posição para a direita e inserimos o "atual". Repetindo esse processo para todos os elementos, obtemos uma lista ordenada, resultado de um algoritmo com complexidade O(N²).

#### Tempo de execução:
- Executando 1000 elementos: Em média aproximadamente 0,05 segundos.
- Executando 10000 elementos: Em média aproximadamente 5,6 segundos.
- Executando 100000 elementos: Em média aproximadamente 540 segundos.

```python
import time
import copy

def InsertionSort(arr):
    array = copy.copy(arr)
    # Registra o tempo de início
    start_time = time.time()
    # Algoritmo
    for i in range(1, len(array)):
        atual = array[i]
        j = i - 1
        while j >= 0 and atual < array[j]:
            array[j + 1] = array[j]
            j -= 1
        array[j + 1] = atual
    # Registra o tempo de término
    end_time = time.time()
    # Calcula o tempo de execução
    execution_time = end_time - start_time
    print(f"Tempo de execução: {execution_time:.6f} segundos")
    return array

# Optei por resumir para apenas 8 iniciais e finais no print
# Printando o array antes da ordenação:
print(f"Antes:{(array[:8] + ['...'] + array[-8:])}")
# Printando o array depois da ordenação:
lista = InsertionSort(array)
print(f"Depois:{(lista[:8] + ['...'] + lista[-8:])}")
```
```bash
Antes:[1000, 93287, -2, 94656, -29, -14, 24, -48, '...', -39, -46, 67711, 14, 42, 65284, 26, 58119]
Tempo de execução: 0.045860 segundos
Depois:[-50, -50, -50, -49, -49, -49, -49, -49, '...', 99199, 99242, 99311, 99638, 99659, 99716, 99877, 99911]
```
### Merge Sort:
#### Explicação do código:
Temos duas funções no código abaixo, sendo a primeira MergeSort uma recursiva que até que fique o menor array possível (1 ou 2) vai dividir em  arrays menores esquerda e direita. Quando não é mais possível dividir executa-se o merge que é basicamente juntar o que foi dividido observando o que é maior e o que menor (esquerda ou direita) e juntando os dois, até que o array volte a ter o tamanho que tinha antes, ou seja, execute o Merge da função inicial.
#### Tempo de execução:
- Executando 1000 elementos: Em média aproximadamente 0,005 segundos.
- Executando 10000 elementos: Em média aproximadamente 0,05 segundos.
- Executando 100000 elementos: Em média aproximadamente 0,7 segundos.
```python
import time

def MergeSort(arr, inicio=0, fim=None):
    if fim is None:
        fim = len(arr)
    if fim - inicio > 1:
        meio = (fim + inicio) // 2
        esquerda = MergeSort(arr[inicio:meio])
        direita = MergeSort(arr[meio:fim])
        return Merge(esquerda, direita)
    return arr

def Merge(esquerda, direita):
    resultado = []
    topo_esquerda = topo_direita = 0

    while topo_esquerda < len(esquerda) and topo_direita < len(direita):
        if esquerda[topo_esquerda] < direita[topo_direita]:
            resultado.append(esquerda[topo_esquerda])
            topo_esquerda += 1
        else:
            resultado.append(direita[topo_direita])
            topo_direita += 1

    resultado.extend(esquerda[topo_esquerda:])
    resultado.extend(direita[topo_direita:])
    return resultado

# Printando o array antes da ordenação:
print(f"Antes:{(array[:8] + ['...'] + array[-8:])}")
# Printando o array depois da ordenação e registrando o tempo de início:
start_time = time.time()
lista = MergeSort(array)
# Registra o tempo de término
end_time = time.time()
# Calcula o tempo de execução
execution_time = end_time - start_time
print(f'Tempo de execução: {execution_time} segundos')
print(f"Depois:{lista[:8] + ['...'] + lista[-8:]}")
```
```bash
Antes:[1000, 93287, -2, 94656, -29, -14, 24, -48, '...', -39, -46, 67711, 14, 42, 65284, 26, 58119]
Tempo de execução: 0.005500316619873047 segundos
Depois:[-50, -50, -50, -49, -49, -49, -49, -49, '...', 99199, 99242, 99311, 99638, 99659, 99716, 99877, 99911]
```
