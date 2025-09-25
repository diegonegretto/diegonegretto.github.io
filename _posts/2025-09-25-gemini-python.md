---
layout: post
title:  Criando um Cliente em Python para a API do Gemini 🤖 [IA]
---

Neste post vamos aprender a construir um projeto em **Python** que se
conecta à API do **Gemini** (Google DeepMind).
O objetivo é criar uma aplicação simples que rode no terminal e permita
fazer perguntas para a IA.


🖥️ Você pode acessar o código-fonte deste projeto em meu repositório no [GitHub](https://github.com/diegonegretto/python_ai) 


------------------------------------------------------------------------

## 🎯 O que você vai aprender

-   Como organizar um projeto Python que consome uma API.
-   Como usar variáveis de ambiente para proteger informações sensíveis (como a chave da API).
-   Como criar uma classe para centralizar a comunicação com o Gemini.
-   Como montar um menu simples para interagir com a IA pelo terminal.


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

Todas as bibliotecas estão listadas em `requirements.txt`.
As principais são:

-   **google-genai** → para acessar o Gemini.
-   **python-dotenv** → para carregar variáveis do `.env`.

Instale com:

``` bash
pip install -r requirements.txt
```

------------------------------------------------------------------------

## 🔑 Configuração da API Key

Para usar a API, você precisa de uma chave fornecida pelo Google.
Essa chave deve ser armazenada no arquivo .env (nunca diretamente no código!):
`.env`:

``` env
API_KEY="sua_chave_aqui"
```

Esse valor é lido pelo programa em tempo de execução.

⚠️ **Importante**:
-   Não compartilhe esse arquivo em repositórios públicos.
-   Sempre use .gitignore para proteger seu .env.

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


### O que está acontecendo aqui?
-   Criamos um cliente (genai.Client) usando nossa chave de API.
-   Definimos o modelo que vamos usar (gemini-2.5-flash).
-   No método ask, enviamos a pergunta (prompt) e recebemos a resposta da IA.
-   Limitamos a resposta a 250 caracteres para não ficar muito longa.


------------------------------------------------------------------------

## 🎛️ A Aplicação Principal (`main.py`)

O `main.py` é responsável pela interação com o usuário.
Ele mostra um menu no terminal, onde é possível escolher entre **fazer
uma pergunta** ou **sair do programa**.

```python
if __name__ == "__main__":
    load_dotenv()
    api_key = os.getenv("API_KEY")

    if not api_key:
        raise ValueError("Defina a variável API_KEY no .env")

    app = Application(api_key=api_key)
    app.menu()
```

Antes de rodar o menu, o código faz três coisas importantes:

1.  **Carrega as variáveis de ambiente** com `load_dotenv()`.
2.  **Busca a chave da API** usando `os.getenv("API_KEY")`.
3.  **Valida se a chave existe** --- se não existir, o programa exibe um
    erro e não continua.

Somente depois disso o programa cria a aplicação (`Application`) e
inicia o menu.
Esse fluxo garante que só conseguimos interagir com a IA se a chave
estiver corretamente configurada.


```python
class Application:
    
    def __init__(self, api_key):
        self.ai = PythonAI(api_key)

    def menu(self):
        print("Bem-vindo ao PythonAI!")
        print("=========================")

        while True:
            print("Escolha uma das opções:")
            print("1 - Perguntar para a AI.")
            print("0 - Sair.")
            print("=========================")

            try:
                op = int(input("Opção: "))
            except ValueError:
                print("Entrada inválida! Digite apenas números.")
                continue

            if op == 1:
                prompt = input("Faça uma pergunta: ")
                response = self.ai.ask(prompt)
                print(response)

            elif op == 0:
                print("Até mais!")
                break

            else:
                print("Opção inválida!")

            print("=========================")
```

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

Esse projeto é um **ponto de partida simples**, mas poderoso.
Você aprendeu a:
-   Configurar um projeto Python com **variáveis de ambiente**.
-   Criar um **cliente de IA**.
-   Fazer uma aplicação de linha de comando para interagir com o Gemini.

👉 **Possíveis evoluções:**

-   Criar uma versão **web** (com Flask ou Django).
-   Construir uma **interface gráfica** (com Tkinter/PyQt).
-   Integrar com **chatbots em sites**.


------------------------------------------------------------------------
