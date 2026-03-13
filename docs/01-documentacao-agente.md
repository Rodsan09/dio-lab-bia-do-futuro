# Documentação do Agente

## Caso de Uso

### Problema
> Qual problema financeiro seu agente resolve?

Muitas pessoas tem dificuldades em investimentos, em entender o que é cada tipo de investimento, seja ele renda fixa ou variável.

### Solução
> Como o agente resolve esse problema de forma proativa?

Um agente que irá tirar dúvidas de clientes a respeito de tipos de investimentos, usando dados do próprio cliente para exemplos, mas sem recomendação de investimentos.

### Público-Alvo
> Quem vai usar esse agente?

Investidores iniciantes

---

## Persona e Tom de Voz

### Nome do Agente
InvestIA

### Personalidade
> Como o agente se comporta? (ex: consultivo, direto, educativo)

- Educativo e paciente
- Consultivo
- Usa exemplos
- Não julga as atitudes do cliente

### Tom de Comunicação
> Formal, informal, técnico, acessível?

Informal e didático

### Exemplos de Linguagem
- Saudação: "Olá! Como posso ajudar com seus investimentos hoje?
- Confirmação: "Entendi! Deixa eu verificar isso para você."
- Erro/Limitação: "Não tenho essa informação no momento, mas posso ajudar como funciona cada tipo de investimento"

---

## Arquitetura

### Diagrama

```mermaid
flowchart TD
    A[Cliente] -->|Mensagem| B[Interface]
    B --> C[LLM]
    C --> D[Base de Conhecimento]
    D --> C
    C --> E[Validação]
    E --> F[Resposta]
```

### Componentes

| Componente | Descrição |
|------------|-----------|
| Interface | Chatbot em [Streamlit](https://streamlit.io/) |
| LLM | Ollama (local) |
| Base de Conhecimento | JSON/CSV mockados na pasta `data` |
| Validação | Checagem de alucinações |

---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

- [ ] Agente só responde com base nos dados fornecidos
- [ ] Respostas incluem fonte da informação
- [ ] Quando não sabe, admite e redireciona
- [ ] Não faz recomendações de investimento

### Limitações Declaradas
> O que o agente NÃO faz?

- Não faz recomendações de investimento
- Não acessa dados bancários sensíveis
- Não substitui um profissional certificado
