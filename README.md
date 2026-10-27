# 🤖 Netinho Digital — Assistente Inteligente de Vendas

**Assistente de vendas via Telegram para registro e consulta de transações por texto ou áudio.**

Projeto desenvolvido para simplificar a rotina comercial de uma pequena loja, permitindo registrar vendas, consultar informações e organizar dados utilizando linguagem natural, inteligência artificial e uma planilha Excel como base de armazenamento.

> **Categoria:** Automação comercial e inteligência artificial aplicada  
> **Status:** Protótipo funcional em desenvolvimento  
> **Autoria:** Galves-gi

![Texto Alternativo](https://github.com/Galves-gi/Assistente-Inteligente-de-Vendas/blob/main/imagem%20(4).png)

---

## 📌 Sumário

- [1. Sobre o projeto](#-1-sobre-o-projeto)
- [2. Problema e objetivo](#-2-problema-e-objetivo)
- [3. Funcionalidades](#-3-funcionalidades)
- [4. Como funciona](#-4-como-funciona)
- [5. Tecnologias utilizadas](#-5-tecnologias-utilizadas)
- [6. Estrutura dos dados](#-6-estrutura-dos-dados)
- [7. Pré-requisitos](#-7-pré-requisitos)
- [8. Validação e tratamento de erros](#-8-validação-e-tratamento-de-erros)
- [9. Aprendizados do projeto](#-9-aprendizados-do-projeto)

---

## 🎯 1. Sobre o projeto

O **Netinho Digital** é um assistente de vendas que conecta o Telegram a uma planilha Excel por meio de um fluxo de processamento desenvolvido em Python.

A usuária pode enviar mensagens de texto ou notas de voz descrevendo uma venda ou solicitando informações sobre registros existentes. O sistema processa a mensagem, identifica a intenção, valida os dados necessários e executa a operação correspondente.

O projeto utiliza inteligência artificial generativa para interpretar linguagem natural, enquanto as regras de negócio implementadas em Python controlam a validação e o processamento das informações.

A proposta é simplificar tarefas comerciais sem exigir que a usuária abandone a ferramenta de organização que já utiliza.

## 💡 2. Problema e objetivo

### Problema

O registro e a consulta de vendas podem se tornar trabalhosos quando as informações são preenchidas manualmente, estão distribuídas em diferentes campos ou não seguem um padrão consistente.

Essa dificuldade pode afetar tarefas como:

- Registrar vendas durante o atendimento.
- Localizar pedidos por cliente, produto ou data.
- Acompanhar formas de pagamento e parcelamentos.
- Consultar valores pendentes.
- Recuperar informações de entrega e rastreamento.

### Objetivo

Desenvolver um assistente acessível pelo Telegram que permita registrar e consultar vendas por meio de mensagens naturais, utilizando IA para interpretar solicitações e Python para executar as operações com validações programáticas.

### Proposta de valor

**Menos etapas para registrar informações, mais facilidade para consultar os dados do negócio.**

---

## ✨ 3. Funcionalidades

### Entrada por texto e áudio

Recebe mensagens pelo Telegram. No fluxo de áudio, o sistema baixa o arquivo enviado e realiza o processamento necessário para obter a transcrição.

### Interpretação de linguagem natural

Utiliza a API do Gemini para identificar se a solicitação corresponde a uma inserção de venda ou a uma consulta e estruturar os parâmetros extraídos da mensagem.

### Validação de dados e regras de negócio

Aplica verificações em Python para validar campos obrigatórios, tipos de dados e condições específicas, como número de parcelas e saldo pendente.

### Cadastro de vendas

Utiliza Pandas e openpyxl para adicionar novos registros à planilha Excel, buscando preservar as informações já existentes.

### Consultas combinadas

Permite filtrar registros por informações como cliente, produto, data, forma de pagamento e termos de pesquisa, conforme os filtros implementados no código.

### Tratamento de falhas

Contempla tratamento de exceções e tentativas adicionais para determinadas falhas de comunicação com a API.

---

## ⚙️ 4. Como funciona

O processamento segue estas etapas:

1. **Recebimento:** o usuário envia uma mensagem pelo Telegram.
2. **Preparação:** se for áudio, o arquivo é baixado, convertido quando necessário e enviado para transcrição.
3. **Interpretação:** o Gemini analisa o texto e estrutura a intenção e os dados relevantes.
4. **Validação:** Python verifica se as informações atendem ao contrato de dados e às regras de negócio.
5. **Execução:** o sistema registra uma venda ou consulta os dados da planilha.
6. **Resposta:** o bot retorna uma confirmação, os resultados encontrados ou uma mensagem informando os dados ausentes ou os erros identificados.

A inteligência artificial auxilia na interpretação da linguagem natural. A execução das operações permanece sob controle do código Python.

> ![Texto Alternativo](https://github.com/Galves-gi/Assistente-Inteligente-de-Vendas/blob/main/Fluxo%20de%20mensagens%20com%20IA.jpg)

---

## 🧰 5. Tecnologias utilizadas

| Tecnologia | Finalidade |
|---|---|
| **Python 3.10+** | Linguagem principal e implementação das regras de negócio. |
| **Telegram Bot API** | Comunicação entre a usuária e o assistente. |
| **pyTelegramBotAPI** | Recebimento de mensagens e envio de respostas pelo Telegram. |
| **Google Gemini API** | Interpretação de mensagens e processamento de linguagem natural. |
| **google-genai** | SDK Python para integração com a API do Gemini. |
| **Pandas** | Leitura, tratamento, filtragem e atualização dos dados. |
| **openpyxl** | Manipulação de arquivos Excel no formato XLSX. |
| **soundfile** | Leitura e processamento de arquivos de áudio, conforme o formato suportado. |
| **Google Colab** | Ambiente utilizado para desenvolvimento e execução do protótipo. |
| **Google Drive** | Armazenamento e acesso aos arquivos, quando configurado no Colab. |

---

## 📊 6. Estrutura dos dados

A planilha utiliza os seguintes campos:

| Campo | Descrição | Regra principal |
|---|---|---|
| `data` | Data da venda | Utiliza o formato `DD/MM/AAAA`, conforme o processamento implementado. |
| `oq vendeu` | Produto vendido | Obrigatório. |
| `pra quem` | Nome do cliente | Opcional. |
| `valor` | Valor total da venda em reais | Obrigatório; deve ser numérico. |
| `como pagou` | Forma de pagamento | Valores previstos: `pix`, `dinheiro`, `debito`, `credito` ou `fiado`. |
| `cartao` | Bandeira ou marca do cartão | Opcional. |
| `vezes` | Número de parcelas | Obrigatório para pagamentos no crédito. |
| `entrega ou loja` | Canal de entrega ou atendimento | Valores previstos: `entrega`, `motoboy`, `correios`, `loja` ou `presencial`. |
| `rastreio` | Código de rastreamento | Opcional. |
| `obs` | Observações adicionais | Texto livre. |
| `valor_restante` | Saldo devedor da venda | Deve ser tratado conforme as regras de pagamento implementadas. |

**Observação:** a planilha é gerada se não encontrar o arquivo correspondente. 

### Regras de negócio relevantes

- Uma venda deve conter: data, nome do produto, valor, forma de pagamento.
- Uma venda no crédito deve informar o número de parcelas.
- A forma de pagamento deve corresponder a um dos valores aceitos pelo sistema (pix, débito, crédito,dinheiro, fiado).
- O canal de entrega ou atendimento deve ser informado conforme as regras implementadas.
- O saldo pendente não deve ser confundido com o valor total da venda.
- Campos ausentes não devem ser preenchidos automaticamente com valores que possam alterar o significado financeiro do registro.

---

## 💻 7. Pré-requisitos

Antes de executar o projeto, tenha:

- Python 3.10 ou superior, caso execute em ambiente local.
- Uma conta no Telegram.
- Um bot criado pelo [@BotFather](https://t.me/BotFather).
- Uma chave de API do Gemini, obtida pelo [Google AI Studio](https://aistudio.google.com/).
- Permissões de leitura e escrita no local em que a planilha está armazenada.

---

## 🧪 8. Validação e tratamento de erros

O projeto contempla validações programáticas para reduzir inconsistências durante o cadastro.

Entre os cenários relevantes estão:

- Ausência de informações obrigatórias.
- Número de parcelas não informado em uma venda no crédito.
- Valores ou tipos de dados inválidos.
- Forma de pagamento fora das opções previstas.
- Erros durante chamadas à API.
- Falhas durante a leitura, filtragem ou gravação da planilha.

O notebook também descreve o uso de até três tentativas com recuo exponencial para determinadas falhas da API, incluindo respostas como `429` e `503`.

---

## 🧠 9. Aprendizados do projeto

O desenvolvimento do Netinho Digital envolve a aplicação prática de conceitos de automação, integração de APIs, processamento de linguagem natural e manipulação de dados.

Entre os principais aprendizados e competências exercitados estão:

- Integração entre Telegram, Python e serviços de IA.
- Estruturação de prompts para extração de informações.
- Validação de dados e implementação de regras de negócio.
- Manipulação de arquivos Excel com Pandas e openpyxl.
- Tratamento de exceções e falhas de serviços externos.
- Organização de fluxos de processamento.
- Identificação de limitações e planejamento de melhorias.

A inteligência artificial também foi utilizada como apoio durante o desenvolvimento para comparar ideias, identificar lacunas e auxiliar na construção do protótipo. As decisões de implementação e a validação da solução continuam sendo responsabilidades do desenvolvimento.

---

**Netinho Digital — tecnologia aplicada à organização da rotina comercial.**
