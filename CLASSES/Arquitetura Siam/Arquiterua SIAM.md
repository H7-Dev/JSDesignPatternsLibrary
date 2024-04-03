# Feature ✨

**feat: Implementação da Arquitetura Siam  `DelegateEventListenerBaseClick`**

_O fluxo: é Abstração, Sistem de Delegação de Eventos  e Modularidade_

## Visão Geral 📄🧐

Este documento descreve a implementação de uma arquitetura baseada em classes para facilitar a modularização e a eficiência na delegação de eventos em aplicações web, permitindo que desenvolvedores concentrem-se nas responsabilidades específicas de cada componente sem a necessidade de gerenciar o carregamento da DOM e a delegação de eventos manualmente.

## Contexto 🌍

Em aplicações web modernas, é comum a necessidade de interagir com elementos da DOM que podem não estar disponíveis imediatamente. Além disso, a gestão eficiente de eventos, como cliques, é fundamental para a interatividade do usuário. Neste cenário, busca-se simplificar o processo de desenvolvimento de componentes interativos.

## Motivação 💡

A motivação central para esta iniciativa é abordar e solucionar a repetitividade e a redundância encontradas na gestão de eventos e na verificação do carregamento da Document Object Model (DOM) em múltiplos componentes de uma aplicação web. Frequentemente, desenvolvedores se veem reescrevendo ou copiando e colando blocos de código similares para cada nova classe que gerencia eventos, o que não só aumenta a quantidade de código como também amplia a margem para erros e inconsistências. 

Este desafio torna-se ainda mais evidente em projetos de grande porte ou em aplicações que operam em um ambiente dinâmico, onde os elementos da página podem ser adicionados, removidos ou alterados com regularidade. A duplicação de código relacionado à inicialização de componentes após o carregamento completo da DOM e à configuração de delegações de eventos contribui para um código base inflado e mais complexo, dificultando a manutenção e escalabilidade do projeto.

Neste contexto, a feature proposta visa simplificar e padronizar o processo de inicialização de componentes e de delegação de eventos. Ao centralizar essas responsabilidades comuns em uma ou mais classes base, espera-se que os desenvolvedores possam dedicar mais atenção à lógica específica e às funcionalidades únicas de cada componente. Esse enfoque não apenas promove a criação de um código mais limpo e modular, mas também potencializa a eficiência do desenvolvimento e a facilidade de manutenção ao longo do tempo.

Consequentemente, a proposta objetiva elevar a qualidade do desenvolvimento de software, facilitando a implementação de componentes interativos mais robustos e confiáveis, ao mesmo tempo em que se reduz o volume de código necessário e se minimizam as chances de erro. Esta abordagem reflete uma evolução significativa na maneira como lidamos com a complexidade inerente à manipulação de eventos em aplicações web, marcando um avanço na direção de práticas de desenvolvimento mais sustentáveis e escaláveis.

## Requisitos 📝

- **Abstração para Carregamento da DOM**: Uma classe base que automatiza a verificação do carregamento da DOM, garantindo que os componentes só se inicializem quando a DOM estiver pronta.
- **Sistema de Delegação de Eventos**: Implementação de um sistema que permita a delegação de eventos a partir de um container pai, evitando a necessidade de adicionar ouvintes de eventos para cada elemento individualmente.
- **Modularidade e Extensibilidade**: Classes filhas devem poder estender a classe base sem se preocupar com a inicialização e a delegação de eventos, focando apenas em suas funcionalidades específicas.
<!-- ASMEX -->
<!-- Siam - Sistem de Delegação de Eventos, Abstração e Modularidade -->
## Testes 🧪

- [x] **Testes Locais**: Verificar o correto funcionamento da inicialização de componentes e a delegação de eventos em um ambiente de desenvolvimento local.
- [ ] **Testes em Servidor**: Avaliar o comportamento da feature em um ambiente de servidor, incluindo carga e performance.
- [ ] **Testes de Integração**: Garantir que a feature interaja corretamente com outras partes da aplicação.
- [ ] **Testes de Aceitação**: Confirmar que a feature atende aos requisitos dos usuários finais.

## ▶ Fluxo Lógico 🧠

1. Verificação do estado de carregamento da DOM.
2. Inicialização de componentes somente após a DOM estar pronta.
3. Configuração da delegação de eventos para elementos dentro de containers específicos.
4. Classes filhas implementam lógica específica de interação sem se preocupar com detalhes de inicialização e delegação.
5. Este modelo é um exemplo clássico de padrões de design em programação orientada a objetos, combinando a herança, polimorfismo e composição de maneiras que facilitam a extensibilidade, a reutilização de código e a separação de preocupações.

### Padrões de Design Relevantes

1. **Template Method**: A implementação da classe `DomReadyComponent` e a forma como a classe `DelegateEventListenerBaseClick` a estende, utilizando o método `initialize` como um gancho para a execução de código específico de inicialização, demonstra o padrão Template Method. Este padrão permite definir o esqueleto de um algoritmo, deixando alguns passos para serem implementados por subclasses. `initialize` atua como um método template, com etapas específicas implementadas pelas subclasses.

