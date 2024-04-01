# Feature ✨

**feat: Implementação da Delegação de Eventos com ClickEventDelegatorModel**    

## Visão Geral 📄🧐

Implementação de uma classe JavaScript para otimizar a manipulação de eventos de clique em uma aplicação web, utilizando a técnica de delegação de eventos. A classe `ClickEventDelegatorModel` permite uma abordagem eficiente, especialmente em cenários com um grande número de elementos interativos.

## Contexto 🌍
A feature será implementada em um ambiente web onde elementos interativos são carregados dinamicamente. Isso é comum em aplicações SPA (Single Page Applications) ou em páginas que recebem conteúdo atualizado frequentemente via AJAX.

## Motivação 💡
A necessidade surge da limitação de performance ao adicionar ouvintes de eventos a cada elemento individualmente em uma página com muitos elementos interativos. Isso pode levar a um uso excessivo de recursos e atrasos na resposta do usuário. A delegação de eventos resolve isso ao reduzir o número de ouvintes de eventos necessários.

## Cenário 
Em uma página web que carrega milhares de cartões de conteúdo (`card-ma`), cada um com botões para ações específicas (como favoritar ou abrir mais opções), a técnica de delegação de eventos permite adicionar um único ouvinte de evento a um contêiner pai. Esse ouvinte gerencia todos os cliques nos botões, independentemente do número de elementos, otimizando a performance e a gestão de eventos.

## Requisitos 📝
- Um contêiner pai com um ID específico para ancorar a delegação de eventos.
- Seletores CSS precisos para identificar corretamente os elementos-alvo dos eventos de clique dentro do contêiner.
- JavaScript ES6+ para suporte a classes e outras funcionalidades modernas da linguagem.

## Testes 🧪
- [x] Testes locais para validar a funcionalidade com diferentes estruturas de DOM e números de elementos.
- [ ] Testes em servidor não aplicáveis.
- [ ] Testes de integração para avaliar a interação com outras partes da aplicação.
- [ ] Testes de aceitação para garantir que a funcionalidade atende às expectativas do usuário final.

## ▶ Fluxo Lógico 🧠

1. A classe `ClickEventDelegatorModel` é inicializada com o ID do contêiner e o seletor dos elementos-alvo.
2. A classe aguarda o carregamento completo do DOM.
3. Um ouvinte de evento é adicionado ao contêiner especificado.
4. O ouvinte delega os eventos de clique para os elementos-alvo, baseando-se no seletor fornecido.

## 🆕 Versão 🔢
- [x] Fase do projeto: Alfa
- [x] Versão da classe/código: 1.0.0
- [x] Linguagem: JavaScript


## Nota de Dependência 📌
Esta feature depende diretamente da classe `DomReadyComponent.js` para garantir que a delegação de eventos seja aplicada apenas após o carregamento completo do DOM. É crucial que `DomReadyComponent.js` esteja corretamente incluído e inicializado no projeto antes de utilizar `ClickEventDelegatorModel`. Para mais detalhes sobre a classe `DomReadyComponent.js`, consulte [a documentação ou o código fonte aqui](CLASSES\DomReadyComponent.class.js.md).

## 🛠️ Implementação da classe

A classe `ClickEventDelegatorModel` oferece uma solução escalável para a gestão de eventos de clique em aplicações web dinâmicas.


```JS
class ClickEventDelegatorModel extends DomReadyComponent {
    constructor(options) {
        super();
        this.options = options;
        this.eventConfigured = false; // Flag para verificar se o evento já foi configurado
        this.delegatedEventHandler = null; // Referência ao manipulador para poder remover mais tarde
    }

    initialize() {
        super.initialize();

        // Aguardar a DOM estar pronta pode ser necessário se a classe pai também estiver esperando
        document.addEventListener('DOMContentLoaded', () => {
            if (!this.initializedSuccessfully) {
                console.error("A inicialização da classe pai falhou. A instância de ClickEventDelegatorModel não será funcional.");
                return;
            }

            // Configura o evento se ainda não estiver configurado
            if (!this.eventConfigured) {
                this.setupDelegatedEvent();
                this.eventConfigured = true;
            }
        });
    }

    setupDelegatedEvent() {
        const container = document.getElementById(this.options.containerId);

        if (!container) {
            console.error(`O elemento pai ${this.options.containerId} não foi encontrado.`);
            return;
        }

        // Remova o evento anterior se já existir
        if (this.delegatedEventHandler) {
            container.removeEventListener('click', this.delegatedEventHandler);
        }

        this.delegatedEventHandler = (e) => {
            const targetButton = e.target.closest(this.options.botaoSeletor);
            if (targetButton) {
                console.log('Botão Mais clicado:', targetButton);
                // Implementação específica do que deve acontecer quando o botão é clicado
            }
        };

        container.addEventListener('click', this.delegatedEventHandler);
    }

    static init(options) {
        const instance = new ClickEventDelegatorModel(options);
        instance.initialize();
        return instance;
    }
}

```
_Como instanciar_
```JS

// Exemplo de uso
ClickEventDelegatorModel.init({
    containerId: 'divTopicosFluxoScroll_2', // O ID do contêiner onde os eventos de clique serão delegados.
    botaoSeletor: '.btn-card-ma-link-mais' // O seletor CSS dos botões para adicionar eventos de clique.
});

```

## Amostra genérica 📄🌐
Aqui está um exemplo de HTML genérico que demonstra como a classe `ClickEventDelegatorModel` pode ser aplicada. Este exemplo inclui um contêiner com vários botões que simulam a situação descrita, como botões dentro de cartões (`card-ma`) que são manipulados através de delegação de eventos.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Delegação de Eventos com ClickEventDelegatorModel</title>
    <style>
        .card {
            border: 1px solid #ddd;
            margin: 10px;
            padding: 10px;
            border-radius: 5px;
            background-color: #f9f9f9;
        }
        .buttonClick {
            cursor: pointer;
            padding: 5px 10px;
            border: none;
            border-radius: 5px;
            background-color: #007bff;
            color: white;
            margin: 5px;
        }
    </style>
</head>
<body>

<div id="container_pai">
    <div class="card">
        <button type="button" class="buttonClick">Mais Opções 1</button>
    </div>
    <div class="card">
        <button type="button" class="buttonClick">Mais Opções 2</button>
    </div>
    <!-- Mais elementos card podem ser adicionados aqui -->
</div>

<script src="path/to/your/DomReadyComponent.js"></script>
<script src="path/to/your/ClickEventDelegatorModel.js"></script>
<script>
    ClickEventDelegatorModel.init({
        containerId: 'container_pai',
        botaoSeletor: '.buttonClick'
    });
</script>

</body>
</html>
```

Neste exemplo, o contêiner `div#container_pai` possui vários elementos `.card`, cada um contendo um botão `.btn-card-link-mais`. A classe `ClickEventDelegatorModel` é inicializada com o ID desse contêiner e o seletor dos botões. Isso significa que, quando qualquer um desses botões é clicado, o manipulador de eventos definido na classe `ClickEventDelegatorModel` é acionado.

Note que os caminhos para os scripts `DomReadyComponent.js` e `ClickEventDelegatorModel.js` devem ser atualizados para refletir o local correto dos arquivos JavaScript em seu projeto.

Esse HTML serve como uma demonstração de como integrar e utilizar a classe `ClickEventDelegatorModel` em uma página web para gerenciar eventos de clique de maneira eficiente, especialmente em cenários com elementos dinâmicos.

Essa implementação permite uma interação eficiente e responsiva em páginas web com grande volume de conteúdo interativo, melhorando significativamente a performance e a experiência do usuário.