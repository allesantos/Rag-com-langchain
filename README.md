# 🤖 Sistema RAG com LangChain - Bot de Perguntas e Respostas em PDFs

Este é um sistema RAG (Retrieval-Augmented Generation) que responde perguntas com base em documentos PDF, utilizando inteligência artificial para buscar e processar informações de forma contextualizada.

---

## 📌 Índice
- [📜 Descrição](#-descrição)
- [🚀 Recursos](#-recursos)
- [🛠 Tecnologias](#-tecnologias)
- [✅ Pré-requisitos](#-pré-requisitos)
- [🔧 Instalação](#-instalação)
- [⚙️ Configuração](#️-configuração)
- [▶️ Uso](#️-uso)
- [💬 Exemplos de Uso](#-exemplos-de-uso)
- [📁 Estrutura do Projeto](#-estrutura-do-projeto)
- [🤝 Contribuição](#-contribuição)
- [📄 Licença](#-licença)

---

## 📜 Descrição  
**Sistema RAG com LangChain** é uma aplicação inteligente construída em Python que permite fazer perguntas sobre o conteúdo de documentos PDF. O sistema utiliza a tecnologia RAG (Retrieval-Augmented Generation) para buscar informações relevantes nos documentos e gerar respostas contextualizadas usando a API da OpenAI.

O projeto é dividido em dois componentes principais:
- **criar_db.py**: Processa os PDFs e cria um banco de dados vetorizado
- **main.py**: Interface de chatbot interativo para fazer perguntas

---

## 🚀 Recursos
- 📄 **Processamento inteligente de PDFs** com extração automática de texto
- 🧠 **Busca semântica avançada** usando embeddings vetoriais
- 💬 **Chatbot interativo** no terminal para perguntas e respostas
- 🎯 **Respostas contextualizadas** baseadas no conteúdo dos documentos
- 💾 **Banco de dados vetorizado** com ChromaDB para buscas rápidas
- 🔐 **Gerenciamento seguro de credenciais** com python-dotenv
- 🔄 **Atualização fácil** da base de conhecimento adicionando novos PDFs

---

## 🛠 Tecnologias

| Camada        | Tecnologias                                            |
| :------------ | :----------------------------------------------------- |
| **Backend**   | Python 3.8+                                            |
| **Framework RAG** | LangChain, LangChain-OpenAI                        |
| **Integração AI** | OpenAI API (embeddings e GPT)                      |
| **Banco Vetorial** | ChromaDB, LangChain-Chroma                        |
| **Processamento PDF** | PyPDF, LangChain-Community                     |
| **Segurança** | python-dotenv (gerenciamento de variáveis de ambiente) |

---

## ✅ Pré-requisitos
Antes de iniciar, certifique-se de ter os seguintes itens instalados:
- Python 3.8 ou superior
- pip (gerenciador de pacotes do Python)
- Virtualenv (recomendado para isolamento do ambiente)
- Git
- Conta na OpenAI com API Key ativa

---

## 🔧 Instalação

1. Clone o repositório para sua máquina local:

    ```bash
    git clone https://github.com/allesantos/Rag-com-langchain.git
    cd Rag-com-langchain
    ```

2. Crie e ative um ambiente virtual:

    ```bash
    python -m venv venv
    source venv/bin/activate  # No Windows: venv\Scripts\activate
    ```

3. Instale as dependências do projeto:

    ```bash
    pip install -r requirements.txt
    ```

    Ou instale manualmente:

    ```bash
    pip install python-dotenv langchain langchain-openai langchain-community langchain-chroma chromadb openai pypdf
    ```

---

## ⚙️ Configuração

1. Crie um arquivo `.env` na raiz do projeto:

    ```bash
    touch .env  # No Windows: type nul > .env
    ```

2. Adicione sua chave da API da OpenAI no arquivo `.env`:

    ```env
    OPENAI_API_KEY=sua-chave-api-aqui
    ```

3. **⚠️ IMPORTANTE:** O arquivo `.env` já deve estar no `.gitignore` para não expor suas credenciais.

4. Adicione seus arquivos PDF na pasta `/base`:

    ```
    /base
      └── seu-documento.pdf
    ```

---

## ▶️ Uso

### 🗄️ Passo 1: Criar o Banco de Dados Vetorizado

Antes de usar o chatbot, você precisa processar os PDFs e criar o banco de dados:

```bash
python criar_db.py
```

Este script irá:
- Ler todos os PDFs da pasta `/base`
- Extrair e dividir o texto em chunks
- Criar embeddings vetoriais
- Armazenar no banco de dados ChromaDB na pasta `/db`

---

### 💬 Passo 2: Interagir com o Chatbot

Após criar o banco de dados, inicie o chatbot:

```bash
python main.py
```

Agora você pode fazer perguntas sobre o conteúdo dos PDFs!

**Exemplo de interação:**

```
Você: Qual é o horário de funcionamento da empresa?

Bot: De acordo com nossos documentos, a empresa funciona de segunda a sexta-feira, 
das 8h às 18h, e aos sábados das 9h às 13h. Estamos fechados aos domingos e feriados.
```

Para sair do chat, digite `sair` ou `exit`.

---

## 🧠 Como Funciona Internamente

1. **Processamento (criar_db.py):**
   - Lê os PDFs da pasta `/base`
   - Extrai o texto usando PyPDF
   - Divide o texto em chunks menores
   - Gera embeddings vetoriais usando OpenAI
   - Armazena os vetores no ChromaDB

2. **Consulta (main.py):**
   - Recebe a pergunta do usuário
   - Converte a pergunta em embedding vetorial
   - Busca os chunks mais relevantes no banco
   - Envia os chunks e a pergunta para o GPT
   - Retorna a resposta contextualizada

---

## 💬 Exemplos de Uso

### 📌 Exemplo 1: Pergunta Sobre Horários
**Pergunta:** "Qual é o horário de funcionamento da empresa?"

**Resposta gerada:**
```
De acordo com nossos documentos, a empresa funciona de segunda a sexta-feira, 
das 8h às 18h, e aos sábados das 9h às 13h. Estamos fechados aos domingos 
e feriados.
```

---

### 📌 Exemplo 2: Consulta Sobre Políticas
**Pergunta:** "Como funciona a política de devolução de produtos?"

**Resposta gerada:**
```
Segundo nossa política, você pode devolver produtos em até 30 dias após 
a compra, desde que estejam em perfeito estado e com a nota fiscal. 
O reembolso é processado em até 7 dias úteis.
```

---

### 📌 Exemplo 3: Informações de Contato
**Pergunta:** "Quais são os canais de atendimento disponíveis?"

**Resposta gerada:**
```
Oferecemos atendimento através dos seguintes canais:
- WhatsApp: (11) 98765-4321
- E-mail: contato@empresa.com
- Chat online no site: disponível 24/7
- Telefone: 0800-123-4567 (segunda a sexta, 8h às 18h)
```

---

## 📁 Estrutura do Projeto

```
Rag-com-langchain/
│
├── .env                    ← Chave da API (não versionar!)
├── .gitignore
├── requirements.txt
├── criar_db.py            ← Cria o banco de dados vetorizado
├── main.py                ← Chatbot interativo
│
├── base/                  ← Coloque seus PDFs aqui
│   └── documento.pdf
│
├── db/                    ← Banco de dados vetorizado (gerado automaticamente)
│   └── chroma/
│
└── venv/                  ← Ambiente virtual (não versionar)
```

---

## 🔄 Atualizando a Base de Conhecimento

Para adicionar novos PDFs ao sistema:

1. Adicione os novos arquivos PDF na pasta `/base`
2. Execute novamente o script de criação:
   ```bash
   python criar_db.py
   ```
3. O banco de dados será atualizado automaticamente

---

## 🤝 Contribuição
Sinta-se à vontade para contribuir com este projeto. Siga estas etapas:

1. Faça um fork do repositório.

2. Crie uma nova branch para sua feature/bugfix:

    ```bash
    git checkout -b minha-feature
    ```

3. Faça commit das suas alterações:

    ```bash
    git commit -m "Adiciona minha feature"
    ```

4. Envie suas alterações:

    ```bash
    git push origin minha-feature
    ```

5. Abra um Pull Request.

---

## 📄 Licença
Este projeto está licenciado sob a **MIT License**.

---

## 🔧 Troubleshooting

### ❌ Erro: "No module named 'langchain'"
**Solução:** Certifique-se de que o ambiente virtual está ativo e instale as dependências:
```bash
pip install -r requirements.txt
```

### ❌ Erro: "OpenAI API key not found"
**Solução:** Verifique se o arquivo `.env` existe e contém a chave correta:
```env
OPENAI_API_KEY=sua-chave-aqui
```

### ❌ Erro: "No PDFs found in /base"
**Solução:** Adicione pelo menos um arquivo PDF na pasta `/base`

---

## 📞 Contato

Desenvolvido com ❤️ por **Alexandre Santos**

- 📧 Email: alledesenvolvimento@gmail.com
- 💼 LinkedIn: www.linkedin.com/in/alle-carlos-alexandre
- 🐙 GitHub: github.com/allesantos

---

## 🎯 Próxima versão deste meu app

- [ ] Interface web com Flask/Django
- [ ] Suporte para múltiplos idiomas
- [ ] Processamento de outros formatos (DOCX, TXT)
- [ ] Sistema de cache para respostas frequentes
- [ ] Métricas de qualidade das respostas

---

**⭐ Se este projeto foi útil para você, deixe uma estrela no repositório!**