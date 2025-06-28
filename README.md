# Agente de IA Modular para Atendimento - Loja de Móveis (N8N)

## 📖 Descrição do Projeto

Este projeto é um agente de IA conversacional para a "Rustic Dream House", uma loja de móveis vintage e personalizados. A solução, construída inteiramente na plataforma N8N, se destaca por sua **arquitetura modular baseada em sub-fluxos**, onde cada fluxo é especializado em uma etapa da jornada do cliente, garantindo manutenibilidade e escalabilidade.

O agente interage com os clientes via WhatsApp e é capaz de apresentar um catálogo de produtos obtido através de **web scraping em tempo real** do site da loja, extrair detalhes específicos de cada item (preços, fotos, dimensões), fornecer recomendações e calcular orçamentos de forma dinâmica e autônoma.

---

## 🎯 Objetivos

* **Criar uma Arquitetura Escalável:** Projetar o sistema em sub-fluxos para facilitar a manutenção e a adição de novas funcionalidades sem impactar o fluxo principal.
* **Apresentar Informações em Tempo Real:** Garantir que o catálogo de produtos e seus detalhes estejam sempre atualizados, utilizando web scraping para buscar os dados diretamente do site da loja no momento da consulta.
* **Gerar Orçamentos Dinâmicos:** Calcular orçamentos precisos combinando o valor do produto (obtido via scraping) com taxas de frete (armazenadas em banco de dados) baseadas na região do cliente.
* **Implementar Controle de Sessão:** Utilizar Redis para criar um mecanismo de "rate limiting" que previne o processamento de mensagens duplicadas e garante a estabilidade do bot.
* **Reduzir Carga Operacional:** Automatizar o atendimento inicial e a qualificação de leads, liberando a equipe de vendas para focar em negociações e no relacionamento com o cliente.

---

## ⚙️ Tecnologias e Técnicas Utilizadas

* **Automação e Arquitetura:** N8N (com uma arquitetura baseada em sub-fluxos).
* **Inteligência Artificial:** OpenAI (GPT-4o Mini).
* **Orquestração de IA:** LangChain.
* **Banco de Dados:**
    * **Supabase:** Para armazenamento de dados de clientes e taxas de entrega.
    * **Redis:** Para controle de sessão temporário e mecanismo anti-spam.
* **Técnica Chave:** **Web Scraping** em tempo real com Nós HTTP e parsing de HTML com JavaScript/Regex.
* **Comunicação:** WhatsApp (via API).
* **Scripting:** JavaScript.

---

## 🛠️ Como Usar e Executar o Projeto

Este projeto utiliza uma arquitetura de **sub-fluxos**. Para executá-lo corretamente, siga os passos abaixo:

1.  **Importe os 3 Fluxos:**
    * Baixe os três arquivos `.json` deste repositório:
        * `workflow-principal-roteador.json`
        * `subworkflow-catalogo.json`
        * `subworkflow-detalhes-e-orcamento.json`
    * Na sua instância do N8N, importe cada um dos três arquivos.

2.  **Ative os Sub-fluxos para Obter as URLs:**
    * Primeiro, ative os dois sub-fluxos (`subworkflow-catalogo` e `subworkflow-detalhes-e-orcamento`).
    * Ao ativar, o N8N irá gerar uma URL de Webhook de **PRODUÇÃO** para cada um. Copie essas duas URLs.

3.  **Conecte os Fluxos:**
    * Abra o **workflow principal**. Encontre o nó de `HTTP Request` chamado "**parteDois**". No campo da URL, cole a URL de produção do seu **sub-fluxo de catálogo**.
    * Abra o **sub-fluxo de catálogo**. Encontre o nó de `HTTP Request` chamado "**parteTres1**". No campo da URL, cole a URL de produção do seu **sub-fluxo de detalhes e orçamento**.

4.  **Configure as Credenciais:**
    * Em cada um dos três workflows, o N8N solicitará que você associe suas próprias credenciais para os serviços utilizados: **OpenAI, Supabase e Redis**.

5.  **Ative o Fluxo Principal:**
    * Após conectar tudo, ative o `workflow-principal-roteador.json`. O sistema estará pronto para receber e processar as mensagens.

---

## 🔗 Contato

* **LinkedIn:** [Leonardo Nonato Antunes](linkedin.com/in/leonardo-nonato-0b37aa189/)
* **Email:** Leonardoantunes241@gmail.com