2. **Strategy**: O método `handleEvent` na classe `DelegateEventListenerBaseClick`, projetado para ser sobrescrito pelas subclasses como `TimerEventHandler`, exemplifica o padrão Strategy. Este padrão permite a seleção do comportamento de um objeto em tempo de execução. Assim, `handleEvent` serve como uma estratégia para o tratamento de eventos, definida especificamente por cada subclass.

3. **Decorator**: Embora não implementado explicitamente, o conceito de adicionar responsabilidades dinamicamente a objetos está implicitamente presente na maneira como a delegação de eventos é manuseada. Em contextos mais complexos, o padrão Decorator pode ser utilizado para adicionar comportamentos específicos aos eventos de forma dinâmica.

4. **Factory Method ou Constructor**: A criação de instâncias de classes via construtores em JavaScript, juntamente com a passagem de configurações como opções, segue o padrão Factory Method. Este padrão está presente no uso dos construtores para criar objetos, facilitando a customização das instâncias criadas.

### Nomenclatura e Reconhecimento

Embora não exista um único termo para descrever a combinação específica de herança, polimorfismo e delegação de eventos, a prática de utilizar classes base para prover funcionalidades comuns que podem ser estendidas ou customizadas pelas subclasses é amplamente reconhecida na programação orientada a objetos. Esta abordagem é particularmente valiosa no desenvolvimento front-end para o gerenciamento eficiente de eventos na DOM, refletindo os princípios SOLID, especialmente o Princípio Aberto/Fechado, que preconiza que classes devem ser abertas para extensão, mas fechadas para modificação.

### Novo Termo
As características da sua implementação tocam em múltiplos padrões de design, como mencionado anteriormente (Template Method, Strategy, entre outros), mas nenhum nome singular captura completamente a essência de combinar herança para extensão de funcionalidade com a flexibilidade do polimorfismo e a eficiência da delegação de eventos.

Em contextos de desenvolvimento web e JavaScript, talvez você possa considerar isso parte do que alguns chamariam de "Component-Based Architecture" ou "Event-Driven Design", mas esses termos são mais amplos e não especificam exatamente a combinação de técnicas que você está usando.

A sua abordagem é um exemplo excelente de aplicação prática de vários princípios de design orientado a objetos e padrões de design para criar um sistema flexível e extensível para manipulação de eventos em aplicações web.

Portano eu o chamo de **`Siam - Sistem de Delegação de Eventos, Abstração e Modularidade`**



## 🆕 Versão 🔢

- [x] **Fase do Projeto**: Alfa
- [x] **Versão da Classe/Código**: 1.0.0
- [x] **Linguagem**: JavaScript

## 🛠️ Implementação 

### **Abstração**

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

### **Sistem de Delegação de Eventos**

#### **Classe Js de Amostra**
```JS
// *Cenário #001
class TimerEventHandler extends DelegateEventListenerBaseClick {
    constructor(options) {
        super(options);
        this.isRunning = false;
        this.elapsed = 0; // Tempo decorrido em segundos
    }

    handleEvent(targetElement) {
        if (!this.isRunning) {
            this.startTimer();
        } else {
            this.stopTimer();
        }
    }

    startTimer() {
        if (!this.isRunning) {
            this.isRunning = true;
            const updateTimer = () => {
                if (!this.isRunning) return;
                this.elapsed++;
                this.displayTime();
                setTimeout(updateTimer, 1000);
            };
            updateTimer();
        }
    }

    stopTimer() {
        this.isRunning = false;
    }

    displayTime() {
        const minutes = Math.floor(this.elapsed / 60).toString().padStart(2, '0');
        const seconds = (this.elapsed % 60).toString().padStart(2, '0');
        console.clear(); // Limpa o console para simular a atualização da mesma linha
        console.log(`${minutes}:${seconds}`);
    }

    // Método estático que serve como um método fábrica
    static init(config) {
        const instance = new TimerEventHandler(config);
        instance.initialize(); // Chama o método initialize para configurar o ouvinte de eventos
        return instance;
    }
}
const timerEventHandler = TimerEventHandler.init({
    containerId: 'containerId_001',
    botaoSeletor: '.botaoSeletorAqui'
});

// *Cenário #002
class ClickCounterEventHandler extends DelegateEventListenerBaseClick {
    constructor(options) {
        super(options);
        this.count = 0; // Inicializa o contador com zero
    }

    handleEvent(targetElement) {
        this.incrementCounter();
    }

    incrementCounter() {
        this.count++; // Incrementa o contador
        console.clear(); // Limpa o console para simular a atualização da mesma linha
        console.log(`Contagem atual: ${this.count}`); // Exibe o valor atual do contador no console
    }

    // Método estático que serve como um método fábrica
    static init(config) {
        const instance = new ClickCounterEventHandler(config);
        instance.initialize(); // Chama o método initialize para configurar o ouvinte de eventos
        return instance;
    }
}
ClickCounterEventHandler.init({
    containerId: 'containerId_002',
    botaoSeletor: '.botaoSeletorAqui'
});

// *Cenário #003
class MenuToggleEventHandler extends DelegateEventListenerBaseClick {
    constructor(options) {
        super(options);
        this.menuOpen = false; // Estado inicial do menu: fechado
    }

    handleEvent(targetElement) {
        // Alternar o estado do menu a cada clique
        this.toggleMenu();
    }

    toggleMenu() {
        this.menuOpen = !this.menuOpen; // Inverte o estado atual do menu
        console.log(this.menuOpen ? 'Menu aberto' : 'Menu fechado');
    }

    // Método estático que serve como um método fábrica
    static init(config) {
        const instance = new MenuToggleEventHandler(config);
        instance.initialize(); // Chama o método initialize para configurar o ouvinte de eventos
        return instance;
    }
}

// Inicialização da classe MenuToggleEventHandler para o botão de menu
MenuToggleEventHandler.init({
    containerId: 'containerId_003',
    botaoSeletor: '.button-menu-dots' // Especifica que esta instância lida apenas com o botão de menu
});


class FavoritarToggleEventHandler extends DelegateEventListenerBaseClick {
    constructor(options) {
        super(options);
        this.menuOpen = false; // Estado inicial do menu: fechado
    }

    handleEvent(targetElement) {
        // Alternar o estado do menu a cada clique
        this.toggleMenu();
    }

    toggleMenu() {
        this.menuOpen = !this.menuOpen; // Inverte o estado atual do card
        console.log(this.menuOpen ? 'Card Favoritado' : 'Card Desfavoritado');
    }

    // Método estático que serve como um método fábrica
    static init(config) {
        const instance = new FavoritarToggleEventHandler(config);
        instance.initialize(); // Chama o método initialize para configurar o ouvinte de eventos
        return instance;
    }
}

// Inicialização da classe FavoritarToggleEventHandler para o botão de menu
FavoritarToggleEventHandler.init({
    containerId: 'containerId_003',
    botaoSeletor: '.button-favoritar' // Especifica que esta instância lida apenas com o botão de menu
});

```

