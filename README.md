# 🤖 InvestIA — Educador Financeiro com IA Generativa

Agente conversacional desenvolvido como solução para o Lab **Bia do Futuro** da [DIO](https://www.dio.me/). O InvestIA é um educador financeiro que tira dúvidas sobre investimentos de forma simples e didática, sem recomendar produtos — apenas educar.

---

## 💡 Sobre o Projeto

Muitas pessoas têm dificuldade em entender o mercado financeiro. O InvestIA resolve isso com um chatbot que:

- Explica conceitos de renda fixa e variável de forma acessível
- Usa os dados do próprio cliente como exemplos práticos
- Nunca inventa informações (anti-alucinação por design)
- Não substitui nem recomenda investimentos — apenas educa

**Público-alvo:** investidores iniciantes

---

## 🏗️ Arquitetura

```
Cliente → Interface (Streamlit) → LLM (Ollama local) → Base de Conhecimento → Resposta Validada
```

| Componente | Tecnologia |
|---|---|
| Interface | Streamlit |
| LLM | Ollama (local) |
| Base de Conhecimento | JSON/CSV mockados |
| Anti-alucinação | Prompt restritivo + dados injetados no contexto |

---

## 📁 Estrutura do Repositório

```
📁 investia/
├── README.md
├── 📁 data/
│   ├── perfil_investidor.json       # Perfil e metas do cliente
│   ├── produtos_financeiros.json    # Produtos disponíveis para explicar
│   ├── transacoes.csv               # Histórico de transações
│   └── historico_atendimento.csv    # Atendimentos anteriores
├── 📁 docs/
│   ├── 01-documentacao-agente.md    # Caso de uso e arquitetura
│   ├── 02-base-conhecimento.md      # Estratégia de dados e integração
│   ├── 03-prompts.md                # System prompt e exemplos de interação
│   ├── 04-metricas.md               # Avaliação e resultados dos testes
│   └── 05-pitch.md                  # Roteiro do pitch
├── 📁 src/
│   └── app.py                       # Código principal da aplicação
└── 📁 assets/
    └── RoteiroLab.md
```

---

## 🚀 Como Rodar

**Pré-requisitos:** Python 3.8+, [Ollama](https://ollama.ai/) instalado e rodando localmente.

```bash
# Instalar dependências
pip install streamlit requests pandas

# Rodar a aplicação
streamlit run src/app.py
```

> O modelo padrão configurado é `gpt-oss` via Ollama em `localhost:11434`. Altere a variável `MODELO` em `app.py` conforme o modelo que você tiver disponível.

---

## 🧠 System Prompt

O comportamento do agente é controlado por um prompt restritivo que define:

- Responder apenas com base nos dados fornecidos
- Nunca inventar informações financeiras
- Admitir quando não sabe e redirecionar
- Linguagem simples e didática
- Recusar perguntas fora do tema de finanças

Veja o prompt completo em [`docs/03-prompts.md`](./docs/03-prompts.md).

---

## 📊 Dados Mockados

Os dados na pasta `data/` representam um cliente fictício (João Silva, perfil moderado) e incluem transações, histórico de atendimento e produtos financeiros disponíveis — inclusive um **Fundo Imobiliário (FII)** adicionado além do dataset original.

---

## ✅ Resultados dos Testes

| Critério | Resultado |
|---|---|
| Não alucinação | ✅ Não inventou informações |
| Escopo correto | ✅ Recusou perguntas fora de finanças |
| Uso da base de dados | ✅ Utilizou os dados do cliente nos exemplos |
| Ponto de melhoria | Expandir a base de dados para mais cenários de teste |

---

## 📄 Documentação Completa

| Documento | Conteúdo |
|---|---|
| [`docs/01-documentacao-agente.md`](./docs/01-documentacao-agente.md) | Persona, arquitetura e segurança |
| [`docs/02-base-conhecimento.md`](./docs/02-base-conhecimento.md) | Integração dos dados com o LLM |
| [`docs/03-prompts.md`](./docs/03-prompts.md) | System prompt, exemplos e edge cases |
| [`docs/04-metricas.md`](./docs/04-metricas.md) | Métricas de avaliação e resultados |
| [`docs/05-pitch.md`](./docs/05-pitch.md) | Roteiro do pitch de 3 minutos |
