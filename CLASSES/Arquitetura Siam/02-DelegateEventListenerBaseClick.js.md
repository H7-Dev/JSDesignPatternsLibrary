# DelegateEventListenerBaseClick

**Classe base para delegação de eventos de clique, estendendo `DomReadyComponent`.**

```JS

// DelegateEventListenerBaseClick 
/**
 * Classe base para delegação de eventos de clique, estendendo `DomReadyComponent`.
 * Essa classe configura a delegação de eventos de clique para elementos específicos dentro de um container,
 * permitindo que subclasses implementem comportamentos específicos ao tratar esses eventos.
 */
class DelegateEventListenerBaseClick extends DomReadyComponent {
    /**
     * Cria uma instância de `DelegateEventListenerBaseClick`.
     * @param {Object} options - Configurações para a delegação de eventos.
     * @param {string} options.containerId - O ID do contêiner onde os eventos de clique serão delegados.
     * @param {string} options.botaoSeletor - O seletor CSS dos botões para adicionar eventos de clique.
     */
    constructor(options) {
        super();
        /**
         * Configurações para a delegação de eventos.
         * @type {Object}
         */
        this.options = options;

        /**
         * Flag para verificar se o evento já foi configurado.
         * @type {boolean}
         */
        this.eventConfigured = false;

        /**
         * Referência ao manipulador de eventos para possibilitar a remoção posterior.
         * @type {Function|null}
         */
        this.delegatedEventHandler = null;
    }

    /**
     * Inicializa o componente, configurando a delegação de eventos de clique após a DOM estar pronta.
     * Sobrescreve o método `initialize` da classe `DomReadyComponent`.
     */
    initialize() {
        super.initialize();

        document.addEventListener('DOMContentLoaded', () => {
            if (!this.initializedSuccessfully) {
                console.error("A inicialização da classe base falhou. Esta instância não será funcional.");
                return;
            }

            if (!this.eventConfigured) {
                this.setupDelegatedEvent();
                this.eventConfigured = true;
            }
        });
    }

    /**
     * Configura a delegação de eventos de clique para o container especificado nas opções.
     * Este método prepara o manipulador de eventos para delegar cliques em botões específicos.
     */
    setupDelegatedEvent() {
        const container = document.getElementById(this.options.containerId);

        if (!container) {
            console.error(`O elemento pai ${this.options.containerId} não foi encontrado.`);
            return;
        }

        if (this.delegatedEventHandler) {
            container.removeEventListener('click', this.delegatedEventHandler);
        }

        this.delegatedEventHandler = (e) => {
            const targetButton = e.target.closest(this.options.botaoSeletor);
            if (targetButton) {
                console.log('Botão clicado:', targetButton);
                this.handleEvent(targetButton);
            }
        };

        container.addEventListener('click', this.delegatedEventHandler);
    }

    /**
     * Método destinado a ser sobrescrito pelas classes filhas para implementar a lógica específica
     * de manipulação de eventos de clique. Este método é chamado quando um evento de clique é capturado
     * pelo manipulador de eventos delegado.
     * @param {Element} targetElement - O elemento alvo do evento de clique.
     */
    handleEvent(targetElement) {
        console.warn('handleEvent não foi sobrescrito na classe filha.');
    }
}
```
