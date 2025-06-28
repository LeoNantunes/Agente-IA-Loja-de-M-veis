## 🚀 Como Executar este Projeto

Este projeto utiliza uma arquitetura de **sub-fluxos** no N8N. Para executá-lo corretamente, siga os passos abaixo:

1.  **Importe os 3 Fluxos:** Importe os três arquivos JSON (`workflow-principal-roteador.json`, `subworkflow-catalogo.json`, e `subworkflow-detalhes-e-orcamento.json`) para a sua instância do N8N.

2.  **Ative os Sub-fluxos:** Ative os dois sub-fluxos (`subworkflow-catalogo` e `subworkflow-detalhes-e-orcamento`) para que o N8N gere as URLs de Webhook de produção para cada um deles.

3.  **Copie as Novas URLs:**
    * Abra o sub-fluxo de catálogo, clique no nó "Webhook" e copie sua URL de produção.
    * Abra o sub-fluxo de detalhes, clique no nó "Webhook" e copie sua URL de produção.

4.  **Conecte os Fluxos:**
    * Vá para o **workflow principal**. Encontre o nó de `HTTP Request` chamado "**parteDois**". Cole a URL do **sub-fluxo de catálogo** neste nó.
    * Vá para o **sub-fluxo de catálogo**. Encontre o nó de `HTTP Request` chamado "**parteTres1**". Cole a URL do **sub-fluxo de detalhes** neste nó.

5.  **Configure as Credenciais:** Em cada um dos três workflows, o N8N solicitará que você associe suas próprias credenciais para os nós de **Supabase, Redis e OpenAI**.

6.  **Ative o Fluxo Principal:** Após conectar tudo, ative o workflow principal. Agora o sistema está pronto para receber mensagens.
