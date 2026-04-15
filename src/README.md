# Código da Aplicação

Esta pasta contém o código do seu agente financeiro.

CÓDIGO DO AGENTE DESENVOLVIDO NO VS CODE
```
import json
import pandas as pd
import requests
import streamlit as st

# ========= CONFIGURAÇÃO =========
OLLAMA_URL = "http://localhost:11434/api/generate"
MODELO = "gpt-oss"

# ========= CARREGAR DADOS =========
perfil = json.load(open('./data/perfil_investidor.json'))
transacoes = pd.read_csv('./data/transacoes.csv')
historico = pd.read_csv('./data/historico_atendimento.csv')
produtos = json.load(open('./data/produtos_financeiros.json'))

# ========= MONTAR CONTEXTO =========
contexto = f"""
CLIENTE: {perfil['nome']}, {perfil['idade']} anos, perfil: {perfil['perfil_investidor']}
OBJETIVO: {perfil['objetivo_principal']}
PATRIMÔNIO: R$ {perfil['patrimonio_total']} | RESERVA: R$ {perfil['reserva_emergencia_atual']}

TRANSAÇÕES RECENTES:
{transacoes.to_string(index=False)}

ATENDIMENTOS ANTERIORES:
{historico.to_string(index=False)}

PRODUTOS DISPONÍVEIS:
{json.dumps(produtos, indent=2, ensure_ascii=False)}
"""

# ========= SYSTEM PROMPT =========

SYSTEM_PROMPT = """
OBJETIVO:
Você é o InvestIA, um agente que irá tirar dúvidas de clientes a respeito de tipos de investimentos de forma simples e didática, usando dados do cliente com exemplos práticos

REGRAS:
1. Sempre baseie suas respostas nos dados fornecidos
2. Nunca invente informações financeiras
3. Se não souber algo, admita e ofereça alternativas
4. Linguagem simples
5. Sempre pergunte educadamente se o cliente entendeu
6. Responda sempre de forma sucinta e direta em poucas linhas
7. Jamais responda a perguntas fora do tema de finanças, quando isso ocorrer, responda lembrando seu papel de educador de investimentos
"""

# ============ CHAMAR OLLAMA ============
def perguntar(msg):
    prompt = f"""
    {SYSTEM_PROMPT}

    CONTEXTO DO CLIENTE:
    {contexto}

    Pergunta: {msg}"""

    r = requests.post(OLLAMA_URL, json={"model": MODELO, "prompt": prompt, "stream": False})
    return r.json()['response']
                    
# ============ INTERFACE ============
st.title("InvestIA, Seu Educador de Investimentos")

if pergunta := st.chat_input("Sua dúvida sobre finanças..."):
    st.chat_message("user").write(pergunta)
    with st.spinner("..."):
        st.chat_message("assistant").write(perguntar(pergunta))
```


## Estrutura Sugerida

```
src/
├── app.py              # Aplicação principal (Streamlit/Gradio)
├── agente.py           # Lógica do agente
├── config.py           # Configurações (API keys, etc.)
└── requirements.txt    # Dependências
```

## Exemplo de requirements.txt

```
streamlit
openai
python-dotenv
```

## Como Rodar

```bash
# Instalar dependências
pip install -r requirements.txt

# Rodar a aplicação
streamlit run app.py
```