#### **Html E Scss de Amostra**

```HTML
<div class="pagina-para-teste">
    <div class="header">
        <span>Header</span>
    </div>
    <div class="main" >
        <!-- *Cenário #001 -->
        <fieldset id="containerId_001">
            <legend>Container #001</legend>
            <button class="botaoSeletorAqui">Botão De Teste <i>containerId_001</i></button>
            <button class="botaoSeletorAqui">Botão De Teste #002 <i>containerId_001</i></button>
        </fieldset>
        <!-- *Cenário #002 -->
        <fieldset id="containerId_002">
            <legend>Container #001</legend>
            <button class="botaoSeletorAqui">Botão De Teste <i>containerId_001</i></button>
            <button class="botaoSeletorAqui">Botão De Teste #002 <i>containerId_001</i></button>
        </fieldset>
        <br>
        <br>
        <!-- *Cenário #003 -->
        <div class="card" id="containerId_003">
            <legend>Card </legend>
            <br>
            <button class="button-menu-dots">Botão De Teste <i>(Aqui seria um button-menu-dots) <br>do mesmo card </i></button>
            <button class="button-favoritar">Botão De Teste #002 <i>(Aqui seria um button-favoritar) <br>do mesmo card</i></button>
        </div>
    </div>
</div>
```
**SCSS**
```SCSS
.pagina-para-teste {
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    justify-content: normal;
    align-items: normal;
    align-content: normal;
    background-color: rgb(245, 245, 245);
    height: 100%;
    padding: 0.75em 0.8em;
    position: relative;

    >div.header {
        display: flex;
        flex-grow: 0;
        flex-shrink: 1;
        flex-basis: auto;
        align-self: auto;
        order: 0;
        // 
        background-color: cornflowerblue;
        padding: 1em 2em;
        overflow-y: hidden;
        overflow-x: auto;
    }
    >div.main {
        background-color: gainsboro;
        display: flex;
        flex-direction: row;
        align-items: center;
        height: 100%;
        justify-content: center;

        >fieldset {
            display: flex;
            gap: 0.75em;
            flex-direction: column;
            padding: 0.75em;
        }
        >div.card {
            background-color: silver;
            padding: 1em;
            height: 250px;
            width: 350px;
        }
    }
}
```

### **Modularidade**

 - A criação de instâncias de classes via construtores em JavaScript, juntamente com a passagem de configurações como opções, segue o padrão Factory Method. 
 - Este padrão está presente no uso dos construtores para criar objetos, facilitando a customização das instâncias criadas.


#### Amostra JS
 ```JS
 /**
 * Método estático que atua como um método fábrica para criar e inicializar uma instância da classe.
 * Este método facilita a criação de instâncias, encapsulando a construção e a inicialização inicial em uma única chamada.
 * 
 * @param {Object} config - Configurações necessárias para a inicialização da instância.
 * @returns {TimerEventHandler} Uma nova instância de TimerEventHandler configurada e inicializada.
 */
static init(config) {
    const instance = new TimerEventHandler(config);
    instance.initialize(); // Chama o método initialize para configurar o ouvinte de eventos
    return instance;
}

 ```




