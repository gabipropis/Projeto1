# 🤖 TechBurger Chatbot
 
Um projeto Python simples que demonstra a criação de um **chatbot com personalidade e contexto de negócio definidos** (System Instruction) usando a biblioteca `google-genai` (API do Gemini). O chatbot atua como assistente virtual de uma hamburgueria futurista chamada **TechBurger**.
 
## ⚙️ Tecnologias Utilizadas
 
* **Linguagem:** Python
* **Biblioteca Principal:** `google-genai` (API do Gemini)
* **Modelo de IA:** `gemini-2.5-flash`
* **Ambiente:** Jupyter Notebook ou Google Colab (devido ao uso de `IPython.display.Markdown`)
 
## ✨ Principais Funcionalidades
 
* **Configuração de Personalidade:** O bot recebe um contexto de negócio detalhado (`contexto_negocio`) que define seu cardápio, horário e tom de voz (amigável e nerd).
* **Histórico de Conversa (Chat):** Utiliza a funcionalidade `start_chat` para manter o contexto e a personalidade definidos ao longo da interação.
* **Loop de Interação:** Limita a interação a um número pré-definido de perguntas (3, no código original).
* **Geração de Resumo:** Ao final, uma **segunda chamada à API** é usada para resumir o atendimento em tópicos, demonstrando o uso de *prompt engineering* para sumarização.
 
## 🍔 Contexto da TechBurger
 
O chatbot foi instruído a seguir a persona e as regras do seguinte negócio:
 
| Detalhe | Informação |
| :--- | :--- |
| **Persona** | Assistente virtual amigável, nerd e prestativo. |
| **Cardápio** | Burger Bit (R$ 20,00), Chips de Silício (R$ 10,00), Shake Java (R$ 15,00). |
| **Horário** | Das 18h às 23h, de terça a domingo. |
| **Regras** | Responde **apenas** perguntas sobre a hamburgueria (regra de segurança). |
 
## 🚀 Como Rodar
 
### Pré-requisitos
 
1.  **Python:** Tenha o Python instalado (versão 3.9+).
2.  **Chave API do Gemini:** Obtenha sua chave de API no Google AI Studio.
 
### Passos de Execução
 
1.  **Instale as Dependências:**
    ```bash
    pip install google-genai ipython
    ```
 
2.  **Configure a Chave API:**
    Substitua o valor de `GOOGLE_API_KEY` no arquivo do projeto pela sua chave real:
    ```python
    GOOGLE_API_KEY = "SUA_CHAVE_AQUI" 
    ```
 
    > **⚠️ Aviso de Segurança:** Em projetos de produção, utilize variáveis de ambiente (`os.environ`) para carregar a chave de API de forma segura, evitando deixá-la diretamente no código-fonte.
 
3.  **Execute o Script:**
    Se estiver usando um ambiente Notebook (Colab ou Jupyter), execute as células na ordem. O script iniciará o chat e pedirá as 3 perguntas.
 
## 💻 Trecho Chave do Código
 
Este é o trecho onde o contexto é injetado e a sessão de chat é iniciada, garantindo que o bot mantenha sua persona em toda a conversa:
 
```python
# Inicializa o chat com a instrução do sistema
chat = model.start_chat(history=[
    {"role": "user", "parts": f"Aja conforme este contexto: {contexto_negocio}"},
    {"role": "model", "parts": "Entendido! Estou pronto para atender os clientes da TechBurger."}
])
