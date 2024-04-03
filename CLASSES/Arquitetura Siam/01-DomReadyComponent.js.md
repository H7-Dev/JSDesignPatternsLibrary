# DomReadyComponent

**Classe base para verifica o estado de carregamento da DOM e garante que o método de inicialização**
```JS

// DomReadyComponent
/** 
 * Representa um componente que precisa ser inicializado somente após o carregamento completo da DOM.
 * Esta classe base verifica o estado de carregamento da DOM e garante que o método de inicialização
 * seja chamado apenas quando a DOM estiver completamente carregada.
 */
class DomReadyComponent {
    /**
     * Construtor para o componente que aguarda a DOM estar pronta.
     */
    constructor() {
        /**
         * Indica se a inicialização foi concluída com sucesso.
         * @type {boolean}
         */
        this.initializedSuccessfully = false;

        if (document.readyState !== "loading") {
            // Se a DOM já estiver carregada, inicializa imediatamente.
            this.initialize();
        } else {
            // Caso contrário, aguarda o evento de carregamento da DOM.
            document.addEventListener("DOMContentLoaded", () => {
                this.initialize();
            });
        }
    }

    /**
     * Método de inicialização que deve ser sobrescrito pelas classes filhas
     * para implementar lógicas específicas de inicialização.
     * Define `initializedSuccessfully` como verdadeiro após a inicialização.
     */
    initialize() {
        // Implementações específicas de inicialização devem ser providas pelas subclasses.
        console.log("✅ Inicialização bem-sucedida!");
        this.initializedSuccessfully = true;
    }
}

```
