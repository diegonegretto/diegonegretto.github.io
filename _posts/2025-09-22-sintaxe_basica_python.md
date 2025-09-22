---
layout: post
title:  Sintaxe Básica do Python - Entrada, Saída e Tipos de Dados 💻 [Python Básico]
---

Depois de instalar o Python e executar seu primeiro programa, é hora de entender os **fundamentos da linguagem**. Neste post, vamos explorar dois pontos essenciais para qualquer iniciante:  

- Como funciona a **entrada e saída de dados**.  
- Quais são os **tipos de dados básicos** em Python.  

---

## Saída de Dados com `print()`

A função `print()` é usada para **exibir informações na tela**.  

### Exemplo simples:
```python
print("Olá, mundo!")
```

Saída no terminal:
```
Olá, mundo!
```

---

### Concatenando textos
Podemos **juntar strings** (concatenação) usando o operador `+`.  

```python
nome = "Diego"
print("Olá, " + nome + "! Seja bem-vindo.")
```

Saída:
```
Olá, Diego! Seja bem-vindo.
```

---

### Separando valores com vírgula
O `print()` também permite exibir vários valores separados por vírgulas.  
O Python automaticamente insere um espaço entre eles:  

```python
nome = "Diego"
idade = 36
print("Nome:", nome, "| Idade:", idade)
```

Saída:
```
Nome: Diego | Idade: 36
```

---

### Usando *f-strings* (formatação moderna)
As **f-strings** (a partir do Python 3.6) são a forma mais prática de formatar saídas.  
Permitem incluir variáveis **dentro da string**, usando `{}`.  

```python
nome = "Diego"
idade = 36
print(f"Meu nome é {nome} e tenho {idade} anos.")
```

Saída:
```
Meu nome é Diego e tenho 36 anos.
```

Também podemos aplicar **formatos especiais**:  

```python
preco = 59.9
print(f"O produto custa R$ {preco:.2f}")
```

Saída:
```
O produto custa R$ 59.90
```

---

## Entrada de Dados com `input()`

A função `input()` é usada para **ler informações digitadas pelo usuário**.  
Por padrão, o valor lido pelo `input()` sempre será do tipo **string** (`str`).

Exemplo:
```python
nome = input("Digite seu nome: ")
print(f"Bem-vindo, {nome}!")
```

Execução no terminal:
```
Digite seu nome: Diego
Bem-vindo, Diego!
```

---

## Tipos de Dados Básicos em Python

Python possui diferentes tipos de dados para representar informações. Os principais são:

### 1. String (`str`)
Representa **textos**.  
```python
mensagem = "Aprendendo Python"
print(mensagem)
```

### 2. Inteiro (`int`)
Representa **números inteiros**.  
```python
idade = 36
print("Idade:", idade)
```

### 3. Ponto flutuante (`float`)
Representa **números decimais**.  
```python
altura = 1.75
print(f"Altura: {altura} metros")
```

### 4. Booleano (`bool`)
Representa valores **verdadeiro ou falso**.  
```python
chovendo = True
print("Está chovendo?", chovendo)
```

---

## Convertendo Tipos de Dados

Como o `input()` sempre retorna uma **string**, muitas vezes precisamos **converter** para outro tipo.  

Exemplo: somando dois números digitados pelo usuário.  

```python
num1 = int(input("Digite um número: "))
num2 = int(input("Digite outro número: "))
soma = num1 + num2
print(f"A soma de {num1} + {num2} é {soma}")
```

Execução:
```
Digite um número: 5
Digite outro número: 7
A soma de 5 + 7 é 12
```

---

## Conclusão

Neste post você aprendeu:  

- Como usar `print()` para exibir informações de diferentes formas:  
  - Simples.  
  - Concatenando com `+`.  
  - Separando com vírgulas.  
  - Usando **f-strings** para formatação elegante.  
- Como usar `input()` para receber dados do usuário.  
- Quais são os **tipos de dados básicos** (`str`, `int`, `float`, `bool`).  
- Como fazer **conversão de tipos**.  

Esses são os primeiros passos para criar programas interativos. 🚀   

---

👉 E você? Já começou a se aventurar na programação com Python?  
