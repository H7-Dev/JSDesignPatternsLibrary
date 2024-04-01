# Issue 😕

**Issue: Eventos de clique sendo disparados duas vezes **

**[Link da Issue](https://github.com/H7-Dev/JSDesignPatternsLibrary/issues/1)**

## Prioridade 🚨: 
Alta

## Visão Geral 🌐
Estamos enfrentando um problema onde os eventos de clique estão sendo registrados duas vezes em nosso sistema de delegação de eventos. Isso resulta em logs duplicados no console e, potencialmente, em ações duplicadas no sistema.

## 🚩 **Problema: 😕**
-  Duplo click em `botaoSeletor` registrando o mesmo evento de clique duas vezes
- Evento disparado para o mesmo botão
- Mesmo sem nenhuma instância duplicada da classe detectada

## 🔍 **Análise do Problema: 😣**
- Eventos de clique podem estar se propagando mais de uma vez devido à reconstrução dinâmica dos elementos
- A atual configuração do ouvinte de eventos não previne a duplicação

## 📋 Lista de Tarefas
- [x] Revisar a implementação da delegação de eventos
    Garantir que os ouvintes de eventos estão sendo adicionados corretamente e não são duplicados.

- [x] Adicionar a flag `eventConfigured`
    Implementar uma flag para prevenir a adição múltipla de ouvintes de eventos no mesmo elemento.

- [x] Refatorar o método `setupDelegatedEvent`
    Incluir a lógica de remoção do ouvinte de evento anterior antes de adicionar um novo.

- [x] Testar a nova implementação
    Realizar testes para confirmar que a duplicação de eventos foi resolvida.

- [x] Documentar a solução no sistema de rastreamento de issues
    Criar e preencher um issue detalhando o problema, a análise, a solução implementada e o código relevante.


## 🛠️ **Solução Implementada: 🤩**
- Implementação de uma flag para verificar se o evento já foi configurado
- Remoção de ouvintes de eventos anteriores antes de adicionar novos para prevenir duplicação
- Testes confirmam que a duplicação de eventos foi resolvida

**Trecho de código relevante:**

```javascript
class ClickEventDelegatorModel extends DomReadyComponent {
    // ...

    constructor(options) {
        super();
        this.options = options;
        this.eventConfigured = false;
        this.delegatedEventHandler = null;
    }

    // ...

    setupDelegatedEvent() {
        const container = document.getElementById(this.options.containerId);

        // Remova o evento anterior se já existir
        if (this.delegatedEventHandler) {
            container.removeEventListener('click', this.delegatedEventHandler);
        }

        // Adiciona o novo evento
        this.delegatedEventHandler = (e) => {
            // Lógica do manipulador de eventos
        };

        container.addEventListener('click', this.delegatedEventHandler);
        this.eventConfigured = true;
    }
}

```

## Data de Vencimento (Due Date): 
N/A

## Referências: 
- Discussões internas com a equipe de desenvolvimento
- Documentação do MDN sobre `EventTarget.addEventListener()` e `EventTarget.removeEventListener()`

---

Este trecho de código mostra como a solução foi implementada para garantir que os ouvintes de eventos não sejam duplicados, mesmo quando os elementos são dinamicamente reconstruídos.


🔑 **Pontos-Chave da Solução:**
- Adição da propriedade `eventConfigured` para atuar como uma flag
- Utilização do método `removeEventListener` para remover ouvintes antigos antes de adicionar novos

## Data de Vencimento (Due Date): 
N/A

## Referências: 
- Discussões internas com a equipe de desenvolvimento
- Documentação do MDN sobre `EventTarget.addEventListener()` e `EventTarget.removeEventListener()`

--- 

Este issue fornece uma visão clara do problema enfrentado, como ele foi analisado e a solução que foi implementada para resolver o problema. Ele pode ser utilizado para futuras referências e como uma parte do conhecimento compartilhado da equipe.


# Mensagem Commit

**01.01 - ClickEventDelegatorModel -v1.1.0**

Statu: Funcional ✔️

feat:
- Implementada flag `eventConfigured` para garantir a adição única de ouvintes de evento.
- Refatorado o método `setupDelegatedEvent` para remover ouvintes de eventos antigos antes da adição de novos.
- Conduzidos testes para assegurar que eventos de clique não são mais duplicados.
- Adicionado trecho de código relevante à documentação da issue para esclarecer a solução implementada.
- Documentada a solução de eventos duplicados no sistema de rastreamento de issues para referência futura.

Versão:
- Fase do projeto: Alfa
- Versão da tabela: 1.1.0
- Linguagem: JavaScript

Resumo do Commit: Resolvida a issue de eventos de clique duplicados na delegação de eventos com a implementação de uma flag e aprimoramento na lógica de adição/remoção de ouvintes de eventos. O sistema agora corretamente registra um único evento por ação do usuário, conforme confirmado pelos testes realizados.

---

Esta mensagem de commit documenta as mudanças feitas em resposta à issue, proporciona um resumo do que foi feito e atualiza as informações de versão do projeto.

[Issue](https://github.com/H7-Dev/JSDesignPatternsLibrary/issues/1)