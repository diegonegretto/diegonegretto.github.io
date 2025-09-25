---
layout: post
title:  Criando um Cliente em Python para a API do Gemini 🤖 [IA]
---

Neste post vamos aprender a construir um projeto em **Python** que se
conecta à API do **Gemini** (Google DeepMind).\
O objetivo é criar uma aplicação simples que rode no terminal e permita
fazer perguntas para a IA.

![Python + Gemini](/img/Gemini+Python.jpg)
------------------------------------------------------------------------

## 🎯 O que você vai aprender

-   Como organizar um projeto Python que consome APIs.\
-   Como usar variáveis de ambiente para proteger sua chave da API.\
-   Como criar um cliente Python para o Gemini.\
-   Como interagir com a IA pelo terminal.

------------------------------------------------------------------------

## 🛠️ Estrutura do Projeto

Nosso projeto tem a seguinte organização:

    📂 projeto_gemini
     ├── ai_client.py        # Cliente que conversa com a API do Gemini
     ├── main.py             # Aplicação principal (menu no terminal)
     ├── requirements.txt    # Dependências
     └── .env                # Variável de ambiente com a API Key

------------------------------------------------------------------------

## 📦 Instalando Dependências

Todas as bibliotecas estão listadas em `requirements.txt`.\
As principais são:

-   **google-genai** → para acessar o Gemini.\
-   **python-dotenv** → para carregar variáveis do `.env`.

Instale com:

``` bash
pip install -r requirements.txt
```

------------------------------------------------------------------------

## 🔑 Configuração da API Key

A API do Gemini precisa de autenticação. Para isso, criamos um arquivo
`.env`:

``` env
API_KEY="sua_chave_aqui"
```

Esse valor é lido pelo programa em tempo de execução.\
⚠️ Lembre-se: nunca compartilhe essa chave em repositórios públicos.

------------------------------------------------------------------------

## 🧩 O Cliente de IA (`ai_client.py`)

A classe `PythonAI` centraliza a comunicação com o Gemini:

``` python
from google import genai

class PythonAI:
    def __init__(self, api_key, model="gemini-2.5-flash"):
        self.client = genai.Client(api_key=api_key)
        self.model = model

    def ask(self, prompt):
        prompt += " Responda em até 250 caracteres."
        response = self.client.models.generate_content(
            model=self.model,
            contents=prompt
        )
        return response.text
```

Ela recebe a chave da API, conecta ao modelo `gemini-2.5-flash`, envia
perguntas (prompts) e retorna as respostas.\
É como se fosse um "**tradutor**" entre o usuário e a IA.

![Gemini 2.5 Flash](/img/google-gemini-flash.jpg)
------------------------------------------------------------------------

## 🎛️ A Aplicação Principal (`main.py`)

O `main.py` é responsável pela interação com o usuário.\
Ele mostra um menu no terminal, onde é possível escolher entre **fazer
uma pergunta** ou **sair do programa**.

Antes de rodar o menu, o código faz três coisas importantes:

1.  **Carrega as variáveis de ambiente** com `load_dotenv()`.\
2.  **Busca a chave da API** usando `os.getenv("API_KEY")`.\
3.  **Valida se a chave existe** --- se não existir, o programa exibe um
    erro e não continua.

Somente depois disso o programa cria a aplicação (`Application`) e
inicia o menu.\
Esse fluxo garante que só conseguimos interagir com a IA se a chave
estiver corretamente configurada.

------------------------------------------------------------------------

## ▶️ Executando o Projeto

Com tudo configurado, basta rodar:

``` bash
python main.py
```

Exemplo prático:

    Bem-vindo ao PythonAI!
    =========================
    Escolha uma das opções:
    1 - Perguntar para a AI.
    0 - Sair.
    =========================
    Opção: 1
    Faça uma pergunta: Qual a capital da França?
    Resposta: Paris.

------------------------------------------------------------------------

## 📌 Conclusão e Próximos Passos

Esse projeto é simples, mas mostra um fluxo completo de integração com a
API do Gemini.\
A partir daqui, você pode evoluir para:

-   Criar uma versão **web** (Flask/Django).\
-   Desenvolver uma **interface gráfica** (Tkinter/PyQt).\
-   Conectar a IA com **chatbots para sites ou WhatsApp**.

------------------------------------------------------------------------
